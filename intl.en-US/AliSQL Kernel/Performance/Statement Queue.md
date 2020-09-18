# Statement Queue

The Statement Queue feature of AliSQL allows statements to queue in the same bucket. These statements may be executed on the same resources. For example, these statements are executed on the same row of a table. This reduces overheads from possible conflicts.

During the execution of concurrent statements, the MySQL server and engine are likely to conflict with each other in a number of serial operations. Take transactional lock conflicts triggered by data manipulation language \(DML\) statements as an example. The InnoDB storage engine supports resource locking accurate to rows. If you execute a number of DML statements concurrently on a row, serious conflicts may occur. The overall throughput of your database system decreases in proportion with the number of concurrent statements. The Statement Queue feature reduces overheads from these conflicts and increases the performance of your database system.

## Prerequisites

The RDS instance version is one of the following:

-   MySQL 8.0
-   MySQL 5.7

## Benefits

AliSQL executes UPDATE statements concurrently on a single row four times faster than native MySQL.

## Variables

AliSQL provides two variables that are used to define the bucket quantity and size of a statement queue:

-   ccl\_queue\_bucket\_count: the number of buckets allowed in the statement queue. Valid values: 1 to 64. Default value: 4.
-   ccl\_queue\_bucket\_size: the number of concurrent statements allowed per bucket. Valid values: 1 to 4096. Default value: 64.

**Note:** You can reconfigure the variables in the ApsaraDB for RDS console. For more information, see [Reconfigure the parameters of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance parameters/Reconfigure the parameters of an ApsaraDB RDS for MySQL instance.md).

## Syntaxes

AliSQL supports two hint syntaxes:

-   ccl\_queue\_value

    AliSQL uses a hash algorithm to determine the bucket into which each statement is placed based on the value of a specified field.

    Syntax:

    ```
    /*+ ccl_queue_value([int | string)] */
    ```

    Example:

    ```
    update /*+ ccl_queue_value(1) */ t set c=c+1 where id = 1;
    
    update /*+ ccl_queue_value('xpchild') */ t set c=c+1 where name = 'xpchild';
    ```

-   ccl\_queue\_field

    AliSQL uses a hash algorithm to determine the bucket into which each statement is placed based on the value of the field that is specified in the WHERE clause.

    Syntax:

    ```
    /*+ ccl_queue_field(string) */
    ```

    Example:

    ```
    update /*+ ccl_queue_field("id") */ t set c=c+1 where id = 1 and name = 'xpchild';
    ```

    **Note:** In the ccl\_queue\_field hint, the WHERE clause only supports binary operators on raw fields. These raw fields have not been altered by using functions or computation operations. In addition, the right operand of such a binary operator must be a number or string.


## Functions

AliSQL provides two functions that are used to query the status of a statement queue:

-   dbms\_ccl.show\_ccl\_queue\(\)

    This function is used to query the status of the current statement queue.

    ```
    mysql> call dbms_ccl.show_ccl_queue();   
    +------+-------+-------------------+---------+---------+----------+
    | ID   | TYPE  | CONCURRENCY_COUNT | MATCHED | RUNNING | WAITTING |
    +------+-------+-------------------+---------+---------+----------+
    |    1 | QUEUE |                64 |       1 |       0 |        0 |
    |    2 | QUEUE |                64 |   40744 |      65 |        6 |
    |    3 | QUEUE |                64 |       0 |       0 |        0 |
    |    4 | QUEUE |                64 |       0 |       0 |        0 |
    +------+-------+-------------------+---------+---------+----------+
    4 rows in set (0.01 sec)
    ```

    The following table describes the parameters in this function.

    |Parameter|Description|
    |---------|-----------|
    |CONCURRENCY\_COUNT|The maximum number of concurrent queries allowed.|
    |MATCHED|The total number of rules matched.|
    |RUNNING|The number of statements that are being executed concurrently.|
    |WAITTING|The number of statements that are waiting in queue.|

-   dbms\_ccl.flush\_ccl\_queue\(\)

    This function is used to delete data about the statement queue from the memory and query the status of the statement queue.

    ```
    mysql> call dbms_ccl.flush_ccl_queue();                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       Query OK, 0 rows affected (0.00 sec)
    
    mysql> call dbms_ccl.show_ccl_queue();
    +------+-------+-------------------+---------+---------+----------+
    | ID   | TYPE  | CONCURRENCY_COUNT | MATCHED | RUNNING | WAITTING |
    +------+-------+-------------------+---------+---------+----------+
    |    1 | QUEUE |                64 |       0 |       0 |        0 |
    |    2 | QUEUE |                64 |       0 |       0 |        0 |
    |    3 | QUEUE |                64 |       0 |       0 |        0 |
    |    4 | QUEUE |                64 |       0 |       0 |        0 |
    +------+-------+-------------------+---------+---------+----------+
    4 rows in set (0.00 sec)
    ```


## Practices

Statement Queue can work with [Statement outline](/intl.en-US/AliSQL Kernel/Feature/Statement outline.md) to support online updates of your application code. In the following example, SysBench is used to execute the update\_non\_index.lua script:

