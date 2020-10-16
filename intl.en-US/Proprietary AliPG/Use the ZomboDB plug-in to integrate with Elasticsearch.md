# Use the ZomboDB plug-in to integrate with Elasticsearch

ZomboDB is a PostgreSQL extension plug-in. It supports the access methods that are provided by native PostgreSQL. It also provides powerful text search and analytics features by using Elasticsearch.

Your ApsaraDB for RDS instance runs PostgreSQL 11.

ZomboDB provides a full set of query languages to query relational data. You can also create ZomboDB indexes. In this case, ZomboDB takes over remote Elasticsearch indexes and ensures transactionally correct query results from text search.

ZomboDB allows you to use Elasticsearch without the need to handle synchronization or communication issues.

## Create and delete the ZomboDB plug-in

-   Create the plug-in

    ```
    CREATE EXTENSION zombodb;
    ```

-   Delete the plug-in

    ```
    DROP EXTENSION zombodb;
    ```


## Examples

1.  Create a table.

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

2.  Create a ZomboDB index for the table.

    ```
    CREATE INDEX idxproducts
              ON products
           USING zombodb ((products. *))
            WITH (url='localhost:9200/');
    ```

    **Note:** The WITH clause is followed by an Elasticsearch endpoint, which points to a running Elasticsearch cluster.

3.  Query data by using the ZomboDB index.

    ```
    SELECT *
      FROM products
     WHERE products ==> '(keywords:(sports OR box) OR long_description:"wooden away"~5) AND price:[1000 TO 20000]';
    ```

    **Note:** For more information about the query syntax, see [ZomboDB Documentation](https://www.zombodb.com/documentation/).


