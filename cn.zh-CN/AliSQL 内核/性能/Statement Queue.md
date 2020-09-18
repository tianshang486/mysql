# Statement Queue

AliSQL设计了针对语句的排队机制，将语句进行分桶排队，尽量把可能具有相同冲突的语句（例如操作相同行）放在一个桶内排队，减少冲突的开销。

MySQL的服务层和引擎层在语句并发执行过程中，有很多串行的点容易导致冲突。例如在DML语句中，事务锁冲突比较常见，InnoDB中事务锁的最细粒度是行级锁，如果语句针对相同行进行并发操作，会导致冲突比较严重，系统吞吐量会随着并发的增加而递减。AliSQL提供Statement Queue机制，能够减少冲突开销、有效提高实例性能。

## 前提条件

实例版本如下：

-   MySQL 8.0
-   MySQL 5.7

## 效果

在单行进行并发UPDATE的场景下测试，相比较原生的MySQL，AliSQL有接近4倍的提升。

## 变量

AliSQL提供了两个变量来定义语句队列的桶数量和大小：

-   ccl\_queue\_bucket\_count：表示桶的数量。取值范围：1~64；默认值：4。
-   ccl\_queue\_bucket\_size：表示一个桶允许的并发数。取值范围：1~4096；默认值：64。

**说明：** 您可以在RDS控制台修改变量值，详情请参见[设置实例参数](/cn.zh-CN/RDS MySQL 数据库/实例参数/参数模板/设置实例参数.md)。

## 语法

AliSQL支持两种hint语法：

-   ccl\_queue\_value

    根据值进行hash分桶。

    语法：

    ```
    /*+ ccl_queue_value([int | string)] */
    ```

    示例：

    ```
    update /*+ ccl_queue_value(1) */ t set c=c+1 where id = 1;
    
    update /*+ ccl_queue_value('xpchild') */ t set c=c+1 where name = 'xpchild';
    ```

-   ccl\_queue\_field

    根据where条件中的字段值进行hash分桶。

    语法：

    ```
    /*+ ccl_queue_field(string) */
    ```

    示例：

    ```
    update /*+ ccl_queue_field("id") */ t set c=c+1 where id = 1 and name = 'xpchild';
    ```

    **说明：** ccl\_queue\_field语法中，where条件只支持原始字段（没有在字段上使用任何函数、计算等）的二元运算，并且二元运算的右侧值必须是数字或者字符串。


## 接口

AliSQL提供两个接口便于您查询Statement Queue状态：

-   dbms\_ccl.show\_ccl\_queue\(\)

    查询当前Statement Queue状态。

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

    参数说明如下。

    |参数|说明|
    |--|--|
    |CONCURRENCY\_COUNT|最大并发数。|
    |MATCHED|命中规则的总数。|
    |RUNNING|当前并发的数量。|
    |WAITTING|当前等待的数量。|

-   dbms\_ccl.flush\_ccl\_queue\(\)

    清理内存中的数据。

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


## 实践

为避免冗长的应用业务代码的修改，Statement Queue可以配合[Statement Outline](/cn.zh-CN/AliSQL 内核/功能/Statement Outline.md)进行在线业务修改，方便快捷。下文使用SysBench的update\_non\_index为例进行演示。

-   测试环境
    -   测试表结构

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

    -   测试语句

        ```
        UPDATE sbtest1 SET c='xpchild' WHERE id=0;
        ```

    -   测试脚本

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

-   测试过程
    1.  在线增加Statement Outline。

        ```
        mysql> CALL DBMS_OUTLN.add_optimizer_outline('test', '', 1, 
                                                     ' /*+ ccl_queue_field("id") */ ',
                                 "UPDATE sbtest1 SET c='xpchild' WHERE id=0");
        Query OK, 0 rows affected (0.01 sec)
        ```

    2.  查看Statement Outline。

        ```
        mysql> call dbms_outln.show_outline();
        +------+--------+------------------------------------------------------------------+-----------+-------+------+--------------------------------+------+----------+---------------------------------------------+
        | ID   | SCHEMA | DIGEST                                                           | TYPE      | SCOPE | POS  | HINT                           | HIT  | OVERFLOW | DIGEST_TEXT                                 |
        +------+--------+------------------------------------------------------------------+-----------+-------+------+--------------------------------+------+----------+---------------------------------------------+
        |    1 | test   | 7b945614749e541e0600753367884acff5df7e7ee2f5fb0af5ea58897910f023 | OPTIMIZER |       |    1 |  /*+ ccl_queue_field("id") */  |    0 |        0 | UPDATE `sbtest1` SET `c` = ? WHERE `id` = ? |
        +------+--------+------------------------------------------------------------------+-----------+-------+------+--------------------------------+------+----------+---------------------------------------------+
        1 row in set (0.00 sec)
        ```

    3.  验证Statement Outline生效。

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

    4.  查询Statement Queue状态。

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

    5.  开启测试。

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

    6.  验证测试效果。

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

        **说明：** 查询结果显示Statement Outline命中了115,795次规则，Statement Queue状态显示命中了10,996次排队，当前运行并发63个，排队等待4个。


