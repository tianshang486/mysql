# AliSQL 小版本 Release Notes

本文介绍AliSQL的内核版本更新说明。

**说明：** 关于RDS MySQL独享代理的小版本说明请参见[独享代理小版本 Release Notes](/cn.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/独享代理小版本 Release Notes.md)。

## MySQL 8.0

|小版本|说明|
|---|--|
|20201031|-   新特性
    -   支持从[Recycle Bin](/cn.zh-CN/自研内核 AliSQL/安全/Recycle Bin.md)还原表。
    -   实例初始化时自动恢复Slow Log文件。
-   性能优化

使用X-Engine引擎时不支持开启[Binlog in Redo](/cn.zh-CN/自研内核 AliSQL/性能/Binlog in Redo.md)。

-   Bug修复
    -   修复唯一索引键值过大导致ASSERT异常的问题。
    -   修复无法终止COM\_DAEMON守护进程的问题。
    -   修复FTS查询导致缓存溢出的问题。
    -   修复Instant-DDL崩溃后回滚出错的问题。 |
|20200831|-   新特性
    -   增加选项禁用`count(*)`并行扫描功能。
    -   MySQL Binlog工具增加开始GTID（start gtid）和结束GTID（stop gtid）功能。
    -   支持输出Redo Log的各个LSN值：
        -   innodb\_lsn：重做日志的lsn编号。
        -   innodb\_log\_checkpoint\_lsn：最后检查点的lsn。
        -   innodb\_log\_write\_lsn：log写入的lsn。
        -   innodb\_log\_ready\_for\_write\_lsn：log buffer完成时间的lsn。
        -   innodb\_log\_flush\_lsn：磁盘上刷新redo log的lsn。
        -   innodb\_log\_dirty\_pages\_added\_up\_to\_lsn：添加脏页的lsn。
        -   innodb\_log\_oldest\_lsn：页面刷新的lsn。
-   性能优化
    -   优化CCL（Concurrency Control）的等待与并发机制。
    -   调整Concurrency Control在存储过程中的执行优先级。
-   Bug修复
    -   修复解析器递归时缺少堆内存大小检查的问题。
    -   修复TDE打开时无法修改表定义的问题。
    -   修复事件调度程序内存泄露的问题。 |
|20200630|-   新特性
    -   [Faster DDL](/cn.zh-CN/自研内核 AliSQL/稳定/Faster DDL.md)：优化DDL操作过程中的Buffer Pool管理机制，降低DDL操作带来的性能影响，提升在线DDL操作的并发数。
    -   增加连接数上限，最大支持500,000连接。
-   性能优化
    -   线程池内部优化。
    -   根据实例规格设置Performance Schema占用内存的上限。
    -   不再检测审计日志文件。
    -   TDE会缓存KMS服务提供的密钥。
    -   修改在[Statement Concurrency Control](/cn.zh-CN/自研内核 AliSQL/稳定/Statement Concurrency Control.md)中运行的线程状态。
-   Bug修复
    -   修复Outline计算摘要时将分号（;）视为输入查询的其中一部分的问题。
    -   修复更改表导致服务器崩溃的问题。
    -   修复关键字member和array与旧版本不兼容的问题。
    -   修复读取客户端命令时的等待计数不正确的问题。
    -   修复内核小版本升级失败的问题。 |
|20200430|-   新特性
    -   [Binlog in Redo](/cn.zh-CN/自研内核 AliSQL/性能/Binlog in Redo.md)：通过将Binlog写入Redo Log来优化事务落盘机制，提高数据库性能。
    -   [Data Protect](/cn.zh-CN/自研内核 AliSQL/安全/Data Protect.md)：允许定制不同的安全策略，收缩DROP和TRUNCATE操作权限，防止数据被误删。
    -   重构X-Engine引擎的行缓存代码。
    -   开放XA\_RECOVER\_ADMIN权限。
-   性能优化
    -   在操作InnoDB临时表时仅扫描脏页列表，而不是扫描整个Buffer Pool列表。
    -   兼容MySQL 5.6，将全局参数opt\_readonly\_trans\_implicit\_commit重命名为rds\_disable\_explicit\_trans。
    -   在实例升级期间，不记录升级相关日志到审计日志。
    -   降低在X-Engine引擎表上执行DDL操作消耗的内存。
