# Statement Concurrency Control

为了应对突发的数据库请求流量、资源消耗过高的语句访问以及SQL访问模型的变化， 保证MySQL实例持续稳定运行，阿里云提供基于语句规则的并发控制CCL（Concurrency Control），并提供了工具包（DBMS\_CCL）便于您快捷使用。

## 前提条件

实例版本如下：

-   MySQL 8.0
-   MySQL 5.7

## 注意事项

-   CCL的操作不产生Binlog，所以CCL的操作只影响当前实例。例如主实例进行CCL操作，不会同步到备实例、只读实例或灾备实例。
-   CCL提供超时机制以应对DML导致事务锁死锁，等待中的线程也会响应事务超时和线程KILL操作以应对死锁。

## 功能设计

CCL规则定义了如下三个维度的特征：

-   SQL command

    SQL命令类型，例如SELECT、UPDATE、INSERT、DELETE等。

-   Object

    SQL命令操作的对象，例如TABLE、VIEW等。

-   keywords

    SQL命令的关键字。


## 创建CCL规则表

AliSQL设计了一个系统表（concurrency\_control）保存CCL规则，系统启动时会自动创建该表，无需您手动创建。这里提供表的创建语句供您参考：

```
CREATE TABLE `concurrency_control` (
  `Id` bigint(20) NOT NULL AUTO_INCREMENT,
  `Type` enum('SELECT','UPDATE','INSERT','DELETE') NOT NULL DEFAULT 'SELECT',
  `Schema_name` varchar(64) COLLATE utf8_bin DEFAULT NULL,
  `Table_name` varchar(64) COLLATE utf8_bin DEFAULT NULL,
  `Concurrency_count` bigint(20) DEFAULT NULL,
  `Keywords` text COLLATE utf8_bin,
  `State` enum('N','Y') NOT NULL DEFAULT 'Y',
  `Ordered` enum('N','Y') NOT NULL DEFAULT 'N',
  PRIMARY KEY (`Id`)
) /*!50100 TABLESPACE `mysql` */ ENGINE=InnoDB 
DEFAULT CHARSET=utf8 COLLATE=utf8_bin
STATS_PERSISTENT=0 COMMENT='Concurrency control'
```

|参数|说明|
|--|--|
|Id|CCL规则ID。|
|Type|SQL command，即SQL命令类型。|
|Schema\_name|数据库名。|
|Table\_name|数据库内的表名。|
|Concurrency\_count|并发数。|
|Keywords|关键字，多个关键字用英文分号（;）分隔。|
|State|本规则是否启用。|
|Ordered|Keywords中多个关键字是否按顺序匹配。|

## 管理CCL规则

为了便捷地管理CCL规则，AliSQL在DBMS\_CCL中定义了四个本地存储规则。详细说明如下：

-   add\_ccl\_rule

    增加规则。命令如下：

    ```
    dbms_ccl.add_ccl_rule('<Type>','<Schema_name>','<Table_name>',<Concurrency_count>,'<Keywords>');
    ```

    示例：

    增加规则，SELECT语句的并发数为10。

    ```
    mysql> call dbms_ccl.add_ccl_rule('SELECT', '', '', 10, '');
    ```

    增加规则，SELECT语句中出现关键字key1的并发数为20。

    ```
    mysql> call dbms_ccl.add_ccl_rule('SELECT', '', '', 20, 'key1');
    ```

    增加规则，test.t表的SELECT语句的并发数为20。

    ```
    mysql> call dbms_ccl.add_ccl_rule('SELECT', 'test', 't', 20, '');
    ```

    **说明：** Id越大，规则的优先级越高。

-   del\_ccl\_rule

    删除规则。命令如下：

    ```
    dbms_ccl.del_ccl_rule(<Id>);
    ```

    示例：

    删除规则ID为15的CCL规则。

    ```
    mysql> call dbms_ccl.del_ccl_rule(15);
    ```

    **说明：** 如果删除的规则不存在，系统会报相应的警告，您可以使用`show warnings;`查看警告内容。

    ```
    mysql> call dbms_ccl.del_ccl_rule(100);
      Query OK, 0 rows affected, 2 warnings (0.00 sec)
    
    mysql> show warnings;
    +---------+------+----------------------------------------------------+
    | Level   | Code | Message                                            |
    +---------+------+----------------------------------------------------+
    | Warning | 7514 | Concurrency control rule 100 is not found in table |
    | Warning | 7514 | Concurrency control rule 100 is not found in cache |
    +---------+------+----------------------------------------------------+
    ```

