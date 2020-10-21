# 高速全文检索（RUM）

RDS PostgreSQL提供RUM插件，实现高速全文检索。

GIN索引（通用倒排索引）支持通过tsvector和tsquery两种数据类型进行全文检索，但是有如下几个问题：

-   排序慢

    需要有关词汇的位置信息才能进行排序。GIN索引不存储词汇的位置，因此在索引扫描之后，需要额外的扫描来检索词汇位置。

-   短语查询慢

    GIN索引需要位置信息来执行短语搜索。

-   时间戳排序慢

    GIN索引无法在带有词素的索引中存储一些相关信息，因此需要执行额外的扫描。


基于GIN索引，RDS PostgreSQL提供RUM插件，在RUM索引中存储额外的信息（词汇位置或时间戳的位置信息）来解决以上问题。

RUM索引的缺点是构建和插入时间比GIN索引慢。 这是因为需要存储除密钥之外的其他信息，并且RUM使用通用WAL记录。

## 通用的操作符

RUM模块提供以下操作符。

|操作符|返回值数据类型|描述|
|---|-------|--|
|tsvector <=\> tsquery|float4|返回tsvector与tsquery之间的距离。|
|timestamp <=\> timestamp|float8|返回两个时间戳之间的距离。|
|timestamp <=\| timestamp|float8|只返回左侧时间戳的距离。|
|timestamp \|=\> timestamp|float8|只返回右侧时间戳的距离。|

**说明：** 后三种操作符也适用于这些数据类型：timestamptz、int2、int4、int8、float4、float8、money、oid。

下文将介绍RUM的各个函数。

## rum\_tsvector\_ops

-   适用数据类型：tsvector
-   说明：该函数存储带有位置信息的tsvector词组，支持按`<=>`运算符排序和前缀搜索。
-   示例

    1.  建立一个表格，命令如下：

        ```
        CREATE TABLE test_rum(t text, a tsvector);
        CREATE TRIGGER tsvectorupdate
        BEFORE UPDATE OR INSERT ON test_rum
        FOR EACH ROW EXECUTE PROCEDURE tsvector_update_trigger('a', 'pg_catalog.english', 't');
        INSERT INTO test_rum(t) VALUES ('The situation is most beautiful');
        INSERT INTO test_rum(t) VALUES ('It is a beautiful');
        INSERT INTO test_rum(t) VALUES ('It looks like a beautiful place');
        ```

    2.  创建RUM插件，命令如下：

        ```
        CREATE EXTENSION rum;
        ```

    3.  创建新的索引，命令如下：

        ```
        CREATE INDEX rumidx ON test_rum USING rum (a rum_tsvector_ops);
        ```

    4.  测试执行如下两种查询：
        -   ```
SELECT t, a <=> to_tsquery('english', 'beautiful | place') AS rank
    FROM test_rum
    WHERE a @@ to_tsquery('english', 'beautiful | place')
    ORDER BY a <=> to_tsquery('english', 'beautiful | place');
```

            返回如下输出结果：

            ```
                            t                |  rank
            ---------------------------------+---------
             It looks like a beautiful place | 8.22467
             The situation is most beautiful | 16.4493
             It is a beautiful               | 16.4493
            (3 rows)
            ```

        -   ```
SELECT t, a <=> to_tsquery('english', 'place | situation') AS rank
    FROM test_rum
    WHERE a @@ to_tsquery('english', 'place | situation')
    ORDER BY a <=> to_tsquery('english', 'place | situation');
```

            返回如下输出结果：

            ```
                            t                |  rank
            ---------------------------------+---------
             The situation is most beautiful | 16.4493
             It looks like a beautiful place | 16.4493
            (2 rows)
            ```


## rum\_tsvector\_hash\_ops

-   适用数据类型：tsvector
-   说明：该函数存储tsvector词组的哈希值和位置信息。支持按`<=>`运算符排序， 但不支持前缀搜索。

## rum\_TYPE\_ops

-   适用数据类型：
    -   `<`、`<=`、`=`、`>=`、`>`和`<=>`操作支持int2、int4、int8、float4、float8、money、oid、time、timetz、date、interval、macaddr、inet、cidr、text、varchar、char、bytea、bit、varbit、numeric、timestamp、timestamptz。
    -   `<=|`和`|=>`支持int2、int4、int8、float4、float8、money、oid、timestamp、timestamptz。
-   说明：该函数可以与rum\_tsvector\_addon\_ops、rum\_tsvector\_hash\_addon\_ops和rum\_anyarray\_addon\_ops函数一起使用。

## rum\_tsvector\_addon\_ops

