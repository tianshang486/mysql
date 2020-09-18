# Performance Insight

This topic describes how to use the Performance Insight function for load monitoring, association analysis, and optimizing performance. This function helps you quickly evaluate the loads of your ApsaraDB for RDS instance and locate performance problems to ensure database stability.

-   Your RDS instance runs one of the following database engine versions:
    -   MySQL 8.0
    -   MySQL 5.7
-   The kernel version of your RDS instance is 20190915 or later.

    **Note:** Log on to the ApsaraDB for RDS console, find the target RDS instance, and navigate to the Basic Information page. Then in the **Configuration Information** section, check whether the **Upgrade Kernel Version** button is available. If the button is available, click it to view the kernel version of your RDS instance. If the button is not available, you are already using the latest kernel version. For more information, see [Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance.md).

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6040359951/p61646.png)


## Overview

The Performance Insight function consists of the following two parts:

-   Object Statistics

    Object Statistics queries statistics from indexes and the following two tables:

    -   TABLE\_STATISTICS: records rows with read and modified data.
    -   INDEX\_STATISTICS: records rows with data read from indexes.
-   Performance Point

    Performance Point collects performance details of your RDS instance. Using these details, you can quantify the overheads of SQL statements faster and more accurately. Performance Point measures database performance using the following three dimensions:

    -   CPU: includes but is not limited to the total time spent executing an SQL statement and the time spent by CPU executing an SQL statement.
    -   Lock: includes the time occupied by locks such as metadata locks on the server, storage transaction locks, mutual exclusions \(mutexes\) \(in debugging mode only\), and readers-writer locks.
    -   I/O: includes the time taken to perform operations such as reading and writing data files, writing log files, reading binary logs, reading redo logs, and asynchronously reading redo logs.

## Use Object Statistics

1.  Check that the values of the OPT\_TABLESTAT and OPT\_INDEXSTAT parameters are ON. Example:

    ```
    mysql> show variables like "opt_%_stat";
      +---------------+-------+
      | Variable_name | Value |
      +---------------+-------+
      | opt_indexstat | ON    |
      | opt_tablestat | ON    |
      +---------------+-------+
    ```

    **Note:** If these parameters cannot be found or their values are not ON, check that your RDS instance is running MySQL 5.7.

2.  Query the TABLE\_STATISTICS or INDEX\_STATISTICS table in the information\_schema database to obtain table or index statistics. Examples:

    ```
    mysql> select * from TABLE_STATISTICS limit 10;
      +--------------+--------------+-----------+--------------+------------------------+---------------+--------------+--------------+
      | TABLE_SCHEMA | TABLE_NAME   | ROWS_READ | ROWS_CHANGED | ROWS_CHANGED_X_INDEXES | ROWS_INSERTED | ROWS_DELETED | ROWS_UPDATED |
      +--------------+--------------+-----------+--------------+------------------------+---------------+--------------+--------------+
      | mysql        | db           |         2 |            0 |                      0 |             0 |            0 |            0 |
      | mysql        | engine_cost  |         2 |            0 |                      0 |             0 |            0 |            0 |
      | mysql        | proxies_priv |         1 |            0 |                      0 |             0 |            0 |            0 |
      | mysql        | server_cost  |         6 |            0 |                      0 |             0 |            0 |            0 |
      | mysql        | tables_priv  |         2 |            0 |                      0 |             0 |            0 |            0 |
      | mysql        | user         |         7 |            0 |                      0 |             0 |            0 |            0 |
      | test         | sbtest1      |      1686 |          142 |                    184 |           112 |           12 |           18 |
      | test         | sbtest10     |      1806 |          125 |                    150 |           105 |            5 |           15 |
      | test         | sbtest100    |      1623 |          141 |                    182 |           110 |           10 |           21 |
      | test         | sbtest11     |      1254 |          136 |                    172 |           110 |           10 |           16 |
      +--------------+--------------+-----------+--------------+------------------------+---------------+--------------+--------------+
    
      mysql> select * from INDEX_STATISTICS limit 10;
      +--------------+--------------+------------+-----------+
      | TABLE_SCHEMA | TABLE_NAME   | INDEX_NAME | ROWS_READ |
      +--------------+--------------+------------+-----------+
      | mysql        | db           | PRIMARY    |         2 |
      | mysql        | engine_cost  | PRIMARY    |         2 |
      | mysql        | proxies_priv | PRIMARY    |         1 |
      | mysql        | server_cost  | PRIMARY    |         6 |
      | mysql        | tables_priv  | PRIMARY    |         2 |
      | mysql        | user         | PRIMARY    |         7 |
      | test         | sbtest1      | PRIMARY    |      2500 |
      | test         | sbtest10     | PRIMARY    |      3007 |
      | test         | sbtest100    | PRIMARY    |      2642 |
      | test         | sbtest11     | PRIMARY    |      2091 |
      +--------------+--------------+------------+-----------+
    ```

    The following table describes parameters of the responses to the sample query requests.

    |Parameter|Description|
    |---------|-----------|
    |TABLE\_SCHEMA|The name of a database.|
    |TABLE\_NAME|The name of a table.|
    |ROWS\_READ|The number of rows read from a table.|
    |ROWS\_CHANGED|The number of rows modified in a table.|
    |ROWS\_CHANGED\_X\_INDEXES|The number of rows modified by using indexes in a table.|
    |ROWS\_INSERTED|The number of rows inserted into a table.|
    |ROWS\_DELETED|The number of rows deleted from a table.|
    |ROWS\_UPDATED|The number of rows updated in a table.|
    |INDEX\_NAME|The name of an index.|


