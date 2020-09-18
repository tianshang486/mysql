# Performance Insight

Performance Insight是专注于实例负载监控、关联分析、性能调优的利器，帮助您迅速评估数据库负载，找到性能问题的源头，提升数据库的稳定性。

-   实例版本如下：
    -   MySQL 8.0
    -   MySQL 5.7
-   内核小版本需要为20190915或以上。

    **说明：** 您可以在基本信息页面的**配置信息**区域查看是否有**升级内核小版本**按钮。如果有按钮，您可以单击按钮查看当前版本；如果没有按钮，表示已经是最新版。详情请参见[升级内核小版本](/cn.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7620649951/p61646.png)


## Performance Insight介绍

Performance Insight由如下两部分组成：

-   Object statistics

    Object statistics查询表和索引的统计信息，包括如下两个表：

    -   TABLE\_STATISTICS：记录读取和修改的行。
    -   INDEX\_STATISTICS：记录索引的读取行。
-   Performance point

    Performance point提供实例的详细性能信息，方便您更快更准确地量化SQL的开销。Performance point包括如下三个维度：

    -   CPU：包括执行任务的总时间（Elapsed time）、CPU执行任务的时间（CPU time）等。
    -   LOCK：包括服务器MDL锁时间、存储事务锁时间、互斥冲突（仅调试模式）、读写锁冲突等。
    -   IO：数据文件读写时间、日志文件写入时间、逻辑读取、物理读取、物理异步读取等。

## Object statistics使用方法

1.  确认参数OPT\_TABLESTAT和OPT\_INDEXSTAT的值为ON。示例如下：

    ```
    mysql> show variables like "opt_%_stat";
      +---------------+-------+
      | Variable_name | Value |
      +---------------+-------+
      | opt_indexstat | ON    |
      | opt_tablestat | ON    |
      +---------------+-------+
    ```

    **说明：** 如果参数找不到或参数值不为ON，请确认您的实例版本是否为MySQL 5.7。

2.  在information\_schema数据库查询TABLE\_STATISTICS表或INDEX\_STATISTICS表，查看表和索引的统计信息。示例如下：

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

    参数说明如下。

    |参数|说明|
    |--|--|
    |TABLE\_SCHEMA|数据库名称。|
    |TABLE\_NAME|表名称。|
    |ROWS\_READ|读的行数。|
    |ROWS\_CHANGED|修改的行数。|
    |ROWS\_CHANGED\_X\_INDEXES|索引修改的行数。|
    |ROWS\_INSERTED|插入的行数。|
    |ROWS\_DELETED|删除的行数。|
    |ROWS\_UPDATED|更新的行数。|
    |INDEX\_NAME|索引名称。|


## Performance point使用方法

1.  确认Performance point的相关参数。正常的示例如下：

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

    **说明：** 如果参数找不到，请确认您的实例版本是否为MySQL 5.7。

2.  在performance\_schema数据库查询events\_statements\_summary\_by\_digest\_supplement表，查看排名前10的SQL语句。示例如下：

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

    参数说明如下。

    |参数|说明|
    |--|--|
    |SCHEMA\_NAME|数据库名称。|
    |DIGEST|**Digest\_text**进行hash计算得到的64字节的hash字符串。|
    |DIGEST\_TEXT|SQL语句的特征。|
    |ELAPSED\_TIME|实际运行时间。单位：μs。|
    |CPU\_TIME|CPU运行时间。单位：μs。|
    |SERVER\_LOCK\_TIME|服务器锁定时间。单位：μs。|
    |TRANSACTION\_LOCK\_TIME|存储事务锁定时间。单位：μs。|
    |MUTEX\_SPINS|互斥旋转次数。|
    |MUTEX\_WAITS|互斥等待次数。|
    |RWLOCK\_SPIN\_WAITS|读写闩锁的自旋等待数。|
    |RWLOCK\_SPIN\_ROUNDS|读写闩锁的旋转循环圈数。|
    |RWLOCK\_OS\_WAITS|读写闩锁的操作系统等待数。|
    |DATA\_READS|数据文件读取次数。|
    |DATA\_READ\_TIME|数据文件读取时间。单位：μs。|
    |DATA\_WRITES|数据文件写入次数。|
    |DATA\_WRITE\_TIME|数据文件写入时间。单位：μs。|
    |REDO\_WRITES|日志文件写入次数。|
    |REDO\_WRITE\_TIME|日志文件写入时间。单位：μs。|
    |LOGICAL\_READS|逻辑页读取次数。|
    |PHYSICAL\_READS|物理页读取次数。|
    |PHYSICAL\_ASYNC\_READS|物理异步页读取次数。|

3.  在information\_schema数据库查询IO\_STATISTICS表，查看最近的数据读写情况。示例如下：

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

    参数说明如下。

    |参数|说明|
    |--|--|
    |TIME|日期。|
    |DATA\_READ|数据读取次数。|
    |DATA\_READ\_TIME|数据读取总时间。单位：μs。|
    |DATA\_READ\_MAX\_TIME|数据读取最长时间。单位：μs。|
    |DATA\_READ\_BYTES|数据读取总大小。单位：byte。|
    |DATA\_WRITE|数据写入次数。|
    |DATA\_WRITE\_TIME|数据写入总时间。单位：μs。|
    |DATA\_WRITE\_MAX\_TIME|数据写入最长时间。单位：μs。|
    |DATA\_WRITE\_BYTES|数据写入总大小。单位：byte。|