-   Test environment
    -   Schema

        ```
        CREATE TABLE `sbtest1` (
          `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
          `k` int(10) unsigned NOT NULL DEFAULT '0',
          `c` char(120) NOT NULL DEFAULT '',
          `pad` char(60) NOT NULL DEFAULT '',
          PRIMARY KEY (`id`),
          KEY `k_1` (`k`)
        ) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8 MAX_ROWS=1000000;
        ```

    -   Statement

        ```
        UPDATE sbtest1 SET c='xpchild' WHERE id=0;
        ```

    -   Script

        ```
        ./sysbench 
        --mysql-host= {$ip}
        --mysql-port= {$port}
        --mysql-db=test 
        --test=./sysbench/share/sysbench/update_non_index.lua 
        --oltp-tables-count=1 
        --oltp_table_size=1 
        --num-threads=128
        --mysql-user=u0
        ```

-   Procedure
    1.  Create a statement outline in online mode.

        ```
        mysql> CALL DBMS_OUTLN.add_optimizer_outline('test', '', 1, 
                                                     ' /*+ ccl_queue_field("id") */ ',
                                 "UPDATE sbtest1 SET c='xpchild' WHERE id=0");
        Query OK, 0 rows affected (0.01 sec)
        ```

    2.  View the statement outline that you created.

        ```
        mysql> call dbms_outln.show_outline();
        +------+--------+------------------------------------------------------------------+-----------+-------+------+--------------------------------+------+----------+---------------------------------------------+
        | ID   | SCHEMA | DIGEST                                                           | TYPE      | SCOPE | POS  | HINT                           | HIT  | OVERFLOW | DIGEST_TEXT                                 |
        +------+--------+------------------------------------------------------------------+-----------+-------+------+--------------------------------+------+----------+---------------------------------------------+
        |    1 | test   | 7b945614749e541e0600753367884acff5df7e7ee2f5fb0af5ea58897910f023 | OPTIMIZER |       |    1 |  /*+ ccl_queue_field("id") */  |    0 |        0 | UPDATE `sbtest1` SET `c` = ? WHERE `id` = ? |
        +------+--------+------------------------------------------------------------------+-----------+-------+------+--------------------------------+------+----------+---------------------------------------------+
        1 row in set (0.00 sec)
        ```

    3.  Verify that the statement outline has taken effect.

        ```
        mysql> explain UPDATE sbtest1 SET c='xpchild' WHERE id=0;
        +----+-------------+---------+------------+-------+---------------+---------+---------+-------+------+----------+-------------+
        | id | select_type | table   | partitions | type  | possible_keys | key     | key_len | ref   | rows | filtered | Extra       |
        +----+-------------+---------+------------+-------+---------------+---------+---------+-------+------+----------+-------------+
        |  1 | UPDATE      | sbtest1 | NULL       | range | PRIMARY       | PRIMARY | 4       | const |    1 |   100.00 | Using where |
        +----+-------------+---------+------------+-------+---------------+---------+---------+-------+------+----------+-------------+
        1 row in set, 1 warning (0.00 sec)
        
        mysql> show warnings;
        +-------+------+-----------------------------------------------------------------------------------------------------------------------------+
        | Level | Code | Message                                                                                                                     |
        +-------+------+-----------------------------------------------------------------------------------------------------------------------------+
        | Note  | 1003 | update /*+ CCL_QUEUE_FIELD('id') */ `test`.`sbtest1` set `test`.`sbtest1`.`c` = 'xpchild' where (`test`.`sbtest1`.`id` = 0) |
        +-------+------+-----------------------------------------------------------------------------------------------------------------------------+
        1 row in set (0.00 sec)
        ```

    4.  Query the status of the statement queue used.

        ```
        mysql> call dbms_ccl.show_ccl_queue();
        +------+-------+-------------------+---------+---------+----------+
        | ID   | TYPE  | CONCURRENCY_COUNT | MATCHED | RUNNING | WAITTING |
        +------+-------+-------------------+---------+---------+----------+
        |    1 | QUEUE |                64 |       0 |       0 |        0 |
        |    2 | QUEUE |                64 |       0 |       0 |        0 |
        |    3 | QUEUE |                64 |       0 |       0 |        0 |
        |    4 | QUEUE |                64 |       0 |       0 |        0 |
        +------+-------+-------------------+---------+---------+----------+
        4 rows in set (0.00 sec)
        ```

    5.  Start the test.

        ```
        sysbench 
        --mysql-host= {$ip}
        --mysql-port= {$port}
        --mysql-db=test 
        --test=./sysbench/share/sysbench/update_non_index.lua 
        --oltp-tables-count=1 
        --oltp_table_size=1 
        --num-threads=128
        --mysql-user=u0
        ```

    6.  View the test result.

        ```
        mysql> call dbms_ccl.show_ccl_queue();
        +------+-------+-------------------+---------+---------+----------+
        | ID   | TYPE  | CONCURRENCY_COUNT | MATCHED | RUNNING | WAITTING |
        +------+-------+-------------------+---------+---------+----------+
        |    1 | QUEUE |                64 |   10996 |      63 |        4 |
        |    2 | QUEUE |                64 |       0 |       0 |        0 |
        |    3 | QUEUE |                64 |       0 |       0 |        0 |
        |    4 | QUEUE |                64 |       0 |       0 |        0 |
        +------+-------+-------------------+---------+---------+----------+
        4 rows in set (0.03 sec)
        
        mysql> call dbms_outln.show_outline();
        +------+--------+-----------+-----------+-------+------+--------------------------------+--------+----------+---------------------------------------------+
        | ID   | SCHEMA | DIGEST    | TYPE      | SCOPE | POS  | HINT                           | HIT    | OVERFLOW | DIGEST_TEXT                                 |
        +------+--------+-----------+-----------+-------+------+--------------------------------+--------+----------+---------------------------------------------+
        |    1 | test   | xxxxxxxxx | OPTIMIZER |       |    1 |  /*+ ccl_queue_field("id") */  | 115795 |        0 | UPDATE `sbtest1` SET `c` = ? WHERE `id` = ? |
        +------+--------+-----------+-----------+-------+------+--------------------------------+--------+----------+---------------------------------------------+
        1 row in set (0.00 sec)
        ```

        **Note:** Based on the query results, the statement outline is hit 115,795 times, the statement queue is hit 10,996 times, a total of 63 statements are being executed concurrently, and four statements are waiting in queue.