-   Bug修复
    -   修复磁盘中实际X-Engine引擎表大小与IS表中的统计信息不一致的问题。
    -   修复重新打开错误日志会导致X-Engine日志初始化的问题。 |
|20200331|-   新特性

[Recycle Bin](/cn.zh-CN/自研内核 AliSQL/安全/Recycle Bin.md)：新增支持`TRUNCATE TABLE`命令，执行时将原始表移动到专门的recycle bin目录中，并使用相同的结构创建新表。

-   性能优化
    -   默认关闭TCP错误的输出。
    -   提高线程池默认配置下的性能。
-   Bug修复
    -   修复因为`#p`分割分区文件名导致的数据库、表无效问题。
    -   修复CCL匹配时区分大小写问题，即不再区分大小写。
-   合并官方8.0.17、8.0.18变更，详情请参见[Changes in MySQL 8.0.17](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-17.html)和[Changes in MySQL 8.0.18](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-18.html)。 |
|20200229|-   新特性
    -   [Performance Agent](/cn.zh-CN/自研内核 AliSQL/稳定/Performance Agent.md)：更加便捷的性能数据统计方案。通过MySQL插件的方式，实现MySQL实例内部各项性能数据的采集与统计。
    -   在半同步模式下添加网络往返时间，并记录到性能数据。
    -   X-Engine引擎支持在线DDL功能。
-   性能优化
    -   允许在只读实例上进行语句级并发控制（CCL）操作。
    -   备实例支持Outline。
    -   Proxy短连接优化。
    -   优化不同CPU架构下的pause指令执行时间。
    -   添加内存表查看线程池运行情况。
-   Bug修复
    -   在低于4.9的Linux Kernel中禁用ppoll，使用poll代替。
    -   修复wrap\_sm4\_encrypt函数调用错误问题。
    -   修复在滚动审核日志时持有全局变量锁的问题。
    -   修复恢复不一致性检查的问题。
    -   修复io\_statistics表出现错误time值的问题。
    -   修复无效压缩算法导致崩溃的问题。
    -   修复用户列与5.6不兼容的问题。
-   修补程序
    -   [Faster DDL](/cn.zh-CN/自研内核 AliSQL/稳定/Faster DDL.md)：优化DDL操作过程中的Buffer Pool管理机制，降低DDL操作带来的性能影响，提升在线DDL操作的并发数。
    -   线程池性能优化。
    -   修复缓冲区计数泄漏问题。 |
|20200110|-   新特性

[Inventory Hint](/cn.zh-CN/自研内核 AliSQL/性能/Inventory Hint.md)：新增了三个hint， 支持SELECT、UPDATE、INSERT、DELETE 语句，快速提交/回滚事务，提高业务吞吐能力。

-   性能优化
    -   启动实例时，先初始化Concurrency Control队列结构，再初始化Concurrency Control规则。
    -   异步清除文件时取消小文件的链接。
    -   优化[Thread Pool](/cn.zh-CN/自研内核 AliSQL/功能/Thread Pool.md)性能。
    -   默认情况下禁用恢复不一致性检查。
    -   更改设置变量所需的权限：
        -   设置以下变量所需的权限已更改为普通用户权限：
            -   auto\_increment\_increment
            -   auto\_increment\_offset
            -   bulk\_insert\_buffer\_size
            -   binlog\_rows\_query\_log\_events
        -   设置以下变量所需的权限已更改为超级用户或系统变量管理用户权限：
            -   binlog\_format
            -   binlog\_row\_image
            -   binlog\_direct
            -   sql\_log\_off
            -   sql\_log\_bin |
|20191225|-   新特性

[Recycle Bin](/cn.zh-CN/自研内核 AliSQL/安全/Recycle Bin.md)：临时将删除的表转移到回收站，还可以设置保留的时间，方便您找回数据。

-   性能优化
    -   提高短连接处理性能。
    -   使用专用线程为maintain user服务，避免HA失败。
    -   通过Redo刷新Binlog时出现错误会显式释放文件同步锁。
    -   删除不必要的TCP错误日志。
    -   默认情况下启用线程池。
