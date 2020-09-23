# Fuzzy query \(PG\_ bigm\)

The pg\_bigm plug-in that is provided by ApsaraDB RDS for PostgreSQL supports full-text search. It allows you to create a 2-gram Generalized Inverted Index \(GIN\) index that is used to expedite full-text search queries.

Your RDS instance runs one of the following PostgreSQL versions:

-   PostgreSQL 12
-   PostgreSQL 11
-   PostgreSQL 10

## Differences between pg\_bigm and pg\_trgm

The pg\_trgm plug-in is also provided by ApsaraDB RDS for PostgreSQL. However, it uses a 3-gram model to implement full-text search. The pg\_bigm plug-in is developed based on the pg\_trgm plug-in. The following table describes the differences between the two plug-ins.

|Functionality|pg\_trgm|pg\_bigm|
|-------------|--------|--------|
|Phrase matching model|3-gram|2-gram|
|Index types|GIN and GiST|GIN|
|Operators|`LIKE` \| `ILIKE` \| `~` \| `~*`|`LIKE`|
|Non-alphabet full-text search|Not supported|Supported|
|Full-text search with keywords that contain 1 to 2 characters|Slow|Fast|
|Similarity search|Supported|Supported|
|Maximum indexed column length|238,609,291 bytes \(approximately equal to 228 MB\)|107,374,180 bytes \(approximately equal to 102 MB\)|

## Precautions

-   The length of the column on which you create a GIN index cannot exceed 107,374,180 bytes \(approximately equal to 102 MB\).
-   If the data in your RDS instance is not encoded by using ASCII, we recommend that you change the encoding format to UTF8.

    **Note:** To query the encoding format of your RDS instance, run the `select pg_encoding_to_char(encoding) from pg_database where datname = current_database();` command.


## Basic operations

-   Create the pg\_bigm plug-in.

    ```
    postgres=> create extension pg_bigm;
    CREATE EXTENSION
    ```

-   Create a GIN index.

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

-   Run a full-text search query.

    ```
    postgres=> SELECT * FROM pg_tools WHERE description LIKE '%search%';
      tool   |                             description
    ---------+---------------------------------------------------------------------
     pg_bigm | Tool that provides 2-gram full text search capability in PostgreSQL
     pg_trgm | Tool that provides 3-gram full text search capability in PostgreSQL
    (2 rows)
    ```

-   Run a similarity search query by using the `=%` operator.

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

-   Delete the pg\_bigm plug-in.

    ```
    postgres=> drop extension pg_bigm;
    DROP EXTENSION
    ```


## Basic functions

-   likequery
    -   Purpose: This function is used to generate a string that can be identified based on the LIKE keyword.
    -   Request parameters: This function contains one request parameter. The data type for this parameter is STRING.
    -   Return value: This function returns a string that can be identified based on the LIKE keyword.
    -   Implementation:
        -   Add a percent sign \(`%`\) preceding and following the keyword.
        -   Use a backward slash \(`\`\) to escape the percent sign \(`%`\).
    -   Example:

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

-   show\_bigm
    -   Purpose: This function is used to obtain all of the 2-gram elements that comprise a string.
    -   Request parameters: This function contains one request parameter. The data type for this parameter is STRING.
    -   Return value: This parameter returns an array that consists of all the 2-gram elements of a string.
    -   Implementation:
        -   Add a space preceding and following the string.
        -   Identify all of the 2-gram elements in the string.
    -   Example:

        ```
        postgres=> SELECT show_bigm('full text search');
                                    show_bigm
        ------------------------------------------------------------------
         {" f"," s"," t",ar,ch,ea,ex,fu,"h ","l ",ll,rc,se,"t ",te,ul,xt}
        (1 row)
        ```

-   bigm\_similarity
    -   Purpose: This function is used to obtain the similarity between two strings.
    -   Request parameters: This function contains two request parameters. The data types for these parameters are STRING.
    -   Return value: This function returns a floating-point number. The number indicates the similarity between the two strings.
    -   Implementation:

        -   Identify the 2-gram elements that are included in both the two strings.
        -   The return value is within the range from 0 to 1. The value 0 indicates that the two strings are completely different. The value 1 indicates that the two strings are identical.
        **Note:**

        -   This function adds a space preceding and following each string. Therefore, the similarity between the `ABC` string and the `B` string is 0, and the similarity between the `ABC` string and the `A` string is 0.25.
        -   This function supports case sensitivity. For example, it determines that the similarity between the `ABC` string and the `abc` string is 0.
    -   Example:

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

-   pg\_gin\_pending\_stats
    -   Purpose: This function is used to obtain the number of pages and the number of tuples in the pending list of a GIN index.
    -   Request parameters: This function contains one parameter. This parameter specifies the name or OID of the GIN index.
    -   Return value: This function returns two values: the number of pages in the pending list of the GIN index and the number of tuples in the pending list of the GIN index.

        **Note:** If you set the FASTUPDATE parameter to False for a GIN index, the GIN index does not have a pending list. In this case, this function returns two values 0.

    -   Example:

        ```
        postgres=> SELECT * FROM pg_gin_pending_stats('pg_tools_idx');
         pages | tuples
        -------+--------
             0 |      0
        (1 row)
        ```


## Behavior control

-   pg\_bigm.last\_update

    This parameter indicates the last date when the pg\_bigm plug-in was updated. This parameter is read-only. You cannot reconfigure this parameter.

    Example:

    ```
    SHOW pg_bigm.last_update;
    ```

-   pg\_bigm.enable\_recheck

    This parameter specifies whether to perform a recheck.

    **Note:** We recommend that you retain the default value ON. This allows you to obtain accurate query results.

    Example:

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

    This parameter specifies the maximum number of 2-gram elements that can be used for a full-text search query. The default value is 0, which indicates that all 2-gram elements are used.

    **Note:** If the use of all 2-gram elements triggers a performance decrease, you can decrease the value of this parameter.

-   pg\_bigm.similarity\_limit

    This parameter specifies the threshold for similarity. The tuples whose similarity exceeds the specified threshold are returned as similarity search results.


