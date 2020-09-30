# User preference recommendation system

This topic describes how to use the HyperLogLog \(HLL\) plug-in to design a recommendation system, which recommends content to a user based on the preferences of the user. The recommendation system is implemented based on similarity computing of PostgreSQL.

A recommendation system can be used to increase user stickiness and conversion rate for the following websites:

-   E-commerce websites
-   Music websites
-   News websites
-   App websites

In this topic, a music website is used as an example to describe how to design a recommendation system and elaborate on the differences between the conventional design and the design that is based on HHL and similarity computing of PostgreSQL.

## Design background

1.  After a user \(uid\) finishes listening to a song \(vid\), the recommendation system binds a tag \(tagid\) to the song. More than one tag is allowed per song.

    ```
    uid ->> tags ->> musics    
    ```

2.  The recommendation system obtains the popularity of each tag based on the number of songs to which the tag is bound.

    ```
    tag(count distinct music)    
    ...   
    ```

3.  The recommendation system obtains the top 5 tags and their recommendation weights.

    ```
    tag1:40%    
    tag2:20%    
    tag3:15%    
    tag4:15%    
    tag5:10%  
    ```

4.  The recommendation system excludes the songs to which the user finishes listening. The recommendation system obtains a library of songs to which the user has not listened. Then, the recommendation system recommends new songs to the user based on the recommendation weights of the songs in the library. For example, the recommendation weights can be the rankings of the songs in descending order.

## Conventional design

The conventional design is suitable for all types of databases. However, if your database system has a large amount of data, the conventional design may use aggregate queries that run slowly. Example:

```
create table t_like(     
uid int,  -- The ID of a user.    
tagid int,  -- The ID of the tag that is bound to a song.   
vid int,   -- The ID of a song.    
mod_time timestamp,  -- The time of the last update. An update is triggered only when one day has passed since the last update.    
primary key (uid,tagid,vid)     
);    
    
insert into t_like values (:uid, :tagid, :vid, :mod_time)     
 on conflict (uid,tagid,vid) do update    
set mod_time=excluded.mod_time    
where    
excluded.mod_time - t_like.mod_time > interval '1 day'    
;    
    
-- Obtain the top 10 tags over the last day.    
select tagid, count(*) from t_like     
where uid=:uid     
and now()-mod_time < interval '1 day'  
group by tagid     
order by count(*) desc limit 10;    
```

The following code snippet is an example of stress testing:

```
vi test.sql  
\set uid random(1,50000)    
\set tagid random(1,5000)    
\set vid random(1,10000000)    
insert into t_like values (:uid, :tagid, :vid, now())     
 on conflict (uid,tagid,vid) do update    
set mod_time=excluded.mod_time    
where    
excluded.mod_time - t_like.mod_time > interval '1 day';    
  
pgbench -M prepared -n -r -P 1 -f ./test.sql -c 32 -j 32 -T 240  
  
transaction type: ./test.sql  
scaling factor: 1  
query mode: prepared  
number of clients: 32  
number of threads: 32  
duration: 240 s  
number of transactions actually processed: 80975327  
latency average = 0.095 ms  
latency stddev = 0.340 ms  
tps = 337396.279382 (including connections establishing)  
tps = 337406.018908 (excluding connections establishing)  
statement latencies in milliseconds:  
         0.000  \set uid random(1,50000)    
         0.000  \set tagid random(1,5000)    
         0.000  \set vid random(1,10000000)    
         0.094  insert into t_like values (:uid, :tagid, :vid, now())    
  
db1=# select tagid, count(*) from t_like     
where uid=1        
and now()-mod_time < interval '1 day'  
group by tagid     
order by count(*) desc limit 10;    
 tagid | count   
-------+-------  
  2519 |     4  
  3049 |     4  
  3648 |     4  
  1777 |     3  
  1352 |     3  
  1491 |     3  
  1064 |     3  
   572 |     3  
   692 |     3  
   301 |     3  
(10 rows)  
  
Time: 3.947 ms  
```

## Design based on HLL and similarity computing of PostgreSQL

The design based on HLL and similarity computing of PostgreSQL stores the IDs of the songs to which each user finishes listening. This design has the following benefits over the conventional design:

-   Stores a small amount of data by using approximate clustered hash values in place of actual values.
-   Supports index-based queries without the need for computing. The index-based queries allow your database system to respond to queries within milliseconds.
-   Supports operations that can be used for sliding window computing to meet more diversified business requirements. These operations include HASH UNION and HASH ADD.