-   适用数据类型：tsvector
-   说明：该函数存储tsvector词法，以及模块字段支持的任何词法。
-   示例

    1.  建立一个表格和索引，命令如下：

        ```
        CREATE TABLE tsts (id int, t tsvector, d timestamp);
        \copy tsts from 'rum/data/tsts.data'
        CREATE INDEX tsts_idx ON tsts USING rum (t rum_tsvector_addon_ops, d)
            WITH (attach = 'd', to = 't');
        ```

    2.  执行如下计划命令：

        ```
        EXPLAIN (costs off)
            SELECT id, d, d <=> '2016-05-16 14:21:25' FROM tsts WHERE t @@ 'wr&qh' ORDER BY d <=> '2016-05-16 14:21:25' LIMIT 5;
        ```

        返回如下输出结果：

        ```
                                            QUERY PLAN
        -----------------------------------------------------------------------------------
         Limit
           ->  Index Scan using tsts_idx on tsts
                 Index Cond: (t @@ '''wr'' & ''qh'''::tsquery)
                 Order By: (d <=> 'Mon May 16 14:21:25 2016'::timestamp without time zone)
        (4 rows)
        ```

    3.  执行如下查询命令：

        ```
        SELECT id, d, d <=> '2016-05-16 14:21:25' FROM tsts WHERE t @@ 'wr&qh' ORDER BY d <=> '2016-05-16 14:21:25' LIMIT 5;
        ```

        返回如下输出结果：

        ```
         id  |                d                |   ?column?
        -----+---------------------------------+---------------
         355 | Mon May 16 14:21:22.326724 2016 |      2.673276
         354 | Mon May 16 13:21:22.326724 2016 |   3602.673276
         371 | Tue May 17 06:21:22.326724 2016 |  57597.326724
         406 | Wed May 18 17:21:22.326724 2016 | 183597.326724
         415 | Thu May 19 02:21:22.326724 2016 | 215997.326724
        (5 rows)
        ```

        **说明：** 当前RUM在使用按引用传递附加信息进行排序来创建索引时可能有缺陷。这是由于后缀树具有固定长度的右边界和固定长度的无子节点后缀项，所以不允许创建此类索引。


## rum\_tsvector\_hash\_addon\_ops

-   适用数据类型：tsvector
-   说明：该函数存储tsvector词库的哈希值以及任何支持模块的字段，不支持前缀搜索。

## rum\_tsquery\_ops

-   适用数据类型：tsquery
-   说明：在其他信息中存储查询树的分支。
-   示例

    1.  建立一个表格和索引，命令如下：

        ```
        CREATE TABLE test_array (i int2[]);
        INSERT INTO test_array VALUES ('{}'), ('{0}'), ('{1,2,3,4}'), ('{1,2,3}'), ('{1,2}'), ('{1}');
        CREATE INDEX idx_array ON test_array USING rum (i rum_anyarray_ops);
        ```

    2.  执行如下计划命令：

        ```
        SET enable_seqscan TO off;
        
        EXPLAIN (COSTS OFF) SELECT * FROM test_array WHERE i && '{1}' ORDER BY i <=> '{1}' ASC;
        ```

        返回如下输出结果：

        ```
                        QUERY PLAN
        ------------------------------------------
         Index Scan using idx_array on test_array
           Index Cond: (i && '{1}'::smallint[])
           Order By: (i <=> '{1}'::smallint[])
        (3 rows)
        ```

    3.  执行如下查询命令：

        ```
        SELECT * FROM test_array WHERE i && '{1}' ORDER BY i <=> '{1}' ASC;
        ```

        返回如下输出结果：

        ```
             i
        -----------
         {1}
         {1,2}
         {1,2,3}
         {1,2,3,4}
        (4 rows)
        ```


## rum\_anyarray\_ops

-   适用数据类型：anyarray
-   说明：该函数存储具有数组长度的anyarrray元素。支持运算符`&&`、`@>`、`<@`、`=`、`％`，支持按`<=>`运算符排序。
-   示例

    1.  建立一个表格和索引，命令如下：

        ```
        CREATE TABLE test_array (i int2[]);
        INSERT INTO test_array VALUES ('{}'), ('{0}'), ('{1,2,3,4}'), ('{1,2,3}'), ('{1,2}'), ('{1}');
        CREATE INDEX idx_array ON test_array USING rum (i rum_anyarray_ops);
        ```

    2.  执行如下计划命令：

        ```
        SET enable_seqscan TO off;
        
        EXPLAIN (COSTS OFF) SELECT * FROM test_array WHERE i && '{1}' ORDER BY i <=> '{1}' ASC;
        ```

        返回如下输出结果：

        ```
                        QUERY PLAN
        ------------------------------------------
         Index Scan using idx_array on test_array
           Index Cond: (i && '{1}'::smallint[])
           Order By: (i <=> '{1}'::smallint[])
        (3 rows)
        ```

    3.  执行如下查询命令：

        ```
        SELECT * FROM test_array WHERE i && '{1}' ORDER BY i <=> '{1}' ASC;
        ```

        返回如下输出结果：

        ```
             i
        -----------
         {1}
         {1,2}
         {1,2,3}
         {1,2,3,4}
        (4 rows)
        ```


## rum\_anyarray\_addon\_ops

-   适用数据类型：anyarray
-   说明：该函数存储anyarrray元素以及模块字段支持的任何元素。

