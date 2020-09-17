# 文本搜索与模糊查询（pg\_bigm）

pg\_bigm是阿里云产品RDS Postgresql的一款插件，该插件提供了全文本搜索能力，允许创建一个二元语法（2-gram）的GIN索引来加速搜索过程。

RDS PostgreSQL实例需为以下版本之一：

-   PostgreSQL 12
-   PostgreSQL 11
-   PostgreSQL 10

## 与pg\_trgm异同

pg\_trgm是RDS Postgresql的另一款插件，使用3-gram的模型来实现全文本搜索。pg\_bigm插件是在pg\_trgm基础上继续开发的，两者的区别如下。

|功能和特性|pg\_trgm|pg\_bigm|
|-----|--------|--------|
|全文搜索的短语匹配方法|3-gram|2-gram|
|支持的索引类型|GIN和GIST|GIN|
|支持的全文本搜索操作符号|`LIKE`、`ILIKE`、`~`、`~*`|`LIKE`|
|非字母语言的全文本搜索|不支持|支持|
|带有1~2个字符的关键字的全文本搜索|慢|快|
|相似性搜索|支持|支持|
|最大可以索引的列大小|238,609,291字节（约228 MB）|107,374,180字节（约102 MB）|

## 注意事项

-   建立GIN索引的列的长度不可以超过107,374,180字节（约102 MB）。
-   如果数据库中存储的内容语言是非ASCII，则建议将数据库的编码方式改为UTF8。

    **说明：** 查询当前数据库的编码方式命令为`select pg_encoding_to_char(encoding) from pg_database where datname = current_database();`。


## 基本操作

-   创建插件

    ```
    postgres=> create extension pg_bigm;
    CREATE EXTENSION
    ```

-   创建索引

    ```
    postgres=> CREATE TABLE pg_tools (tool text, description text);
    CREATE TABLE
    postgres=> INSERT INTO pg_tools VALUES ('pg_hint_plan', 'Tool that allows a user to specify an optimizer HINT to PostgreSQL');
    INSERT 0 1
    postgres=> INSERT INTO pg_tools VALUES ('pg_dbms_stats', 'Tool that allows a user to stabilize planner statistics in PostgreSQL');
    INSERT 0 1
    postgres=> INSERT INTO pg_tools VALUES ('pg_bigm', 'Tool that provides 2-gram full text search capability in PostgreSQL');
    INSERT 0 1
    postgres=> INSERT INTO pg_tools VALUES ('pg_trgm', 'Tool that provides 3-gram full text search capability in PostgreSQL');
    INSERT 0 1
    postgres=> CREATE INDEX pg_tools_idx ON pg_tools USING gin (description gin_bigm_ops);
    CREATE INDEX
    postgres=> CREATE INDEX pg_tools_multi_idx ON pg_tools USING gin (tool gin_bigm_ops, description gin_bigm_ops) WITH (FASTUPDATE = off);
    CREATE INDEX
    ```

-   执行全文本搜索

    ```
    postgres=> SELECT * FROM pg_tools WHERE description LIKE '%search%';
      tool   |                             description
    ---------+---------------------------------------------------------------------
     pg_bigm | Tool that provides 2-gram full text search capability in PostgreSQL
     pg_trgm | Tool that provides 3-gram full text search capability in PostgreSQL
    (2 rows)
    ```

-   使用`=%`操作符执行相似性搜索

    ```
    postgres=> SET pg_bigm.similarity_limit TO 0.2;
    SET
    postgres=> SELECT tool FROM pg_tools WHERE tool =% 'bigm';
      tool
    ---------
     pg_bigm
     pg_trgm
    (2 rows)
    ```

-   卸载插件

    ```
    postgres=> drop extension pg_bigm;
    DROP EXTENSION
    ```


## 插件常用函数