**Note:** For more information about how to use the HLL plug-in, see [Use the hll plug-in](/intl.en-US/AliPG Kernel/Use the hll plug-in.md).

1.  The recommendation system maintains one HLL per tag. The HLL contains a hash value that consists of the IDs of all the songs to which each user finishes listening.

    ```
    create table t_like (    
    uid int,     
    tagid int, -- The ID of the tag.    
    w1 hll, w1_mod_time timestamp, -- The hash value that consists of the IDs of the songs to which the user finishes listening on a Monday within the tag.   
    w2 hll, w2_mod_time timestamp, -- The hash value that consists of the IDs of the songs to which the user finishes listening on a Tuesday within the tag.
    w3 hll, w3_mod_time timestamp, -- The hash value that consists of the IDs of the songs to which the user finishes listening on a Wednesday within the tag.    
    w4 hll, w4_mod_time timestamp, -- The hash value that consists of the IDs of the songs to which the user finishes listening on a Thursday within the tag.    
    w5 hll, w5_mod_time timestamp, -- The hash value that consists of the IDs of the songs to which the user finishes listening on a Friday within the tag.    
    w6 hll, w6_mod_time timestamp, -- The hash value that consists of the IDs of the songs to which the user finishes listening on a Saturday within the tag.    
    w7 hll, w7_mod_time timestamp, -- The hash value that consists of the IDs of the songs to which the user finishes listening on a Sunday within the tag.    
    whole hll,                   -- The hash value that consists of the IDs of the songs to which the user finishes listening from a Monday to Sunday period within the tag.    
    primary key (uid,tagid)    
    );  
    ```

    **Note:** You can specify the w1 to w7 day fields based on your business requirements. For example, if you want to view only the data of a specific day, you can specify only one of the w1 to w7 day fields.

2.  After a user finishes listening to a song, the recommendation system writes the information of the song to the current day field. If the field has a value but the value is not last modified on the current day, the recommendation system overwrites the existing value by using the new value. Otherwise, the recommendation system appends a hash value to the current day field. The hash value consists of both the existing value and the new value. The preceding logic is implemented by using the `INSERT INTO ON CONFLICT` syntax.

    ```
    -- Configure the hash value that consists of the IDs of all the songs to which each user finishes listening within a tag.    
    insert into t_like (    
    uid,    
    tagid,    
    w5,     
    w5_mod_time,    
    whole    
    )    
    values (    
    1,  -- uid    
    200,  -- The ID of the tag.  
    hll_hash_integer(12346)||hll_empty(),  -- The ID of the song to which the user finishes listening. If the user finishes listening to more than one song, the subsequent coding continues.   
    now(),     
    hll_hash_integer(12346)||hll_empty()   -- The ID of the song to which the user finishes listening.    
    )    
    on conflict (uid,tagid)     
    do update    
    set w5=    
    case     
    when date(t_like.w5_mod_time) <> current_date     
    then excluded.w5     
    else hll_union(coalesce(t_like.w5,hll_empty()), excluded.w5)    
    end,    
    w5_mod_time = excluded.w5_mod_time,    
    whole = hll_union(coalesce(t_like.whole,hll_empty()), excluded.whole)    
    where    
    hll_union(coalesce(t_like.w5,hll_empty()), excluded.w5) <> coalesce(t_like.w5,hll_empty())    
    or    
    hll_union(coalesce(t_like.whole,hll_empty()), excluded.whole) <> coalesce(t_like.whole,hll_empty())    
    ;    
    ```

    **Note:** You can perform HLL UNION operations to merge all the data updates to the data records of a user within a tag at a time.

3.  Query the top 10 tags of the user with the uid value being 1 over the last two days. Example:

    ```
    select tagid,     
    hll_cardinality( hll_union(coalesce(w4,hll_empty()), coalesce(w5,hll_empty())) ) as vids     
    from t_like    
    where uid = 1    
    order by 2 desc limit 10;    
        
        
        
     tagid | vids     
    -------+------    
       200 |    2    
    (1 row)    
    ```

4.  Create an index. Example:

    ```
    create index idx_t_like_1 on t_like (uid, hll_cardinality( hll_union(coalesce(w4,hll_empty()), coalesce(w5,hll_empty())) ));
    ```