-   show\_ccl\_rule

    查看内存中已启用规则。命令如下：

    ```
    dbms_ccl.show_ccl_rule();
    ```

    示例：

    ```
    ​mysql> call dbms_ccl.show_ccl_rule();
    +------+--------+--------+-------+-------+-------+-------------------+---------+---------+----------+----------+
    | ID   | TYPE   | SCHEMA | TABLE | STATE | ORDER | CONCURRENCY_COUNT | MATCHED | RUNNING | WAITTING | KEYWORDS |
    +------+--------+--------+-------+-------+-------+-------------------+---------+---------+----------+----------+
    |   17 | SELECT | test   | t     | Y     | N     |                30 |       0 |       0 |        0 |          |
    |   16 | SELECT |        |       | Y     | N     |                20 |       0 |       0 |        0 | key1     |
    |   18 | SELECT |        |       | Y     | N     |                10 |       0 |       0 |        0 |          |
    +------+--------+--------+-------+-------+-------+-------------------+---------+---------+----------+----------+​
    ```

    关于MATCHED、RUNNING和WAITTING的说明如下。

    |参数|说明|
    |--|--|
    |MATCHED|规则匹配成功次数。|
    |RUNNING|此规则下正在并发执行的线程数。|
    |WAITTING|此规则下正在等待执行的线程数。|

-   flush\_ccl\_rule

    如果您直接操作了表concurrency\_control修改规则，规则不能立即生效，您需要让规则重新生效。命令如下：

    ```
    dbms_ccl.flush_ccl_rule();
    ```

    示例：

    ```
    ​mysql> update mysql.concurrency_control set CONCURRENCY_COUNT = 15 where Id = 18;
    Query OK, 1 row affected (0.00 sec)
    Rows matched: 1  Changed: 1  Warnings: 0
    
    mysql> call dbms_ccl.flush_ccl_rule();
    Query OK, 0 rows affected (0.00 sec)​
    ```


## 功能测试

-   测试规则

    设计如下三条规则对应三个维度：

    ```
    call dbms_ccl.add_ccl_rule('SELECT', 'test', 'sbtest1', 3, '');  //SELECT命令操作表sbtest1并发数为3
    call dbms_ccl.add_ccl_rule('SELECT', '', '', 2, 'sbtest2');       //SELECT命令关键字sbtest2并发数为2
    call dbms_ccl.add_ccl_rule('SELECT', '', '', 2, '');            //SELECT命令并发数为2
    ```

-   测试场景

    使用sysbench进行测试，场景如下：

    -   64 threads
    -   4 tables
    -   select.lua
-   测试结果

    查看规则并发数情况如下：

    ```
    ​mysql> call dbms_ccl.show_ccl_rule();
    +------+--------+--------+---------+-------+-------+-------------------+---------+---------+----------+----------+
    | ID   | TYPE   | SCHEMA | TABLE   | STATE | ORDER | CONCURRENCY_COUNT | MATCHED | RUNNING | WAITTING | KEYWORDS |
    +------+--------+--------+---------+-------+-------+-------------------+---------+---------+----------+----------+
    |   20 | SELECT | test   | sbtest1 | Y     | N     |                 3 |     389 |       3 |        9 |          |
    |   21 | SELECT |        |         | Y     | N     |                 2 |     375 |       2 |       14 | sbtest2  |
    |   22 | SELECT |        |         | Y     | N     |                 2 |     519 |       2 |       34 |          |
    +------+--------+--------+---------+-------+-------+-------------------+---------+---------+----------+----------+
    3 rows in set (0.00 sec)​
    ```

    查看**RUNNING**列，符合预期的并行数量。