## Use Performance Point

1.  View the global variable settings of your RDS instance, as shown in the following example:

    ```
    mysql> show variables like "%performance_point%";
      +---------------------------------------+-------+
      | Variable_name                         | Value |
      +---------------------------------------+-------+
      | performance_point_dbug_enabled        | OFF   |
      | performance_point_enabled             | ON    |
      | performance_point_iostat_interval     | 2     |
      | performance_point_iostat_volume_size  | 10000 |
      | performance_point_lock_rwlock_enabled | ON    |
      +---------------------------------------+-------+
    ```

    **Note:** If these variables cannot be found, check that your RDS instance is running MySQL 5.7.

2.  Query the events\_statements\_summary\_by\_digest\_supplement table in the performance\_schema database to obtain the top 10 SQL statements in various dimensions. Example:

    ```
    mysql> select * from events_statements_summary_by_digest_supplement limit 10;
      +--------------------+----------------------------------+-------------------------------------------+--------------+
      | SCHEMA_NAME        | DIGEST                           | DIGEST_TEXT                               | ELAPSED_TIME | ......
      +--------------------+----------------------------------+-------------------------------------------+--------------+
      | NULL               | 6b787dd1f9c6f6c5033120760a1a82de | SELECT @@`version_comment` LIMIT ?        |          932 |
      | NULL               | 2fb4341654df6995113d998c52e5abc9 | SHOW SCHEMAS                              |         2363 |
      | NULL               | 8a93e76a7846384621567fb4daa1bf95 | SHOW VARIABLES LIKE ?                     |        17933 |
      | NULL               | dd148234ac7a20cb5aee7720fb44b7ea | SELECT SCHEMA ( )                         |         1006 |
      | information_schema | 2fb4341654df6995113d998c52e5abc9 | SHOW SCHEMAS                              |         2156 |
      | information_schema | 74af182f3a2bd265678d3dadb53e08da | SHOW TABLES                               |         3161 |
      | information_schema | d3a66515192fcb100aaef6f8b6e45603 | SELECT * FROM `TABLE_STATISTICS` LIMIT ?  |         2081 |
      | information_schema | b3726b7c4c4db4b309de2dbc45ff52af | SELECT * FROM `INDEX_STATISTICS` LIMIT ?  |         2384 |
      | information_schema | dd148234ac7a20cb5aee7720fb44b7ea | SELECT SCHEMA ( )                         |          129 |
      | test               | 2fb4341654df6995113d998c52e5abc9 | SHOW SCHEMAS                              |          342 |
      +--------------------+----------------------------------+-------------------------------------------+--------------+
    ```

    The following table describes parameters of the response to the sample query request.

    |Parameter|Description|
    |---------|-----------|
    |SCHEMA\_NAME|The name of a database.|
    |DIGEST|The 64-byte hash string obtained from the **DIGEST\_TEXT** parameter.|
    |DIGEST\_TEXT|The digest of an SQL statement.|
    |ELAPSED\_TIME|The total time spent executing an SQL statement. Unit: μs.|
    |CPU\_TIME|The time spent by CPU executing an SQL statement. Unit: μs.|
    |SERVER\_LOCK\_TIME|The time occupied by metadata locks on the server during the execution of an SQL statement. Unit: μs.|
    |TRANSACTION\_LOCK\_TIME|The time occupied by storage transaction locks during the execution of an SQL statement. Unit: μs.|
    |MUTEX\_SPINS|The number of mutex spins triggered during the execution of an SQL statement.|
    |MUTEX\_WAITS|The number of spin waits triggered by mutexes during the execution of an SQL statement.|
    |RWLOCK\_SPIN\_WAITS|The number of spin waits triggered by readers-write locks during the execution of an SQL statement.|
    |RWLOCK\_SPIN\_ROUNDS|The number of rounds in which the background thread looped in the spin-wait cycles triggered by readers-write locks during the execution of an SQL statement.|
    |RWLOCK\_OS\_WAITS|The number of operating system waits triggered by readers-write locks during the execution of an SQL statement.|
    |DATA\_READS|The number of times the system read data from data files during the execution of an SQL statement.|
    |DATA\_READ\_TIME|The time spent reading data from data files during the execution of an SQL statement. Unit: μs.|
    |DATA\_WRITES|The number of times the system wrote data into data files during the execution of an SQL statement.|
    |DATA\_WRITE\_TIME|The time spent writing data into data files during the execution of an SQL statement. Unit: μs.|
    |REDO\_WRITES|The number of times the system wrote data into log files during the execution of an SQL statement.|
    |REDO\_WRITE\_TIME|The time spent writing data into log files during the execution of an SQL statement. Unit: μs.|
    |LOGICAL\_READS|The number of times the system read logical pages during the execution of an SQL statement.|
    |PHYSICAL\_READS|The number of times the system read physical pages during the execution of an SQL statement.|
    |PHYSICAL\_ASYNC\_READS|The number of times system read physical asynchronous pages during the execution of an SQL statement.|

