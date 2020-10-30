# Optimize parameters of an ApsaraDB RDS for MySQL instance

You can modify parameter values of an ApsaraDB RDS for MySQL instance in the ApsaraDB RDS console. Improper values of key parameters may downgrade performance of an RDS instance or cause errors in your application. This topic provides optimization suggestions for key parameters.

## back\_log

-   Applicable MySQL versions: 8.0, 5.7, 5.6, and 5.5.
-   Default value: 3000.
-   Whether to restart the instance after parameter modification: Yes.
-   Function: The primary MySQL thread creates a new thread for each connection request that it processes. If frontend applications initiate a large number of short-lived connections when the primary thread creates a new thread, ApsaraDB RDS for MySQL restricts the short-lived connection requests to enter the queue based on the back\_log parameter. When the number of waiting connection requests in the queue exceeds the value of the back\_log parameter, ApsaraDB RDS for MySQL denies new connection requests. If you want ApsaraDB RDS for MySQL to process a large number of short-lived connections, increase the value of this parameter.
-   Symptom: If the value of this parameter is too small, the application may encounter the following error:

    ```
    SQLSTATE[HY000] [2002] Connection timed out;
    ```

-   Suggestion: Increase the value of this parameter.

## innodb\_autoinc\_lock\_mode

-   Applicable MySQL versions: 8.0, 5.7, 5.6, and 5.5.
-   Default value: 1.
-   Whether to restart the instance after parameter modification: Yes.
-   Function: In MySQL 5.1.22 and later, the innodb\_autoinc\_lock\_mode parameter is used in InnoDB to control auto-increment locks. Valid values: 0, 1, or 2. Default value: 1. The default value indicates that InnoDB uses a lightweight mutex to obtain auto-increment locks, instead of table-level locks. However, the SQL statements that are used to load data \(including the `INSERT ... SELECT` and `REPLACE ... SELECT`\) use auto-increment table locks. If the application initiates a number of SQL statements that are concurrently executed to load data, a deadlock may occur.
-   Symptom: If the SQL statements that are used to load data \(including `INSERT ... SELECT` and `REPLACE ... SELECT`\) use auto-increment table locks, the following deadlock occurs during concurrent data loading:

    ```
    RECORD LOCKS space id xx page no xx n bits xx index PRIMARY of table xx.xx trx id xxx lock_mode X insert intention waiting. TABLE LOCK table xxx.xxx trx id xxxx lock mode AUTO-INC waiting;
    ```

-   Suggestion: Change the value of this parameter to 2. This value indicates that all SQL statements that are used to load data in row mode use a lightweight mutex. This avoids the AUTO-INC deadlock and greatly improves performance of the `INSERT ... SELECT` statement.

    **Note:** If you set the parameter to 2, you must set the format of binary logs to row.


## query\_cache\_size

-   Applicable MySQL versions: 5.7, 5.6, and 5.5.
-   Default value: 3145728.
-   Whether to restart the instance after parameter modification: No.
-   Function: This parameter controls the memory capacity of the MySQL query cache. If you enable the MySQL query cache, the system locks the query cache before it performs a query. Then, the system checks for the query result in the cache. If the query result exists in the query cache, the system directly returns the result. Otherwise, it performs the query to obtain the result. The INSERT, UPDATE, and DELETE operations invalidate the query cache and cause changes in schemas or indexes. Frequent invalidation of the query cache brings heavy pressure on the RDS instance. If data on the RDS instance is not frequently updated, the query cache can greatly improve query efficiency. However, if the database processes a large number of write operations on a few tables, the lock mechanism of the query cache may cause frequent lock conflicts. Both the write and read requests on the locked table wait for the query cache to be unlocked. This reduces query efficiency of SELECT statements.
-   Symptom: A large number of database connections are in the following states: `checking query cache for query`, `waiting for query cache lock`, and `storing result in query cache`.
-   Suggestion: By default, ApsaraDB RDS disables query cache. If you have enabled query cache and encountered the preceding symptom, disable query cache.

## net\_write\_timeout

