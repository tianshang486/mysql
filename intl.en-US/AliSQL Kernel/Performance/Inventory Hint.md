# Inventory Hint

This topic describes the Inventory Hint feature provided by AliSQL. This feature can work with the Returning and Statement Queue features to commit and roll back transactions rapidly.

## Background information

In business scenarios such as seckilling, inventory reduction is a common task model that requires high concurrency and serialization. In this model, AliSQL uses queues and transactional hints to control concurrency and commit or roll back transactions. This increases the throughput of your business.

## Prerequisites

The RDS instance version is one of the following:

-   MySQL 8.0
-   MySQL 5.7
-   MySQL 5.6

## Syntax

The following three hints are introduced to specify tables in SELECT, UPDATE, INSERT, and DELETE statements.

-   COMMIT\_ON\_SUCCESS and ROLLBACK\_ON\_FAIL

    These are two transactional hints.

    -   COMMIT\_ON\_SUCCESS: specifies to commit the transaction if the execution of the statement to which this hint is applied succeeds.
    -   ROLLBACK\_ON\_FAIL: specifies to roll the transaction back if the execution of the statement to which this hint is applied fails.
    Syntax:

    ```
    /*+ COMMIT_ON_SUCCESS */
    /*+ ROLLBACK_ON_FAIL */
    ```

    Example:

    ```
    UPDATE /*+ COMMIT_ON_SUCCESS ROLLBACK_ON_FAIL */ T
    SET c = c - 1
    WHERE id = 1;
    ```

-   TARGET\_AFFECT\_ROW\(NUMBER\)

    This is a conditional hint. After you apply it to a statement, the execution of the statement succeeds only when the number of affected rows is the same as the number specified in this hint.

    Syntax:

    ```
    /*+ TARGET_AFFECT_ROW(NUMBER) */
    ```

    Example:

    ```
    UPDATE /*+ TARGET_AFFECT_ROW(1) */ T
    SET c = c - 1
    WHERE id = 1;
    ```


## Precautions

-   The transactional hints do not support the autocommit mode. If you use a transactional hint in a statement with the autocommit mode, an error is reported. Example:

    ```
    mysql> UPDATE /*+ commit_on_success rollback_on_fail target_affect_row(1) */ t
        -> SET col1 = col1 + 1
        -> WHERE id = 1;
    ERROR 7531 (HY000): Inventory transactinal hints didn't allowed in autocommit mode
    ```

-   Transactional hints cannot be used in substatements. If you use a transactional hint in a substatement, an error is reported. Example:

    ```
      mysql> CREATE TRIGGER tri_1
        -> BEFORE INSERT ON t
        -> FOR EACH ROW
        -> BEGIN
        -> INSERT /*+ commit_on_success */ INTO t1 VALUES (1);
        -> end//
    
    mysql> INSERT INTO t VALUES (2, 1);
    ERROR HY000: Inventory transactional hints didn't alllowed in stored procedure
    ```

-   The conditional hint cannot be used in a SELECT or EXPLAIN statement. If you use the conditional hint in a SELECT or EXPLAIN statement, an error is reported. Example:

    ```
    mysql> EXPLAIN UPDATE /*+ commit_on_success rollback_on_fail target_affect_row(1) */ t
        -> SET col1 = col1 + 1
        -> WHERE id = 1;
    ERROR 7532 (HY000): Inventory conditional hints didn't match with result
    ```

    **Note:** You can specify an invalid number in the TARGET\_AFFECT\_ROW hint and check whether the system reports errors:

    ```
    mysql> EXPLAIN UPDATE /*+ commit_on_success rollback_on_fail target_affect_row(-1) */ t
        -> SET col1 = col1 + 1
        -> WHERE id = 1;
    +----+-------------+-------+------------+-------+---------------+---------+---------+-------+------+----------+-------------+
    | id | select_type | table | partitions | type  | possible_keys | key     | key_len | ref   | rows | filtered | Extra       |
    +----+-------------+-------+------------+-------+---------------+---------+---------+-------+------+----------+-------------+
    |  1 | UPDATE      | t     | NULL       | range | PRIMARY       | PRIMARY | 4       | const |    1 |   100.00 | Using where |
    +----+-------------+-------+------------+-------+---------------+---------+---------+-------+------+----------+-------------+
    1 row in set, 2 warnings (0.00 sec)
    
    mysql> show warnings;
    +---------+------+-----------------------------------------------------------------------------------------------------------------------------------------+
    | Level   | Code | Message                                                                                                                                 |
    +---------+------+-----------------------------------------------------------------------------------------------------------------------------------------+
    | Warning | 1064 | Optimizer hint syntax error near '-1) */ t set col1=col1+1 where id =1' at line 1                                                       |
    | Note    | 1003 | update /*+ COMMIT_ON_SUCCESS ROLLBACK_ON_FAIL */ `test`.`t` set `test`.`t`.`col1` = (`test`.`t`.`col1` + 1) where (`test`.`t`.`id` = 1) |
    +---------+------+-----------------------------------------------------------------------------------------------------------------------------------------+
    2 rows in set (0.00 sec)
    ```


## Work with Returning

You can use Inventory Hint with [Returning](/intl.en-US/AliSQL Kernel/Feature/Returning.md) for the system to return real-time result sets. Example:

```
mysql> CALL dbms_trans.returning("*", "update /*+ commit_on_success rollback_on_fail target_affect_row(1) */ t
                                       set col1=col1+1 where id=1");
+----+------+
| id | col1 |
+----+------+
|  1 |   13 |
+----+------+
1 row in set (0.00 sec)

mysql> CALL dbms_trans.returning("*", "insert /*+ commit_on_success rollback_on_fail target_affect_row(1) */ into
                                       t values(10,10)");
+----+------+
| id | col1 |
+----+------+
| 10 |   10 |
+----+------+
1 row in set (0.01 sec)
			
```

## Work with Statement Queue

You can use Inventory Hint with [Statement Queue](/intl.en-US/AliSQL Kernel/Performance/Statement Queue.md) for the system to queue statements. Example:

```
mysql> UPDATE /*+ ccl_queue_field(id) commit_on_success rollback_on_fail target_affect_row(1) */ t
    -> SET col1 = col1 + 1
    -> WHERE id = 1;

Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE /*+ ccl_queue_value(1) commit_on_success rollback_on_fail target_affect_row(1) */ t
    -> SET col1 = col1 + 1
    -> WHERE id = 1;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