3.  Query the IO\_STATISTICS table in the information\_schema database to obtain information about recent data read and write operations: Example:

    ```
    mysql> select * from IO_STATISTICS limit 10;
      +---------------------+-----------+----------------+
      | TIME                | DATA_READ | DATA_READ_TIME | ......
      +---------------------+-----------+----------------+
      | 2019-08-08 09:56:53 |        73 |            983 |
      | 2019-08-08 09:56:57 |         0 |              0 |
      | 2019-08-08 09:59:17 |         0 |              0 |
      | 2019-08-08 10:00:55 |      4072 |          40628 |
      | 2019-08-08 10:00:59 |         0 |              0 |
      | 2019-08-08 10:01:09 |       562 |           5800 |
      | 2019-08-08 10:01:11 |       606 |           6910 |
      | 2019-08-08 10:01:13 |       609 |           6875 |
      | 2019-08-08 10:01:15 |       625 |           7077 |
      | 2019-08-08 10:01:17 |       616 |           5800 |
      +---------------------+-----------+----------------+
    ```

    The following table describes parameters of the response to the query request.

    |Parameter|Description|
    |---------|-----------|
    |TIME|The point in time at which data read and write operations were performed.|
    |DATA\_READ|The number of times the system read data.|
    |DATA\_READ\_TIME|The total time spent reading data. Unit: μs.|
    |DATA\_READ\_MAX\_TIME|The maximum time spent reading data. Unit: μs.|
    |DATA\_READ\_BYTES|The total amount of data read. Unit: bytes.|
    |DATA\_WRITE|The number of times the system wrote data.|
    |DATA\_WRITE\_TIME|The total time spent writing data. Unit: μs.|
    |DATA\_WRITE\_MAX\_TIME|The maximum time spent writing data. Unit: μs.|
    |DATA\_WRITE\_BYTES|The total amount of data written. Unit: bytes.|