-   likequery函数
    -   作用：生成可以被LIKE关键字识别的字符串。
    -   参数：1个请求参数，类型为字符串。
    -   返回值：可以被LIKE关键字识别的搜索字符串。
    -   实现原理：
        -   在关键词前后添加`%`符号。
        -   使用`\`来自动转义符号`%`。
    -   示例如下：

        ```
        postgres=> SELECT likequery('pg_bigm has improved the full text search performance by 200%');
                                     likequery
        -------------------------------------------------------------------
         %pg\_bigm has improved the full text search performance by 200\%%
        (1 row)
        
        postgres=> SELECT * FROM pg_tools WHERE description LIKE likequery('search');
          tool   |                             description
        ---------+---------------------------------------------------------------------
         pg_bigm | Tool that provides 2-gram full text search capability in PostgreSQL
         pg_trgm | Tool that provides 3-gram full text search capability in PostgreSQL
        (2 rows)
        ```

-   show\_bigm函数
    -   作用：返回给定字符串的所有2-gram元素的集合。
    -   参数：1个请求参数，类型为字符串。
    -   返回值：数组，包含所有的2-gram元素。
    -   实现原理：
        -   在字符串前后添加空格字符。
        -   计算所有的2-gram子串。
    -   示例如下：

        ```
        postgres=> SELECT show_bigm('full text search');
                                    show_bigm
        ------------------------------------------------------------------
         {" f"," s"," t",ar,ch,ea,ex,fu,"h ","l ",ll,rc,se,"t ",te,ul,xt}
        (1 row)
        ```

-   bigm\_similarity函数
    -   作用：计算两个字符串的相似度。
    -   参数：2个请求参数，类型为字符串。
    -   返回值：浮点数，表示相似度。
    -   实现原理：

        -   统计两个字符串共有的2-gram元素。
        -   相似度范围是\[0, 1\]，0代表两个字符串完全不一样，1代表两个字符串一样。
        **说明：**

        -   由于计算2-gram时，会在字符串前后添加空格，于是`ABC`和`B`的相似度为0，`ABC`和`A`的相似度为0.25。
        -   bigm\_similarity函数是大小写不敏感的，例如`ABC`和`abc`的相似度为0。
    -   示例如下：

        ```
        postgres=> SELECT bigm_similarity('full text search', 'text similarity search');
         bigm_similarity
        -----------------
               0.5714286
        (1 row)
        
        postgres=> SELECT bigm_similarity('ABC', 'A');
         bigm_similarity
        -----------------
                    0.25
        (1 row)
        
        postgres=> SELECT bigm_similarity('ABC', 'B');
         bigm_similarity
        -----------------
                       0
        (1 row)
        
        postgres=> SELECT bigm_similarity('ABC', 'abc');
         bigm_similarity
        -----------------
                       0
        (1 row)
        ```

-   pg\_gin\_pending\_stats函数
    -   作用：返回GIN索引的pending list中页面和元组的个数。
    -   参数：1个，GIN索引的名字或者OID。
    -   返回值：2个，pending list中页面的数量和元组的数量。

        **说明：** 如果GIN索引创建时，指定参数FASTUPDATE为False，则该GIN索引不存在pending list，即返回结果为0。

    -   示例如下：

        ```
        postgres=> SELECT * FROM pg_gin_pending_stats('pg_tools_idx');
         pages | tuples
        -------+--------
             0 |      0
        (1 row)
        ```


## 插件行为控制

-   pg\_bigm.last\_update

    该插件的最后更新日期，只读参数，无法修改。

    示例如下：

    ```
    SHOW pg_bigm.last_update;
    ```

-   pg\_bigm.enable\_recheck

    决定是否进行recheck。

    **说明：** 建议您保持默认值（ON）以保证结果正确性。

    示例如下：

    ```
    postgres=> CREATE TABLE tbl (doc text);
    CREATE TABLE
    postgres=> INSERT INTO tbl VALUES('He is awaiting trial');
    INSERT 0 1
    postgres=> INSERT INTO tbl VALUES('It was a trivial mistake');
    INSERT 0 1
    postgres=> CREATE INDEX tbl_idx ON tbl USING gin (doc gin_bigm_ops);
    CREATE INDEX
    postgres=> SET enable_seqscan TO off;
    SET
    postgres=> EXPLAIN ANALYZE SELECT * FROM tbl WHERE doc LIKE likequery('trial');
                                                       QUERY PLAN
    -----------------------------------------------------------------------------------------------------------------
     Bitmap Heap Scan on tbl  (cost=20.00..24.01 rows=1 width=32) (actual time=0.020..0.021 rows=1 loops=1)
       Recheck Cond: (doc ~~ '%trial%'::text)
       Rows Removed by Index Recheck: 1
       Heap Blocks: exact=1
       ->  Bitmap Index Scan on tbl_idx  (cost=0.00..20.00 rows=1 width=0) (actual time=0.013..0.013 rows=2 loops=1)
             Index Cond: (doc ~~ '%trial%'::text)
     Planning Time: 0.117 ms
     Execution Time: 0.043 ms
    (8 rows)
    
    postgres=>
    postgres=> SELECT * FROM tbl WHERE doc LIKE likequery('trial');
             doc
    ----------------------
     He is awaiting trial
    (1 row)
    
    postgres=> SET pg_bigm.enable_recheck = off;
    SET
    postgres=> SELECT * FROM tbl WHERE doc LIKE likequery('trial');
               doc
    --------------------------
     He is awaiting trial
     It was a trivial mistake
    (2 rows)
    ```

-   pg\_bigm.gin\_key\_limit

    限制用于全文本搜索的2-gram元素的最大个数，默认为0，0代表使用所有的2-gram元素。

    **说明：** 如果发现使用所有的2-gram元素导致性能下降，可以调整该参数值，限制2-gram元素的个数来提高性能。

-   pg\_bigm.similarity\_limit

    设置相似度阈值，相似度超过这个阈值的元组会做为相似性搜索的结果。


