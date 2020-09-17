# Elasticsearch索引接口（ZomboDB）

ZomboDB是一个PostgreSQL扩展插件，支持原生的访问方式，为PostgreSQL数据库带来了强大的文本索引和分析功能。

RDS PostgreSQL实例版本为PostgreSQL 11。

ZomboDB提供了一套全方位的查询语言，可以供您自由地查询关系型数据。此外，ZomboDB允许您创建ZomboDB类型的索引，此时ZomboDB完全接管远程的Elasticsearch，并负责文本搜索的事务正确性。

ZomboDB的优势在于允许您直接使用Elasticsearch的强大功能而不用处理同步、通信等问题。

## 插件的创建与删除

-   创建插件

    ```
    CREATE EXTENSION zombodb;
    ```

-   删除插件

    ```
    DROP EXTENSION zombodb;
    ```


## 示例

1.  创建一个表。

    ```
    CREATE TABLE products (
        id SERIAL8 NOT NULL PRIMARY KEY,
        name text NOT NULL,
        keywords varchar(64)[],
        short_summary text,
        long_description zdb.fulltext,
        price bigint,
        inventory_count integer,
        discontinued boolean default false,
        availability_date date
    );
    ```

2.  为表添加ZomboDB类型的索引。

    ```
    CREATE INDEX idxproducts
              ON products
           USING zombodb ((products.*))
            WITH (url='localhost:9200/');
    ```

    **说明：** WITH语句后跟随了Elasticsearch的地址，该地址指向了一个正在服务的Elasticsearch实例。

3.  使用ZomboDB格式的查询语句进行查询。

    ```
    SELECT *
      FROM products
     WHERE products ==> '(keywords:(sports OR box) OR long_description:"wooden away"~5) AND price:[1000 TO 20000]';
    ```

    **说明：** ZomboDB格式的查询语句详细规则请参见[ZomboDB官方文档](https://www.zombodb.com/documentation/)。


