# AliSQL Release Notes {#concept_kry_21l_n2b .concept}

## MySQL 8.0 {#section_qws_5xk_n2b .section}

**20190915**

-   新特性

    支持事务性本机过程。

-   Bug修复

    修复Cmd\_set\_current\_connection内存泄露问题。


**20190816**

-   新特性
    -   [Thread Pool](cn.zh-CN/AliSQL内核/Thread Pool.md#)：将线程和会话分离，在拥有大量会话的同时，只需要少量线程完成活跃会话的任务即可。
    -   [Statement Concurrency Control](cn.zh-CN/AliSQL内核/Statement Concurrency Control.md#)：通过控制并发数应对突发的数据库请求流量、资源消耗过高的语句访问以及SQL访问模型的变化，保证MySQL实例持续稳定运行。
    -   [Statement Outline](cn.zh-CN/AliSQL内核/Statement Outline.md#)：利用Optimizer Hint和Index Hint让MySQL稳定执行计划。
    -   [Recycle Bin](cn.zh-CN/AliSQL内核/Recycle Bin.md#)：临时将删除的表转移到回收站，还可以设置保留的时间，方便您找回数据。
    -   [Sequence Engine](cn.zh-CN/AliSQL内核/Sequence Engine.md#)：简化获取序列值的复杂度。
    -   [Purge Large File Asynchronously](cn.zh-CN/AliSQL内核/Purge Large File Asynchronously.md#)：删除单个表空间时，会将表空间文件重命名为临时文件，等待异步清除进程清理临时文件。
    -   [Performance Insight](cn.zh-CN/AliSQL内核/Performance Insight.md#)：专注于实例负载监控、关联分析、性能调优的利器，帮助您迅速评估数据库负载，找到性能问题的源头，提升数据库的稳定性。
    -   优化实例锁状态：实例锁定状态下，可以drop或truncate表。
-   Bug修复
    -   修复文件大小计算错误的问题。
    -   修复偶尔出现的内存空闲后再次使用的问题。
    -   修复主机缓存大小为0时的崩溃问题。
    -   修复隐式主键与CTS语句的冲突问题。
    -   修复慢查询导致的slog出错问题。

**20190601**

-   性能优化
    -   缩短日志表MDL范围，减少MDL阻塞的可能性。
    -   重构终止选项的代码。
-   Bug修复
    -   修复审计日志中没有记录预编译语句的问题。
    -   屏蔽无效表名的错误日志。

## MySQL 5.7 {#section_4d5_4iq_4a4 .section}

**20190915**

-   新特性

    [Thread Pool](cn.zh-CN/AliSQL内核/Thread Pool.md#)：将线程和会话分离，在拥有大量会话的同时，只需要少量线程完成活跃会话的任务即可。

-   Bug修复
    -   修复MySQL测试用例rpl\_kill\_query。
    -   修复MySQL测试用例innitialize-sha256。

**20190815**

-   新特性
    -   [Purge Large File Asynchronously](cn.zh-CN/AliSQL内核/Purge Large File Asynchronously.md#)：删除单个表空间时，会将表空间文件重命名为临时文件，等待异步清除进程清理临时文件。
    -   [Performance Insight](cn.zh-CN/AliSQL内核/Performance Insight.md#)：专注于实例负载监控、关联分析、性能调优的利器，帮助您迅速评估数据库负载，找到性能问题的源头，提升数据库的稳定性。
    -   优化实例锁状态：实例锁定状态下，可以drop或truncate表。
-   Bug修复
    -   禁止在`set rds_current_connection`命令中设置rds\_prepare\_begin\_id。
    -   允许更改已锁定用户的信息。
    -   禁止用关键字actual作为表名。
    -   修复慢日志导致时间字段溢出的问题。

**20190510版本**

新特性：允许在事务内创建临时表。

**20190319版本**

新特性：支持在handshake报文内代理设置threadID。

**20190131版本**

-   升级到官方5.7.25版本。
-   关闭内存管理功能jemalloc。
-   修复内部变量net\_lenth\_size计算错误问题。

**20181226版本**

-   新特性：支持动态修改binlog-row-event-max-size，加速无主键表的复制。
-   修复Proxy实例内存申请异常的问题。

**20181010版本**

-   支持隐式主键。
-   加快无主键表的主备复制。
-   支持Native AIO，提升I/O性能。

**20180431版本**

新特性：

-   支持高可用版。
-   支持[SQL审计](../../../../cn.zh-CN/RDS for MySQL 用户指南/SQL审计与历史事件/SQL审计.md#)。
-   增强对处于快照备份状态的实例的保护。

## MySQL 5.6 {#section_d3k_zxk_n2b .section}

**20190815**

优化实例锁状态：实例锁定状态下，可以drop或truncate表。

**20190130版本**

修复部分可能导致系统不稳定的bug。

**20181010版本**

添加参数rocksdb\_ddl\_commit\_in\_the\_middle（MyRocks）。如果这个参数被打开，部分DDL在执行过程中将会执行commit操作。

**201806\*\* （5.6.16）版本**

新特性：slow log精度提升为微秒。

**20180426（5.6.16）版本**

-   新特性：引入隐藏索引，支持将索引设置为不可见，详情请参见[参考文档](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2017-07-16)#1-invisible-indexes)。
-   修复备库apply线程的bug。
-   修复备库apply分区表更新时性能下降问题。
-   修复TokuDB下alter table comment重建整张表问题，详情请参见[参考文档](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2018-05-01)#1-alter-tokudb-table-comment-rebuild-whole-engine-data)。
-   修复由show slave status/show status可能触发的死锁问题。

**20171205（5.6.16）版本**

-   修复OPTIMIZE TABLE和ONLINE ALTER TABLE同时执行时会触发死锁的问题。
-   修复SEQUENCE与隐含主键冲突的问题。
-   修复SHOW CREATE SEQUENCE问题。
-   修复TokuDB引擎的表统计信息错误。
-   修复并行OPTIMIZE表引入的死锁问题。
-   修复QUERY\_LOG\_EVENT中记录的字符集问题。
-   修复信号处理引起的数据库无法停止问题，详情请参见[参考文档](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-%282017-10-10%29#1-the-ack-receiver-thread-didnt-handle-signal-correctly)。
-   修复RESET MASTER引入的问题。
-   修复备库陷入等待的问题。
-   修复SHOW CREATE TABLE可能触发的进程崩溃问题。

**20170927（5.6.16）版本**

修复TokuDB表查询时使用错误索引问题。

**20170901（5.6.16）版本**

-   新特性：
    -   升级SSL加密版本到TLS 1.2，详情请参见[参考文档](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2017-10-10)#2-upgrade-ssl-tlsv12)。
    -   支持Sequence。
-   修复NOT IN查询在特定场景下返回结果集有误的问题。

**20170530 \(5.6.16\)版本**

新特性：支持高权限账号Kill其他账号下的连接。

**20170221（5.6.16）版本**

新特性：支持[读写分离简介](../../../../cn.zh-CN/RDS for MySQL 用户指南/只读实例与读写分离/读写分离简介.md#)。

## MySQL 5.5 {#section_ap5_kn3_25v .section}

**20181212**

修复调用系统函数gettimeofday\(2\) 返回值不准确的问题。该系统函数返回值为时间，常用来计算等待超时，时间不准确时会导致一些操作永不超时。

