# Performance Agent

Performance Agent是AliSQL提供的一种更加便捷的性能数据统计方案。通过MySQL插件的方式，实现MySQL实例内部各项性能数据的采集与统计。

## 背景信息

Performance Agent在information\_schema系统库下新增了一张内存表PERF\_STATISTICS，用于统计最近一段时间的性能数据，您可以直接查询该表获取相关指标的性能数据。

## 前提条件

实例版本如下：

-   MySQL 8.0（内核小版本20200229或以上）
-   MySQL 5.7（内核小版本20200229或以上）
-   MySQL 5.6（内核小版本20200630或以上）

**说明：** 升级内核小版本请参见[升级内核小版本](/cn.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)。

## 参数说明

与Performance Agent功能相关的参数说明如下。

|参数|说明|
|--|--|
|performance\_agent\_enabled|是否开启Performance Agent功能。取值：ON \| OFF。默认值为ON。|
|performance\_agent\_interval|性能数据采集间隔。单位为秒，默认值为1。|
|performance\_agent\_perfstat\_volume\_size|PERF\_STATISTICS表的最大数据条数。默认值为3600。即当采样间隔为1秒时，保存最近1小时的性能数据。|

## 表结构说明

PERF\_STATISTICS内存表的结构如下：

```
CREATE TEMPORARY TABLE `PERF_STATISTICS` (
  `TIME` datetime NOT NULL DEFAULT '0000-00-00 00:00:00',
  `PROCS_MEM_USAGE` double NOT NULL DEFAULT '0',
  `PROCS_CPU_RATIO` double NOT NULL DEFAULT '0',
  `PROCS_IOPS` double NOT NULL DEFAULT '0',
  `PROCS_IO_READ_BYTES` bigint(21) NOT NULL DEFAULT '0',
  `PROCS_IO_WRITE_BYTES` bigint(21) NOT NULL DEFAULT '0',
  `MYSQL_CONN_ABORT` int(11) NOT NULL DEFAULT '0',
  `MYSQL_CONN_CREATED` int(11) NOT NULL DEFAULT '0',
  `MYSQL_USER_CONN_COUNT` int(11) NOT NULL DEFAULT '0',
  `MYSQL_CONN_RUNNING` int(11) NOT NULL DEFAULT '0',
  `MYSQL_LOCK_IMMEDIATE` int(11) NOT NULL DEFAULT '0',
  `MYSQL_LOCK_WAITED` int(11) NOT NULL DEFAULT '0',
  `MYSQL_COM_INSERT` int(11) NOT NULL DEFAULT '0',
  `MYSQL_COM_UPDATE` int(11) NOT NULL DEFAULT '0',
  `MYSQL_COM_DELETE` int(11) NOT NULL DEFAULT '0',
  `MYSQL_COM_SELECT` int(11) NOT NULL DEFAULT '0',
  `MYSQL_COM_COMMIT` int(11) NOT NULL DEFAULT '0',
  `MYSQL_COM_ROLLBACK` int(11) NOT NULL DEFAULT '0',
  `MYSQL_COM_PREPARE` int(11) NOT NULL DEFAULT '0',
  `MYSQL_LONG_QUERY` int(11) NOT NULL DEFAULT '0',
  `MYSQL_TCACHE_GET` bigint(21) NOT NULL DEFAULT '0',
  `MYSQL_TCACHE_MISS` bigint(21) NOT NULL DEFAULT '0',
  `MYSQL_TMPFILE_CREATED` int(11) NOT NULL DEFAULT '0',
  `MYSQL_TMP_TABLES` int(11) NOT NULL DEFAULT '0',
  `MYSQL_TMP_DISKTABLES` int(11) NOT NULL DEFAULT '0',
  `MYSQL_SORT_MERGE` int(11) NOT NULL DEFAULT '0',
  `MYSQL_SORT_ROWS` int(11) NOT NULL DEFAULT '0',
  `MYSQL_BYTES_RECEIVED` bigint(21) NOT NULL DEFAULT '0',
  `MYSQL_BYTES_SENT` bigint(21) NOT NULL DEFAULT '0',
  `MYSQL_BINLOG_OFFSET` int(11) NOT NULL DEFAULT '0',
  `MYSQL_IOLOG_OFFSET` int(11) NOT NULL DEFAULT '0',
  `MYSQL_RELAYLOG_OFFSET` int(11) NOT NULL DEFAULT '0',
  `EXTRA` json NOT NULL DEFAULT 'null'
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

|列名|说明|
|--|--|
|TIME|时间，格式为yyyy-MM-dd HH:mm:ss。|
|PROCS\_MEM\_USAGE|物理内存使用量，单位为Byte。|
|PROCS\_CPU\_RATIO|CPU使用率。|
|PROCS\_IOPS|系统IO调用次数。|
|PROCS\_IO\_READ\_BYTES|IO读取数据量，单位为Byte。|
|PROCS\_IO\_WRITE\_BYTES|IO写入数据量，单位为Byte。|
|MYSQL\_CONN\_ABORT|断开连接数。|
|MYSQL\_CONN\_CREATED|新建连接数。|
|MYSQL\_USER\_CONN\_COUNT|当前总的用户连接数。|
|MYSQL\_CONN\_RUNNING|当前活跃连接数。|
|MYSQL\_LOCK\_IMMEDIATE|当前锁占用数。|
|MYSQL\_LOCK\_WAITED|当前锁等待数。|
|MYSQL\_COM\_INSERT|插入语句数。|
|MYSQL\_COM\_UPDATE|更新语句数。|
|MYSQL\_COM\_DELETE|删除语句数。|
|MYSQL\_COM\_SELECT|查询语句数。|
|MYSQL\_COM\_COMMIT|事务提交数（显式提交）。|
|MYSQL\_COM\_ROLLBACK|事务回滚数。|
|MYSQL\_COM\_PREPARE|预处理语句数。|
|MYSQL\_LONG\_QUERY|慢查询数。|
|MYSQL\_TCACHE\_GET|缓存表命中数。|
|MYSQL\_TCACHE\_MISS|缓存表未命中数。|
|MYSQL\_TMPFILE\_CREATED|临时文件创建数。|
|MYSQL\_TMP\_TABLES|临时表创建数。|
|MYSQL\_TMP\_DISKTABLES|临时磁盘表创建数。|
|MYSQL\_SORT\_MERGE|合并排序次数。|
|MYSQL\_SORT\_ROWS|排序行数。|
|MYSQL\_BYTES\_RECEIVED|接收数据量，单位为Byte。|
|MYSQL\_BYTES\_SENT|发送数据量，单位为Byte。|
|MYSQL\_BINLOG\_OFFSET|产生的Binlog文件大小，单位为Byte。|
|MYSQL\_IOLOG\_OFFSET|主库发送的Binlog文件大小，单位为Byte。|
|MYSQL\_RELAYLOG\_OFFSET|从库应用的Binlog文件大小，单位为Byte。|
|EXTRA|InnoDB统计信息。EXTRA包含多个字段，为JSON格式。详细字段介绍请参见下方[表 1](#table_z5j_t5y_wkb)。 **说明：** InnoDB统计信息的指标项与`SHOW STATUS`命令显示的值相同。 |

|字段|说明|
|--|--|
|INNODB\_TRX\_CNT|事务数。|
|INNODB\_DATA\_READ|读取数据量，单位为Byte。|
|INNODB\_IBUF\_SIZE|合并记录页数。|
|INNODB\_LOG\_WAITS|Log写入等待次数。|
|INNODB\_MAX\_PURGE|清除事务数。|
|INNODB\_N\_WAITING|锁等待数。|
|INNODB\_ROWS\_READ|读取数据行数。|
|INNODB\_LOG\_WRITES|日志写次数。|
|INNODB\_IBUF\_MERGES|合并次数。|
|INNODB\_DATA\_WRITTEN|写入数据量，单位为Byte。|
|INNODB\_DBLWR\_WRITES|双写操作写入次数。|
|INNODB\_IBUF\_SEGSIZE|当前插入缓冲大小。|
|INNODB\_ROWS\_DELETED|删除数据行数。|
|INNODB\_ROWS\_UPDATED|更新数据行数。|
|INNODB\_COMMIT\_TRXCNT|提交事务数。|
|INNODB\_IBUF\_FREELIST|空闲列表长度。|
|INNODB\_MYSQL\_TRX\_CNT|MySQL事务数。|
|INNODB\_ROWS\_INSERTED|插入数据行数。|
|INNODB\_ACTIVE\_TRX\_CNT|活跃事务数。|
|INNODB\_OS\_LOG\_WRITTEN|日志文件写入量，单位为Byte。|
|INNODB\_ACTIVE\_VIEW\_CNT|活跃视图数。|
|INNODB\_RSEG\_HISTORY\_LEN|TRX\_RSEG\_HISTORY表长度。|
|INNODB\_AVG\_COMMIT\_TRXTIME|平均事务提交时间。|
|INNODB\_MAX\_COMMIT\_TRXTIME|最长事务提交时间。|
|INNODB\_DBLWR\_PAGES\_WRITTEN|双写操作完成写入次数。|

## 使用方法

-   直接查询系统表，获取性能数据。 您可以参见如下示例：
    -   查询最近30秒的CPU和内存使用情况，示例如下：

        ```
        MySQL> select TIME, PROCS_MEM_USAGE, PROCS_CPU_RATIO from information_schema.PERF_STATISTICS order by time DESC limit 30;
        +---------------------+-----------------+-----------------+
        | TIME                | PROCS_MEM_USAGE | PROCS_CPU_RATIO |
        +---------------------+-----------------+-----------------+
        | 2020-02-27 11:15:36 |       857812992 |           18.55 |
        | 2020-02-27 11:15:35 |       857808896 |           18.54 |
        | 2020-02-27 11:15:34 |       857268224 |           19.64 |
        | 2020-02-27 11:15:33 |       857268224 |           21.06 |
        | 2020-02-27 11:15:32 |       857264128 |           20.39 |
        | 2020-02-27 11:15:31 |       857272320 |           20.32 |
        | 2020-02-27 11:15:30 |       857272320 |           21.35 |
        | 2020-02-27 11:15:29 |       857272320 |            28.8 |
        | 2020-02-27 11:15:28 |       857268224 |           29.08 |
        | 2020-02-27 11:15:27 |       857268224 |           26.92 |
        | 2020-02-27 11:15:26 |       857268224 |           23.84 |
        | 2020-02-27 11:15:25 |       857264128 |           13.76 |
        | 2020-02-27 11:15:24 |       857264128 |           15.12 |
        | 2020-02-27 11:15:23 |       857264128 |           14.76 |
        | 2020-02-27 11:15:22 |       857264128 |           15.38 |
        | 2020-02-27 11:15:21 |       857260032 |           13.23 |
        | 2020-02-27 11:15:20 |       857260032 |           12.75 |
        | 2020-02-27 11:15:19 |       857260032 |           12.17 |
        | 2020-02-27 11:15:18 |       857255936 |           13.22 |
        | 2020-02-27 11:15:17 |       857255936 |           20.51 |
        | 2020-02-27 11:15:16 |       857255936 |           28.74 |
        | 2020-02-27 11:15:15 |       857251840 |           29.85 |
        | 2020-02-27 11:15:14 |       857251840 |           29.31 |
        | 2020-02-27 11:15:13 |       856981504 |           28.85 |
        | 2020-02-27 11:15:12 |       856981504 |           29.19 |
        | 2020-02-27 11:15:11 |       856977408 |           29.12 |
        | 2020-02-27 11:15:10 |       856977408 |           29.32 |
        | 2020-02-27 11:15:09 |       856977408 |            29.2 |
        | 2020-02-27 11:15:08 |       856973312 |           29.36 |
        | 2020-02-27 11:15:07 |       856973312 |           28.79 |
        +---------------------+-----------------+-----------------+
        30 rows in set (0.08 sec)
        ```

    -   查询最近30秒的InnoDB读写的数据行数，示例如下：

        ```
        MySQL> select TIME, EXTRA->'$.INNODB_ROWS_READ', EXTRA->'$.INNODB_ROWS_INSERTED' from information_schema.PERF_STATISTICS order by time DESC limit 30;
        +---------------------+-----------------------------+---------------------------------+
        | TIME                | EXTRA->'$.INNODB_ROWS_READ' | EXTRA->'$.INNODB_ROWS_INSERTED' |
        +---------------------+-----------------------------+---------------------------------+
        | 2020-02-27 11:22:17 | 39209                       | 0                               |
        | 2020-02-27 11:22:16 | 36098                       | 0                               |
        | 2020-02-27 11:22:15 | 38035                       | 0                               |
        | 2020-02-27 11:22:14 | 37384                       | 0                               |
        | 2020-02-27 11:22:13 | 38336                       | 0                               |
        | 2020-02-27 11:22:12 | 33946                       | 0                               |
        | 2020-02-27 11:22:11 | 36301                       | 0                               |
        | 2020-02-27 11:22:10 | 36835                       | 0                               |
        | 2020-02-27 11:22:09 | 36900                       | 0                               |
        | 2020-02-27 11:22:08 | 36402                       | 0                               |
        | 2020-02-27 11:22:07 | 39672                       | 0                               |
        | 2020-02-27 11:22:06 | 39316                       | 0                               |
        | 2020-02-27 11:22:05 | 37830                       | 0                               |
        | 2020-02-27 11:22:04 | 36396                       | 0                               |
        | 2020-02-27 11:22:03 | 34820                       | 0                               |
        | 2020-02-27 11:22:02 | 37350                       | 0                               |
        | 2020-02-27 11:22:01 | 39463                       | 0                               |
        | 2020-02-27 11:22:00 | 38419                       | 0                               |
        | 2020-02-27 11:21:59 | 37673                       | 0                               |
        | 2020-02-27 11:21:58 | 35117                       | 0                               |
        | 2020-02-27 11:21:57 | 36140                       | 0                               |
        | 2020-02-27 11:21:56 | 37592                       | 0                               |
        | 2020-02-27 11:21:55 | 39765                       | 0                               |
        | 2020-02-27 11:21:54 | 35553                       | 0                               |
        | 2020-02-27 11:21:53 | 35882                       | 0                               |
        | 2020-02-27 11:21:52 | 37061                       | 0                               |
        | 2020-02-27 11:21:51 | 40699                       | 0                               |
        | 2020-02-27 11:21:50 | 39608                       | 0                               |
        | 2020-02-27 11:21:49 | 39317                       | 0                               |
        | 2020-02-27 11:21:48 | 37413                       | 0                               |
        +---------------------+-----------------------------+---------------------------------+
        30 rows in set (0.08 sec)
        ```

-   对接性能监控平台，实现实时监控。例如使用[Grafana](https://grafana.com/)。

    ![Grafana](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0940359951/p87223.png)


