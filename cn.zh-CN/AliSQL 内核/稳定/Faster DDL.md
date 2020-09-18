# Faster DDL

优化DDL操作过程中的Buffer Pool管理机制，降低DDL操作带来的性能影响，提升在线DDL操作的并发数。

实例版本如下：

-   MySQL 8.0（[内核小版本](/cn.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)为20200630或以上）
-   MySQL 5.7（[内核小版本](/cn.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)为20200630或以上）
-   MySQL 5.6（[内核小版本](/cn.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)为20200630或以上）

数据库经常会执行DDL操作，也经常会遇到DDL相关的问题，例如：

-   为什么加索引会造成实例的抖动，影响正常的业务读写？
-   为什么不到1 GB的表执行DDL有时需要十几分钟？
-   为什么使用了临时表的连接退出时会造成实例抖动？

针对这些常见问题，RDS内核团队进行分析后发现MySQL在DDL操作期间的缓存维护逻辑存在性能缺陷，通过深入分析及多次测试，开发Faster DDL功能，优化了Buffer Pool页面管理策略，大幅减少DDL操作导致的锁争用，有效解决或缓解上述问题，让您的实例在正常业务压力下可以安心执行DDL操作。

## 开启Faster DDL

您可以在控制台修改参数**loose\_innodb\_rds\_faster\_ddl**为**ON**，开启Faster DDL。详情请参见[设置实例参数](/cn.zh-CN/RDS MySQL 数据库/实例参数/参数模板/设置实例参数.md)。

## DDL场景测试

-   测试场景

    选取RDS MySQL 8.0支持的两种In Place Online DDL操作进行验证， 其中CREATE INDEX操作不需要重建表，OPTIMIZE TABLE操作需要重建表。

    |操作|Instant|In Place|重建表|允许并发DML|只修改元数据|
    |--|-------|--------|---|-------|------|
    |CREATE INDEX|否|是|否|是|否|
    |OPTIMIZE TABLE|否|是|是|是|否|

-   测试实例

    MySQL 8.0实例（8核、64 GB），执行DDL操作的表大小为600 MB。

-   测试过程

    使用Sysbench模拟线上业务进行压力测试，在压测期间执行DDL操作，进行反复对比测试。

-   测试结果

    |操作|平均执行时间（关闭优化）|平均执行时间（开启优化）|性能提升倍数|
    |--|------------|------------|------|
    |Create Index|56秒|4.9秒|11.4|
    |Optimize Table|220秒|17秒|12.9|

-   测试小结

    在DDL场景下，优化后的AliSQL内核MySQL相比社区版本MySQL，DDL操作执行时间缩短了90%以上。


## 临时表场景测试

MySQL在很多情况下会使用临时表，例如查询information\_schema库里的表、 加速复杂SQL执行时自动创建临时表。在线程退出时系统会集中清理用过的临时表，这也属于一种特殊类型的DDL操作，同样会导致实例的性能抖动。 详情请参见[Temp ibt tablespace truncation at disconnection stuck InnoDB under large BP](https://bugs.mysql.com/bug.php?id=98869)。

-   测试实例

    MySQL 8.0实例（8核、64 GB）。

-   测试过程

    使用tpcc-mysql进行压力测试，将Buff Pool基本用满，然后发起单线程短连接的临时表请求。

-   测试结果

    |对比项|正常情况（无DDL操作）|开启优化|关闭优化|
    |---|------------|----|----|
    |每秒事务数（TPS）|42,000|40,000|<10,000|

    压测过程中的秒级性能数据如下图所示（红线处为关闭DDL加速功能）：

    ![TPS性能](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5381749951/p130824.png)

-   测试小结

    原生MySQL在每次临时表线程退出时出现剧烈的性能抖动，TPS下降超过70%，开启优化之后性能影响降低至5%。


## 优化效果

Faster DDL加速功能支持RDS MySQL 5.6、5.7、8.0三个版本，但是不同版本支持加速的DDL类型不同，详情请参见下表。

|分类|DDL操作|MySQL 5.6|MySQL 5.7|MySQL 8.0|
|--|-----|---------|---------|---------|
|In Place DDL|详情请参见[MySQL 8.0 Online DDL Operations](https://dev.mysql.com/doc/refman/8.0/en/innodb-online-ddl-operations.html)和[MySQL 5.7 Online DDL Operations](https://dev.mysql.com/doc/refman/5.7/en/innodb-online-ddl-operations.html)。|否|是|是|
|表空间管理|开关表空间加密。|否|是|是|
|释放或删除表空间。|否|是|是|
|丢弃表空间。|是|是|是|
|删除表|释放或删除表。|是|是|是|
|Undo操作|释放或删除undo表空间。|否|否|是|
|刷新表|刷新表及脏页。|是|是|是|

## Faster DDL解决的缺陷

Faster DDL完美解决了以下MySQL临时缺陷：

-   [Bug \#95582: DDL using bulk load is very slow under long flush\_list](https://bugs.mysql.com/bug.php?id=95582)
-   [Bug \#98869: Temp ibt tablespace truncation at disconnection stuck InnoDB under large BP](https://bugs.mysql.com/bug.php?id=98869)
-   [Bug \#99021: BUF\_REMOVE\_ALL\_NO\_WRITE is not needed for undo tablespace](https://bugs.mysql.com/bug.php?id=99021)
-   [Bug \#98974: InnoDB temp table could hurt InnoDB perf badly](https://bugs.mysql.com/bug.php?id=98974)

