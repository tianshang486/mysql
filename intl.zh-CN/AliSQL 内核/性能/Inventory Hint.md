# Inventory Hint

AliSQL提供Inventory Hint，帮助您快速提交/回滚事务，配合Returning和Statement Queue，能有效提高业务吞吐能力。

## 背景信息

在秒杀等业务场景中，减少库存是一个常见的需要高并发，同时也需要串行化的任务模型，AliSQL使用排队和事务性hint来控制并发和快速提交/回滚事务，提高业务吞吐能力。

## 前提条件

实例版本如下：

-   MySQL 8.0
-   MySQL 5.6

## 语法

新增了三个hint， 支持SELECT、UPDATE、INSERT、DELETE 语句。

-   COMMIT\_ON\_SUCCESS/ROLLBACK\_ON\_FAIL

    两个事务hint为COMMIT\_ON\_SUCCESS和ROLLBACK\_ON\_FAIL：

    -   COMMIT\_ON\_SUCCESS：当前语句执行成功就提交事务上下文。
    -   ROLLBACK\_ON\_FAIL：当前语句执行失败就回滚事务上下文。
    语法：

    ```
    /*+ COMMIT_ON_SUCCESS */
    /*+ ROLLBACK_ON_FAIL */
    ```

    示例：

    ```
    UPDATE /*+ COMMIT_ON_SUCCESS ROLLBACK_ON_FAIL */ T
    SET c = c - 1
    WHERE id = 1;
    ```

-   TARGET\_AFFECT\_ROW\(NUMBER\)

    条件hint为TARGET\_AFFECT\_ROW\(NUMBER\) ：如果当前语句影响行数是指定的就成功，否则语句失败。

    语法：

    ```
    /*+ TARGET_AFFECT_ROW(NUMBER) */
    ```

    示例：

    ```
    UPDATE /*+ TARGET_AFFECT_ROW(1) */ T
    SET c = c - 1
    WHERE id = 1;
    ```


## 注意事项

-   事务hint不能运行在autocommit模式下， 例如：

    ```
    mysql> UPDATE /*+ commit_on_success rollback_on_fail target_affect_row(1) */ t
        -> SET col1 = col1 + 1
        -> WHERE id = 1;
    ERROR 7531 (HY000): Inventory transactinal hints didn't allowed in autocommit mode
    ```

-   事务hint不能运行在sub statement下，例如：

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

-   条件hint不能运行在SELECT/EXPLAIN statement下， 例如：

    ```
    mysql> EXPLAIN UPDATE /*+ commit_on_success rollback_on_fail target_affect_row(1) */ t
        -> SET col1 = col1 + 1
        -> WHERE id = 1;
    ERROR 7532 (HY000): Inventory conditional hints didn't match with result
    ```

    **说明：** 您可以指定target\_affect\_row为一个无效的number进行测试，系统会有告警。

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


## 配合Returning使用

Inventory Hint可以配合[Returning](/intl.zh-CN/AliSQL 内核/功能/Returning.md)使用，实时返回结果集， 例如：

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

## 配合Statement queue使用

Inventory Hint可以配合[Statement Queue](/intl.zh-CN/AliSQL 内核/性能/Statement Queue.md)进行排队，例如：

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

