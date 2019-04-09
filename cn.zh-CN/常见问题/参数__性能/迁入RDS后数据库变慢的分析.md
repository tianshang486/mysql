# 迁入RDS后数据库变慢的分析 {#concept_q4t_rbg_jhb .concept}

部分用户将数据库迁入RDS后，发现访问速度变慢了。本文将通过真实案例来分析一下迁入RDS后数据库变慢的原因。

## 案例一 {#section_x4k_2dg_jhb .section}

**问题描述：**用户的PostgreSQL数据库数据量在百万级左右，将PostgreSQL数据库迁移到RDS for MySQL后，发现相同的一条SQL语句，在原来PostgreSQL中执行大概是0.015s，而在RDS下执行是6分20秒左右。

**可能原因：**可能是SQL的执行计划改变导致执行时间剧增。

**问题排查：**通过`explain`命令查看SQL的执行计划，一步一步进行优化。

![explain](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8316/155479955443580_zh-CN.png)

通过分析，可以从执行计划上分析出b表做了一个全表扫描\(执行计划的最后一行\)，查看b表中tid并无索引，所以这里可以进行优化，减少查询过程中关联的行数。

![tid](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8316/155479955443582_zh-CN.png)

优化后再次查看执行计划，可以看到执行计划中的**ROWS**已经从452变为了2。

![新执行计划](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8316/155479955443583_zh-CN.png)

再次执行该查询，执行时间已经由原来的6分20秒下降到了10秒。

![10秒](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8316/155479955443586_zh-CN.png)

继续分析执行计划，该SQL的结果集只有8行，但是扫描的行数却是非常多（1055789\*1\*1\*1\*1\*2），在优化SQL时非常关键的一点就是优化SQL的执行路程，检查SQL最后一句：

```
WHERE EXISTS
(SELECT 1 FROM xxxx_test5 b WHERE a.tid = b.tid);
```

SQL查询中是要查询出每笔订单的详细信息而不得不关联其他一些表，但是最后的一个EXISTS限定了我们最后结果的范围。

两张表（ xxxx\_test5和xxxx\_test）关联后只有8行记录，如果将订单表xxxx\_test和限定表先做关联，再和其他的一些订单信息表做连接，将会极大减少关联的行数，所以进一步改写SQL。

![改进SQL](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8316/155479955443592_zh-CN.png)

此时执行查询，只需要0.13s。

**总结**：由于环境迁移，导致SQL执行计划改变，这是导致RDS变慢的最终原因。

## 案例二 {#section_bsx_1hg_jhb .section}

**问题描述：** 使用RDS for SQL Server时经常报如下错误。

```
A network-related orinstance-specific error occurred while establishing a connection toSQL Server. The server was not found or was not accessible. Verifythat the instance name is correct and that SQL Server is configured toallow remote connections. (provider: SQL Network Interfaces, error:26 – Error Locating Server/Instance Specified)
```

**可能原因：**可能是用户的应用程序设计问题导致数据库锁争用较多，或者由于没有建立适当的索引导致全表扫描，造成了数据库等待。

**问题排查：**通过CloudDBA查看数据库的监控指标，发现在某个时间段有大量的全表扫描，同时数据库的锁等待超时，会话数明显增加。

![监控数据](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8316/155479955543614_zh-CN.png)

查看SQL Server内部的一些视图，来找到对应消耗资源top 5的SQL，发现用户频繁地查询一个视图，在视图中有多表连接，但在这些表连接中的字段上没有添加索引，导致了全表扫描，用户视图如下：

```
CREATE VIEW [dbo].[Vi_xxx]

AS

SELECT ..........

..........

FROM dbo.xxxx_test6 INNER JOIN

dbo.xxxx_test1 ON dbo.xxxx_test5.docID = dbo.xxxx_test1.docID

INNER JOIN

dbo.xxxx_test2 ON dbo.xxxx_test5.typeID = dbo.xxxx_test2.typeID

INNER JOIN

dbo.xxxx_test3 ON dbo.xxxx_test5.docID = dbo.xxxx_test3.docID

INNER JOIN

dbo.xxxx_test4 ON dbo.xxxx_test5.categoryID =

dbo.xxxx_test4.categoryID

WHERE (dbo.xxxx_test5.isDelete = 0)
```

通过查看执行计划，发现表上面很多的关联字段没有建立索引，导致全表扫描执行计划如下\(有很多的table scan\)。

![表扫描](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8316/155479955743615_zh-CN.png)

**总结**：用户频繁的查询一个视图，而该视图中表的关联字段上没有索引，导致了大量的全表扫描，累积了大量的会话数，造成数据库性能的下降，应用与数据库之间出现连接错误。

## 案例三 {#section_ulw_tjg_jhb .section}

**问题描述：**用户网站打开缓慢，质疑RDS性能不好。

**可能原因：**用户的数据存放在RDS中，网站访问数据库的时间较长，大多web应用程序设计，SQL没有优化或索引建立的不好导致。

**问题排查：**通过查看数据库的慢日志，发现大量的慢SQL，执行时间超过了2s。慢SQL如下：

```
UPDATE USER SET xx=xx+N.N WHEREaccount=130000870343 LIMIT 10SELECT * FROM USER WHERE account=13056870 LIMIT 10
```

检查user表是否建立索引：

```
CREATE TABLE `user` (

`id` smallint(5) unsigned NOT NULL AUTO_INCREMENT,

`account` char(11) NOT NULL COMMENT ‘???’,

…………………….

…………………….

PRIMARY KEY (`id`),

UNIQUE KEY `username` (`account`),

…………………….

) ENGINE=InnoDB CHARSET=utf8 ;
```

再查看执行计划，查询使用了全表扫描。检查发现account定义为字符串，而传入的条件为数字，由于数字的精度是比字符串高的，所以这里做了隐式转换。这样即使account上有索引，也无法使用，因此将传入的数字改为字符串后就能正常使用索引了。

**总结**：由于用户在设计表结构的时候字段定义使用了字符串，而传入的条件却传入了数字造成了隐式转换，这是数据库应用中经常出现的典型问题。

由上面的三个案例，可以总结一下，用户在使用RDS的时候，发现数据库执行SQL超时、性能较差、连接超时等等这些问题，除非实例不可用（主机down掉，实例服务停掉，实例由于存储空间过大而被锁定）而导致用户应用不可用（实例的故障RDS 会有监控报警），大多数情况是由于应用程序的设计，SQL没有优化，或者索引建立的不好而导致。