-   Applicable MySQL versions: 8.0, 5.7, 5.6, and 5.5.
-   Default value: 60.
-   Whether to restart the instance after parameter modification: No.
-   Function: This parameter sets the timeout period that ApsaraDB RDS waits before it sends a block to a client.
-   Symptom: If the parameter value is too small, the client may encounter the following error:

    ```
    "the last packet successfully received from the server was milliseconds ago" or "the last packet sent successfully to the server was milliseconds ago"
    ```

-   Suggestion: The default value of this parameter is 60s. If the value is too small, the client may be frequently disconnected from the RDS instance when the network is not stable or it takes a long time for the client to process each block. We recommend that you increase the value of this parameter.

## tmp\_table\_size

-   Applicable MySQL versions: 8.0, 5.7, 5.6, and 5.5.
-   Default value: 2097152.
-   Whether to restart the instance after parameter modification: No.
-   Function: This parameter determines the maximum size of an internal temporary memory table. The size is assigned to each thread. The actual value is the smaller one between tmp\_table\_size and max\_heap\_table\_size. If the size of the temporary memory table exceeds the limit, ApsaraDB RDS for MySQL automatically converts the table to a disk-based MyISAM table. When you optimize query statements, do not use internal temporary tables. If you have to use a temporary table, make sure that the temporary table is stored in the memory.
-   Symptom: If you use a temporary table for complicated SQL statements that contain GROUP BY or DISTINCT clauses and cannot be optimized by using indexes, SQL execution takes a longer time.
-   Suggestion: If the SQL statements contain a large number of GROUP BY or DISTINCT clauses and the instance has enough memory, increase the values of the tmp\_table\_size and max\_heap\_table\_size parameters to improve query performance.

## loose\_rds\_max\_tmp\_disk\_space

-   Applicable MySQL versions: 5.6 and 5.5.
-   Default value: 10737418240.
-   Whether to restart the instance after parameter modification: No.
-   Function: This parameter controls the size of temporary files on the RDS instance.
-   Symptom: If the size of temporary files exceeds the value of the loose\_rds\_max\_tmp\_disk\_space parameter, the application may encounter the following error:

    ```
    The table '/home/mysql/dataxxx/tmp/#sql_2db3_1' is full
    ```

-   Suggestion: Evaluate whether you can optimize the SQL statements that cause an increase of temporary files by using indexing or other methods. If your instance has enough space, increase the value of this parameter to ensure normal execution of SQL statements.

## loose\_tokudb\_buffer\_pool\_ratio

-   Applicable version: 5.6
-   Default value: 0.
-   Whether to restart the instance after parameter modification: Yes.
-   Function: This parameter specifies the size of buffer memory that can be used by TokuDB tables. For example, if the innodb\_buffer\_pool\_size parameter is set to 1000 MB and the tokudb\_buffer\_pool\_ratio parameter to 50 \(indicating 50%\), the size of buffer memory that can be used by TokuDB tables is 500 MB.
-   Suggestion: If the TokuDB engine is used on the RDS instance, increase the value of this parameter to improve access performance of TokuDB tables.

## loose\_max\_statement\_time

-   Applicable MySQL version: 5.6
-   Default value: 0.
-   Whether to restart the instance after parameter modification: No.
-   Function: This parameter sets a limit on how long a query can take before it times out. By default, the query time is not limited. If this parameter is configured and the query time exceeds the specified limit, the query fails.
-   Symptom: If the query time exceeds the value of this parameter, the following error occurs:

    ```
    ERROR 3006 (HY000): Query execution was interrupted, max_statement_time exceeded
    ```

-   Suggestion: If you want to limit the time to execute SQL statements, set this parameter to a non-zero value. Unit: milliseconds.

## loose\_rds\_threads\_running\_high\_watermark

-   Applicable MySQL versions: 5.6 and 5.5.
-   Default value: 50000.
-   Whether to restart the instance after parameter modification: No.
-   Function: This parameter limits the number of concurrent queries. For example, if you set the rds\_threads\_running\_high\_watermark parameter to 100, 100 MySQL queries can be concurrently executed. Additional queries are denied.
-   Suggestion: This parameter is used to handle burst requests and requests during peak hours to protect the RDS instance.