-   Bug修复
    -   修复慢日志刷新的问题。
    -   修复锁定范围不正确的问题。
    -   修复TDE的Select函数导致的核心转储问题。 |
|20191115|新特性

[Statement Queue](/cn.zh-CN/自研内核 AliSQL/性能/Statement Queue.md)：针对语句的排队机制，将语句进行分桶排队，尽量把可能具有相同冲突的语句放在一个桶内排队，减少冲突的开销。 |
|20191101|-   新特性
    -   为[TDE](/cn.zh-CN/RDS MySQL 数据库/数据安全/加密/设置透明数据加密TDE.md)添加SM4加密算法。
    -   保护备实例信息：拥有SUPER或REPLICATION\_SLAVE\_ADMIN权限的用户才能插入/删除/修改表slave\_master\_info、slave\_relay\_log\_info、slave\_worker\_info。
    -   提高自动递增键的优先级：如果表中没有主键或非空唯一键，具有自动增量的非空键将是第一候选项。
    -   对系统表和处于初始化状态线程用到的表，不进行Memory引擎到MyISAM引擎的自动转换。
    -   Redo Log刷新到磁盘之前先将Binlog文件刷新到磁盘。
    -   实例被锁定时也会影响临时表。
    -   添加新的基于LSM树的事务存储引擎X-Engine。
-   性能优化
    -   [Thread Pool](/cn.zh-CN/自研内核 AliSQL/功能/Thread Pool.md)：互斥优化。
    -   [Performance Insight](/cn.zh-CN/自研内核 AliSQL/稳定/Performance Insight.md)：性能点支持线程池。
    -   参数调整：
        -   `primary_fast_lookup`：会话参数，默认值为true。
        -   `thread_pool_enabled`：全局参数，默认值为true。 |
|20191015|-   新特性
    -   [TDE](/cn.zh-CN/RDS MySQL 数据库/数据安全/加密/设置透明数据加密TDE.md)：支持透明数据加密TDE（Transparent Data Encryption）功能，可对数据文件执行实时I/O加密和解密，数据在写入磁盘之前进行加密，从磁盘读入内存时进行解密。
    -   [Returning](/cn.zh-CN/自研内核 AliSQL/功能/Returning.md)：Returning功能支持DML语句返回Resultset，同时提供了工具包（DBMS\_TRANS）便于您快捷使用。
    -   强制将引擎从MyISAM或MEMORY转换为InnoDB：如果全局变量**force\_mysiam\_to\_innodb**或**force\_memory\_to\_innodb**为**ON**，则创建和修改表时会将表引擎从MyISAM或MEMORY转换为InnoDB。
    -   禁止非高权限账号切换主备实例。
    -   性能代理插件：收集性能数据并保存到本地格式化文本文件，采用文件轮循方式，保留最近的秒级性能数据。
    -   Innodb mutex timeout configurable：可配置全局变量**innodb\_fatal\_semaphore\_wait\_threshold**，默认值：600。
    -   忽略索引提示错误：可配置全局变量**ignore\_index\_hint\_error**，默认值：false。
    -   可关闭[SSL加密](/cn.zh-CN/RDS MySQL 数据库/数据安全/加密/设置SSL加密.md)功能。
    -   TCP错误信息：返回TCP方向（读取、读取等待、写入等待）错误及错误代码到end\_connection事件，并且输出错误信息到错误日志。
-   Bug修复
    -   支持本地AIO的Linux系统内，在触发线性预读之前会合并AIO请求。
    -   优化表/索引统计信息。
    -   如果指定了主键，则直接访问主索引。 |
|20190915|Bug修复