5.  View the query plan. Example:

    ```
    postgres=# explain select tagid,     
    hll_cardinality( hll_union(coalesce(w4,hll_empty()), coalesce(w5,hll_empty())) ) as vids    
    from t_like    
    where uid = 1    
    order by 2 desc limit 10;    
                                            QUERY PLAN                                             
    -------------------------------------------------------------------------------------------    
     Limit  (cost=0.11..0.15 rows=1 width=12)    
       ->  Index Scan Backward using idx_t_like_1 on t_like  (cost=0.11..0.15 rows=1 width=12)    
             Index Cond: (uid = 1)    
    (3 rows)    
    ```

6.  Write tens of millions of data records and perform a stress test. Example:

    ```
    vi test.sql    
    \set uid random(1,50000)    
    \set tagid random(1,5000)    
    \set vid random(1,10000000)    
    insert into t_like (    
    uid,    
    tagid,    
    w5,     
    w5_mod_time,    
    whole    
    )    
    values (    
    :uid,    
    :tagid,    
    hll_hash_integer(:vid)||hll_empty(),    
    now(),    
    hll_hash_integer(:vid)||hll_empty()    
    )    
    on conflict (uid,tagid)     
    do update    
    set w5=    
    case     
    when date(t_like.w5_mod_time) <> current_date     
    then excluded.w5     
    else hll_union(coalesce(t_like.w5,hll_empty()), excluded.w5)    
    end,    
    w5_mod_time = excluded.w5_mod_time,    
    whole = hll_union(coalesce(t_like.whole,hll_empty()), excluded.whole)    
    where    
    hll_union(coalesce(t_like.w5,hll_empty()), excluded.w5) <> coalesce(t_like.w5,hll_empty())    
    or    
    hll_union(coalesce(t_like.whole,hll_empty()), excluded.whole) <> coalesce(t_like.whole,hll_empty())    
    ;    
        
        
    pgbench -M prepared -n -r -P 1 -c 32 -j 32 -T 120 -f ./test.sql    
    ```

    The following test result is obtained:

    ```
    transaction type: ./test.sql    
    scaling factor: 1    
    query mode: prepared    
    number of clients: 32    
    number of threads: 32    
    duration: 120 s    
    number of transactions actually processed: 24636321    
    latency average = 0.156 ms    
    latency stddev = 0.339 ms    
    tps = 205301.110313 (including connections establishing)    
    tps = 205354.851711 (excluding connections establishing)    
    statement latencies in milliseconds:    
             0.001  \set uid random(1,5000000)    
             0.001  \set tagid random(1,5000)    
             0.000  \set vid random(1,10000000)    
             0.154  insert into t_like (    
    ```

7.  Query the tags of a user based on the tag popularity. Example:

    ```
    postgres=# select tagid,     
    hll_cardinality( hll_union(coalesce(w4,hll_empty()), coalesce(w5,hll_empty())) ) as vids    
    from t_like    
    where uid = 1    
    order by 2 desc limit 10;    
     tagid | vids     
    -------+------    
       200 |    2    
      1413 |    1    
      1996 |    1    
      2642 |    1    
      3664 |    1    
      4340 |    1    
    (6 rows)    
        
    Time: 0.688 ms    
    ```

    **Note:** This query is responded in 0.688 milliseconds.


You can use the preceding design method to implement other business logic in the recommendation system. For example, you can use the following design to filter songs to which a user finishes listening:

-   Determine whether the ID of a song is included in the specified hash value by using fuzzy match. Example:

    ```
    postgres=# select whole || hll_hash_integer(1) = whole        
    from     
    t_like     
    where uid=1 and tagid=200;  -- If the value false is returned, the song with the vid value being 1 is not included.    
     ? column?     
    ----------    
     f    
    (1 row)    
        
    postgres=# select whole || hll_hash_integer(12345) = whole     
    from     
    t_like     
    where uid=1 and tagid=200;   -- If the value true is returned, the song with the vid value being 12345 is included.    
     ? column?     
    ----------    
     t    
    (1 row)    
    ```

-   Determine whether the ID of a song is included in the specified hash value by using exact match. The following example shows how to create a table:

    ```
    create table t_like_lossless (    
    uid int,    
    vid int,    
    primary key (uid,vid)    
    );    
    ```

    **Note:** If you run the query based on a primary key, the query runs fast.