修复Cmd\_set\_current\_connection内存泄露问题。 |
|20190816|-   新特性
    -   [Thread Pool](/cn.zh-CN/自研内核 AliSQL/功能/Thread Pool.md)：将线程和会话分离，在拥有大量会话的同时，只需要少量线程完成活跃会话的任务即可。
    -   [Statement Concurrency Control](/cn.zh-CN/自研内核 AliSQL/稳定/Statement Concurrency Control.md)：通过控制并发数应对突发的数据库请求流量、资源消耗过高的语句访问以及SQL访问模型的变化，保证MySQL实例持续稳定运行。
    -   [Statement Outline](/cn.zh-CN/自研内核 AliSQL/功能/Statement Outline.md)：利用Optimizer Hint和Index Hint让MySQL稳定执行计划。
    -   [Sequence Engine](/cn.zh-CN/自研内核 AliSQL/功能/Sequence Engine.md)：简化获取序列值的复杂度。
    -   [Purge Large File Asynchronously](/cn.zh-CN/自研内核 AliSQL/稳定/Purge Large File Asynchronously.md)：删除单个表空间时，会将表空间文件重命名为临时文件，等待异步清除进程清理临时文件。
    -   [Performance Insight](/cn.zh-CN/自研内核 AliSQL/稳定/Performance Insight.md)：专注于实例负载监控、关联分析、性能调优的利器，帮助您迅速评估数据库负载，找到性能问题的源头，提升数据库的稳定性。
    -   优化实例锁状态：实例锁定状态下，可以drop或truncate表。
-   Bug修复
    -   修复文件大小计算错误的问题。
    -   修复偶尔出现的内存空闲后再次使用的问题。
    -   修复主机缓存大小为0时的崩溃问题。
    -   修复隐式主键与CTS语句的冲突问题。
    -   修复慢查询导致的slog出错问题。 |
|20190601|-   性能优化
    -   缩短日志表MDL范围，减少MDL阻塞的可能性。
    -   重构终止选项的代码。
-   Bug修复
    -   修复审计日志中没有记录预编译语句的问题。
    -   屏蔽无效表名的错误日志。 |

## MySQL 5.7基础版或高可用版

|小版本|说明|
|---|--|
|20201031|Bug修复

-   修复并发更新导致ROW\_SEARCH\_MVCC崩溃的问题。
-   修复更改innodb\_undo\_tablespaces导致无法启动的问题。
-   修复FTS查询导致缓存溢出的问题。 |
|20200831|-   新特性
    -   合并官方5.7.30变更，详情请参见[GitHub](https://github.com/mysql/mysql-server)。
    -   优化CCL（Concurrency Control）的等待与并发机制。
    -   MySQL Binlog工具增加开始GTID（start gtid）和结束GTID（stop gtid）功能。
    -   支持输出Redo Log的各个LSN值：
        -   innodb\_lsn：重做日志的lsn编号。
        -   innodb\_log\_write\_lsn：log写入的lsn。
        -   innodb\_log\_checkpoint\_lsn：最后检查点的lsn。
        -   innodb\_log\_flushed\_lsn：磁盘上刷新redo log的lsn。
        -   innodb\_log\_Pages\_flushed：页面刷新的lsn。
-   性能优化

调整Concurrency Control在存储过程中的执行优先级。

-   Bug修复

修复服务器在关闭时异常终止的严重错误。 |
|20200630|-   新特性
    -   [Inventory Hint](/cn.zh-CN/自研内核 AliSQL/性能/Inventory Hint.md)：新增了三个hint， 支持SELECT、UPDATE、INSERT、DELETE 语句，快速提交/回滚事务，提高业务吞吐能力。
    -   [Statement Concurrency Control](/cn.zh-CN/自研内核 AliSQL/稳定/Statement Concurrency Control.md)：通过控制并发数应对突发的数据库请求流量、资源消耗过高的语句访问以及SQL访问模型的变化，保证MySQL实例持续稳定运行。
    -   [Statement Queue](/cn.zh-CN/自研内核 AliSQL/性能/Statement Queue.md)：针对语句的排队机制，将语句进行分桶排队，尽量把可能具有相同冲突的语句放在一个桶内排队，减少冲突的开销。
    -   [Statement Outline](/cn.zh-CN/自研内核 AliSQL/功能/Statement Outline.md)：利用Optimizer Hint和Index Hint让MySQL稳定执行计划。
    -   [Faster DDL](/cn.zh-CN/自研内核 AliSQL/稳定/Faster DDL.md)：优化DDL操作过程中的Buffer Pool管理机制，降低DDL操作带来的性能影响，提升在线DDL操作的并发数。
    -   增加连接数上限，最大支持500,000连接。
-   性能优化
    -   可通过`call dbms_admin.show_native_procedure();`命令查看所有本机过程。
    -   新增删除孤立表的函数。
    -   线程池内部优化。
    -   优化查询缓存。
    -   根据实例规格设置Performance Schema占用内存的上限。
-   Bug修复

修复审计刷新线程进入死循环的问题。 |
|20200430|-   新特性

[Data Protect](/cn.zh-CN/自研内核 AliSQL/安全/Data Protect.md)：允许定制不同的安全策略，收缩DROP和TRUNCATE操作权限，防止数据被误删。

-   性能优化

QueryCache中删除rwlock，并将默认哈希函数从LF\_hash改为murmur3 hash。

-   Bug修复

修复在事务隔离（可重复读级别）中命中查询缓存时的两个错误。 |
|20200331|-   新特性
    -   [Fast Query Cache](/cn.zh-CN/自研内核 AliSQL/性能/Fast Query Cache.md)：针对原生MySQL Query Cache的不足，阿里云进行重新设计和全新实现，推出RDS Query Cache，能够有效提高数据库查询性能。
    -   从percona-server 5.7移植两个MDL锁，LOCK TABLES FOR BACKUP （LTFB）和LOCK BINLOG FOR BACKUP （LBFB）。
-   性能优化
    -   添加线程池对低版本的兼容。
    -   默认关闭TCP错误的输出。
    -   提高线程池默认配置下的性能。
-   Bug修复
    -   修复清理大文件时包含临时文件的问题。
    -   修复线程池转储线程超时的问题。
    -   修复进程上下文中IPK字段计数错误的问题。
    -   修复rds\_change\_user导致的pfs线程泄漏和释放问题。
-   合并官方5.7.28变更，详情请参见[GitHub](https://github.com/mysql/mysql-server)。 |
|20200229|-   新特性
    -   [Performance Agent](/cn.zh-CN/自研内核 AliSQL/稳定/Performance Agent.md)：更加便捷的性能数据统计方案。通过MySQL插件的方式，实现MySQL实例内部各项性能数据的采集与统计。
    -   在半同步模式下添加网络往返时间，并记录到性能数据。
-   性能优化
    -   优化不同CPU架构下的pause指令执行时间。
    -   Proxy短连接优化。
    -   添加内存表查看线程池运行情况。
-   Bug修复
    -   修复DDL重做日志不安全的问题。
    -   修复io\_statistics表出现错误time值的问题。
    -   修复更改表导致服务器崩溃的问题。
    -   修复MySQL测试用例。 |
|20200110|性能优化

-   异步清除文件时取消小文件的链接。
-   优化[Thread Pool](/cn.zh-CN/自研内核 AliSQL/功能/Thread Pool.md)性能。
-   thread\_pool\_enabled参数的默认值调整为OFF。 |
|20191225|-   新特性

内部账户管理与防范：调整用户权限保护数据安全。

-   性能优化
    -   提高短连接处理性能。
    -   使用专用线程为maintain user服务，避免HA失败。
    -   删除不必要的TCP错误日志。
    -   优化线程池。
-   Bug修复
    -   修复读写分离时mysqld进程崩溃问题。
    -   修复密钥环引起的核心转储问题。 |
|20191115|Bug修复

修复主备切换后审计日志显示变量的问题。 |
|20191101|-   新特性
    -   为[TDE](/cn.zh-CN/RDS MySQL 数据库/数据安全/加密/设置透明数据加密TDE.md)添加SM4加密算法。
    -   如果指定了主键，则直接访问主索引。
    -   对系统表和处于初始化状态线程用到的表，不进行Memory引擎到MyISAM引擎的自动转换。
-   性能优化
    -   [Thread Pool](/cn.zh-CN/自研内核 AliSQL/功能/Thread Pool.md)：互斥优化。
    -   引入审计日志缓冲机制，提高审计日志的性能。
    -   [Performance Insight](/cn.zh-CN/自研内核 AliSQL/稳定/Performance Insight.md)：性能点支持线程池。
    -   默认开启[Thread Pool](/cn.zh-CN/自研内核 AliSQL/功能/Thread Pool.md)。
-   Bug修复
    -   在处理维护用户列表时释放锁。
    -   补充更多TCP错误信息。 |
|20191015|-   新特性
    -   轮换慢日志：为了在收集慢查询日志时保证零数据丢失，轮换日志表会将慢日志表的csv数据文件重命名为唯一名称并创建新文件。您可以使用`show variables like '%rotate_log_table%';`查看是否开启轮换慢日志。
    -   性能代理插件：收集性能数据并保存到本地格式化文本文件，采用文件轮循方式，保留最近的秒级性能数据。
    -   强制将引擎从MEMORY转换为InnoDB：如果全局变量**rds\_force\_memory\_to\_innodb**为**ON**，则创建/修改表时会将表引擎从MEMORY转换为InnoDB。
    -   TDE机制优化：添加keyring-rds插件与管控系统/密钥管理服务进行交互。
    -   TCP错误信息：返回TCP方向（读取、读取等待、写入等待）错误及错误代码到end\_connection事件，并且输出错误信息到错误日志。
-   Bug修复

修复DDL中的意外错误Error 1290。 |
|20190925|参数修改

-   将系统变量auto\_generate\_certs的默认值由true改为false。
-   增加全局只读变量auto\_detact\_certs，默认值为false，有效值为\[true \| false\]。 该系统变量在Server端使用OpenSSL编译时可用，用于控制Server端在启动时是否在数据目录下自动查找SSL加密证书和密钥文件，即控制是否开启Server端的证书和密钥的自动查找功能。 |
|20190915|新特性

[Thread Pool](/cn.zh-CN/自研内核 AliSQL/功能/Thread Pool.md)：将线程和会话分离，在拥有大量会话的同时，只需要少量线程完成活跃会话的任务即可。 |
|20190815|-   新特性
    -   [Purge Large File Asynchronously](/cn.zh-CN/自研内核 AliSQL/稳定/Purge Large File Asynchronously.md)：删除单个表空间时，会将表空间文件重命名为临时文件，等待异步清除进程清理临时文件。
    -   [Performance Insight](/cn.zh-CN/自研内核 AliSQL/稳定/Performance Insight.md)：专注于实例负载监控、关联分析、性能调优的利器，帮助您迅速评估数据库负载，找到性能问题的源头，提升数据库的稳定性。
    -   优化实例锁状态：实例锁定状态下，可以drop或truncate表。
-   Bug修复
    -   禁止在`set rds_current_connection`命令中设置rds\_prepare\_begin\_id。
    -   允许更改已锁定用户的信息。
    -   禁止用关键字actual作为表名。
    -   修复慢日志导致时间字段溢出的问题。 |
|20190510|新特性

允许在事务内创建临时表。 |
|20190319|新特性

支持在handshake报文内代理设置threadID。 |
|20190131|-   性能优化
    -   升级到官方5.7.25版本。
    -   关闭内存管理功能jemalloc。
-   Bug修复

修复内部变量net\_lenth\_size计算错误问题。 |
|20181226|-   新特性

支持动态修改binlog-row-event-max-size，加速无主键表的复制。

-   Bug修复

修复Proxy实例内存申请异常的问题。 |
|20181010|性能优化

-   支持隐式主键。
-   加快无主键表的主备复制。
-   支持Native AIO，提升I/O性能。 |
|20180431|新特性

-   支持高可用版。
-   支持[SQL审计]()。
-   增强对处于快照备份状态的实例的保护。 |

## MySQL 5.7三节点企业版

|小版本|说明|
|---|--|
|20191128|-   新特性

支持读写分离。

-   Bug修复
    -   修复部分场景下Follower Second\_Behind\_Master计算错误问题。
    -   修复表级并行复制事务重试时死锁问题。
    -   修复XA相关bug。 |
|20191016|-   新特性
    -   支持MySQL 5.7高可用版（本地SSD盘）升级到三节点企业版。
    -   兼容MySQL官方GTID功能，默认不开启。
    -   合并AliSQL MySQL 5.7基础版/高可用版 20190915版本及之前的自研功能。
-   Bug修复

修复重置备实例导致binlog被关闭问题。 |
|20190909|-   新特性
    -   优化大事务在三节点强一致状态下的执行效率。
    -   支持从Leader/Follower进行Binlog转储。
    -   支持创建只读实例。
    -   系统表默认使用InnoDB引擎。
-   Bug修复
    -   修复Follower日志清理命令失效问题。
    -   修复参数slave\_sql\_verify\_checksum=OFF和binlog\_checksum=crc32时Slave线程异常退出问题。 |
|20190709|新特性

-   支持三节点功能。
-   禁用semi-sync插件。
-   支持表级并行复制、Writeset并行复制。
-   支持pk\_access主键查询加速。
-   支持线程池。
-   合并AliSQL MySQL 5.7基础版/高可用版 20190510版本及之前的自研功能。 |

## MySQL 5.6

|小版本|说明|
|---|--|
|20201031|Bug修复

-   修复IN子句内的子查询无效的问题。
-   修复进程权限错误的问题。
-   修复kill\_user\_list表中用户授权的问题。
-   修复`DROP DATABASE`语句出错的问题。
-   修复PREVIOUS\_GTID事件导致SECONDS\_BEHIND\_MASTER计算错误的问题。 |
|20200831|-   新特性

支持输出Redo Log的各个LSN值：

    -   innodb\_lsn：重做日志的lsn编号。
    -   innodb\_log\_write\_lsn：log写入的lsn。
    -   innodb\_log\_checkpoint\_lsn：最后检查点的lsn。
    -   innodb\_log\_flushed\_lsn：磁盘上刷新redo log的lsn。
    -   innodb\_log\_Pages\_flushed：页面刷新的lsn。
-   Bug修复
    -   修复SHOW\_HA\_ROWS类型错误的问题。
    -   修复过程上下文中IPK字段计数错误的问题。
    -   修复查询INFORMATION\_SCHEMA导致服务器崩溃的问题。
    -   修复审计刷新线程死循环的问题。
    -   修复备实例不报告主备延迟的问题。 |
|20200630|-   新特性
    -   [Performance Agent](/cn.zh-CN/自研内核 AliSQL/稳定/Performance Agent.md)：更加便捷的性能数据统计方案。通过MySQL插件的方式，实现MySQL实例内部各项性能数据的采集与统计。
    -   增加连接数上限，最大支持500,000连接。
    -   [Faster DDL](/cn.zh-CN/自研内核 AliSQL/稳定/Faster DDL.md)：优化DDL操作过程中的Buffer Pool管理机制，降低DDL操作带来的性能影响，提升在线DDL操作的并发数。
-   性能优化
    -   增加全局参数max\_execution\_time，当SQL语句执行时间超过此参数值时会被中断。
    -   线程池内部优化。
-   Bug修复

修复读取客户端命令时的等待计数不正确的问题。 |
|20200430|-   新特性
    -   [Data Protect](/cn.zh-CN/自研内核 AliSQL/安全/Data Protect.md)：允许定制不同的安全策略，避免DROP和TRUNCATE操作导致数据丢失。
    -   增加存储MDL锁信息的表mdl\_info。
-   Bug修复

解决同时开启线程池和ic\_reduce（秒杀）功能的冲突问题。 |
|20200331|性能优化

-   提高线程池默认配置下的性能。
-   默认关闭TCP错误的输出。 |
|20200229|-   新特性

支持Proxy读写分离功能。

-   性能优化
    -   优化线程池功能。
    -   优化不同CPU架构下的pause指令执行时间。
-   Bug修复

修复XA事务部分提交的问题。 |
|20200110|-   新特性

[Thread Pool](/cn.zh-CN/自研内核 AliSQL/功能/Thread Pool.md)：将线程和会话分离，在拥有大量会话的同时，只需要少量线程完成活跃会话的任务即可。

-   性能优化

异步清除文件时取消小文件的链接。

-   Bug修复
    -   修复页面清理程序的睡眠时间计算不正确问题。
    -   修复`SELECT @@global.gtid_executed`导致的故障转移失败问题。
    -   修复[IF CLIENT KILLED AFTER ROLLBACK TO SAVEPOINT PREVIOUS STMTS COMMITTED](https://bugs.mysql.com/bug.php?id=79596)问题。 |
|20191212|性能优化

删除不必要的tcp错误日志 |
|20191115|Bug修复

修复慢日志时间戳溢出问题。 |
|20191101|Bug修复

-   修复刷新日志时切换慢日志的问题，仅在执行刷新慢日志时切换慢日志。
-   修正部分显示错误。 |
|20191015|-   新特性
    -   轮换慢日志：为了在收集慢查询日志时保证零数据丢失，轮换日志表会将慢日志表的csv数据文件重命名为唯一名称并创建新文件。您可以使用`show variables like '%rotate_log_table%';`查看是否开启轮换慢日志。
    -   SM4加密算法：添加新的SM4加密算法，取代旧的SM加密算法。
    -   [Purge Large File Asynchronously](/cn.zh-CN/自研内核 AliSQL/稳定/Purge Large File Asynchronously.md)：删除单个表空间时，会将表空间文件重命名为临时文件，等待异步清除进程清理临时文件。
    -   TCP错误信息：返回TCP方向（读取、读取等待、写入等待）错误及错误代码到end\_connection事件，并且输出错误信息到错误日志。
    -   引入审计日志缓冲机制，提高审计日志的性能。
-   Bug修复
    -   禁用pstack，避免存在大量连接时可能导致pstack无响应。
    -   修复隐式主键与`create table as select`语句之间的冲突。
    -   自动清除由二进制日志创建的临时文件。 |
|20190815|性能优化

优化实例锁状态：实例锁定状态下，可以drop或truncate表。 |
|20190130|Bug修复

修复部分可能导致系统不稳定的bug。 |
|20181010|性能优化

添加参数rocksdb\_ddl\_commit\_in\_the\_middle（MyRocks）。如果这个参数被打开，部分DDL在执行过程中将会执行commit操作。 |
|201806\*\*|新特性

slow log精度提升为微秒。 |
|20180426|-   新特性

引入隐藏索引，支持将索引设置为不可见，详情请参见[参考文档](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2017-07-16)#1-invisible-indexes)。

-   Bug修复
    -   修复备库apply线程的bug。
    -   修复备库apply分区表更新时性能下降问题。
    -   修复TokuDB下alter table comment重建整张表问题，详情请参见[参考文档](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2018-05-01)#1-alter-tokudb-table-comment-rebuild-whole-engine-data)。
    -   修复由show slave status/show status可能触发的死锁问题。 |
|20171205|Bug修复

-   修复OPTIMIZE TABLE和ONLINE ALTER TABLE同时执行时会触发死锁的问题。
-   修复SEQUENCE与隐含主键冲突的问题。
-   修复SHOW CREATE SEQUENCE问题。
-   修复TokuDB引擎的表统计信息错误。
-   修复并行OPTIMIZE表引入的死锁问题。
-   修复QUERY\_LOG\_EVENT中记录的字符集问题。
-   修复信号处理引起的数据库无法停止问题，详情请参见[参考文档](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-%282017-10-10%29#1-the-ack-receiver-thread-didnt-handle-signal-correctly)。
-   修复RESET MASTER引入的问题。
-   修复备库陷入等待的问题。
-   修复SHOW CREATE TABLE可能触发的进程崩溃问题。 |
|20170927|Bug修复

修复TokuDB表查询时使用错误索引问题。 |
|20170901|-   新特性
    -   升级SSL加密版本到TLS 1.2，详情请参见[参考文档](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2017-10-10)#2-upgrade-ssl-tlsv12)。
    -   支持Sequence。
-   Bug修复

修复NOT IN查询在特定场景下返回结果集有误的问题。 |
|20170530|新特性

支持高权限账号Kill其他账号下的连接。 |
|20170221|新特性

支持[读写分离](/cn.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/读写分离.md)。 |

## MySQL 5.5

|小版本|说明|
|---|--|
|20181212|Bug修复

修复调用系统函数`gettimeofday(2)`返回值不准确的问题。该系统函数返回值为时间，常用来计算等待超时，时间不准确时会导致一些操作永不超时。 |

