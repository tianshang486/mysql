# AliSQL 功能概览

本文介绍AliSQL和其他版本的功能对比。

## AliSQL介绍

AliSQL是阿里云深度定制的独立MySQL分支，除了社区版的所有功能外，AliSQL提供了类似于MySQL企业版的诸多功能，如企业级备份恢复、线程池、并行查询等，并且AliSQL还提供兼容Oracle的能力，如sequence引擎等。RDS MySQL使用AliSQL内核，为用户提供了MySQL所有的功能，同时提供了企业级的安全、备份、恢复、监控、性能优化、只读实例等高级特性。

## 版本支持情况

|类别|功能|描述|MySQL 8.0|MySQL 5.7|MySQL 5.6|
|--|--|--|---------|---------|---------|
|功能|[Thread Pool](/intl.zh-CN/自研内核 AliSQL/功能/Thread Pool.md)|提供线程池（Thread Pool）功能，将线程和会话分离，在拥有大量会话的同时，只需要少量线程完成活跃会话的任务即可。|支持|支持|支持|
|[Statement Outline](/intl.zh-CN/自研内核 AliSQL/功能/Statement Outline.md)|利用Optimizer Hint和Index Hint让MySQL稳定执行计划，该方法称为Statement Outline，并提供了工具包（DBMS\_OUTLN）便于您快捷使用。|支持|支持|不支持|
|[Sequence Engine](/intl.zh-CN/自研内核 AliSQL/功能/Sequence Engine.md)|提供Sequence Engine，简化获取序列值的复杂度。|支持|不支持|支持|
|[Returning](/intl.zh-CN/自研内核 AliSQL/功能/Returning.md)|支持DML语句返回Resultset，同时提供了工具包（DBMS\_TRANS）便于您快捷使用。|支持|不支持|不支持|
|性能|[Fast Query Cache](/intl.zh-CN/自研内核 AliSQL/性能/Fast Query Cache.md)|针对原生MySQL Query Cache的不足，阿里云进行重新设计和全新实现，推出Fast Query Cache，能够有效提高数据库查询性能。|不支持|支持|不支持|
|[Binlog in Redo](/intl.zh-CN/自研内核 AliSQL/性能/Binlog in Redo.md)|在事务提交时将Binlog内容同步写入到Redo Log中，减少对磁盘的操作，提高数据库性能。|支持|不支持|不支持|
|[Statement Queue](/intl.zh-CN/自研内核 AliSQL/性能/Statement Queue.md)|针对语句的排队机制，将语句进行分桶排队，尽量把可能具有相同冲突的语句（例如操作相同行）放在一个桶内排队，减少冲突的开销。|支持|支持|不支持|
|[Inventory Hint](/intl.zh-CN/自研内核 AliSQL/性能/Inventory Hint.md)|快速提交、回滚事务，配合Returning和Statement Queue，能有效提高业务吞吐能力。|支持|支持|支持|
|稳定|[Faster DDL](/intl.zh-CN/自研内核 AliSQL/稳定/Faster DDL.md)|优化DDL操作过程中的Buffer Pool管理机制，降低DDL操作带来的性能影响，提升在线DDL操作的并发数。|支持|支持|支持|
|[Statement Concurrency Control](/intl.zh-CN/自研内核 AliSQL/稳定/Statement Concurrency Control.md)|提供基于语句规则的并发控制CCL（Concurrency Control），并提供了工具包（DBMS\_CCL）便于您快捷使用。|支持|支持|不支持|
|[Performance Agent](/intl.zh-CN/自研内核 AliSQL/稳定/Performance Agent.md)|便捷的性能数据统计方案。通过MySQL插件的方式，实现MySQL实例内部各项性能数据的采集与统计。|支持|支持|支持|
|[Purge Large File Asynchronously](/intl.zh-CN/自研内核 AliSQL/稳定/Purge Large File Asynchronously.md)|通过异步删除大文件的方式保证系统稳定性。|支持|支持|支持|
|[Performance Insight](/intl.zh-CN/自研内核 AliSQL/稳定/Performance Insight.md)|是专注于实例负载监控、关联分析、性能调优的利器，帮助您迅速评估数据库负载，找到性能问题的源头，提升数据库的稳定性。|支持|支持|不支持|
|安全|[Data Protect](/intl.zh-CN/自研内核 AliSQL/安全/Data Protect.md)|提供数据保护功能，通过控制高危险的删除操作的权限，实现数据保护。|支持|支持|支持|
|[Recycle Bin](/intl.zh-CN/自研内核 AliSQL/安全/Recycle Bin.md)|支持回收站（Recycle Bin）功能，临时将删除的表转移到回收站，还可以设置保留的时间，方便您找回数据，同时提供了工具包（DBMS\_RECYCLE）便于您快捷使用。|支持|不支持|不支持|

## 功能列表

|分类|功能|社区版|官方企业版|AliSQL内核（5.7&8.0）|阿里云 RDS MySQL|
|--|--|---|-----|-----------------|-------------|
|企业增值服务|[24\*7 支持](https://www.alibabacloud.com/zh/services/list)|未提供|√|√|√|
|[紧急故障救援](https://www.alibabacloud.com/zh/services/list)|未提供|√|√|√|
|[专家服务顾问支持](https://www.alibabacloud.com/zh/services/list)|未提供|√|√|√|
|MySQL Features|[MySQL Database Server](/intl.zh-CN/RDS MySQL 数据库/快速入门/创建RDS MySQL实例.md)|√|√|√|√|
|MySQL Document Store|√|√|MySQL 8.0支持|MySQL 8.0支持|
|MySQL Connectors|√|√|支持公开发行版|支持公开发行版|
|MySQL Replication|√|√|√|√|
|MySQL Router|√|√|MaxScale（MySQL 8.0支持）|数据库单租户代理|
|MySQL Partitioning|√|√|√|√|
|[Storage Engine](/intl.zh-CN/自研内核 AliSQL/X-Engine引擎/X-Engine简介.md)|InnoDB

MyISAM

NDB

|InnoDB

MyISAM

NDB

|InnoDB

X-Engine

|InnoDB

X-Engine |
|Oracle Compatibility|[Sequence Engine](/intl.zh-CN/自研内核 AliSQL/功能/Sequence Engine.md)|未提供|未提供|MySQL 8.0支持|MySQL 8.0支持|
|MySQL Enterprise Monitor|[Enterprise Dashboard](/intl.zh-CN/RDS MySQL 数据库/监控与报警/查看资源和引擎监控.md)|未提供|√|开发中|Enhanced Monitor|
|[Query Analyzer](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/SQL洞察.md)|未提供|√|开发中|Performance Insight|
|[Replication Monitor](/intl.zh-CN/RDS MySQL 数据库/监控与报警/查看资源和引擎监控.md)|未提供|√|开发中|√|
|[Enhanced OS Metrics](/intl.zh-CN/RDS MySQL 数据库/监控与报警/查看资源和引擎监控.md)|未提供|未提供|未提供|Enhanced Monitor|
|MySQL Enterprise Backup|[Hot backup for InnoDB](/intl.zh-CN/RDS MySQL 数据库/备份/备份MySQL数据.md)|未提供|√|√|√|
|[Full, Incremental, Partial, Optimistic Backups](/intl.zh-CN/RDS MySQL 数据库/恢复/MySQL单库单表恢复.md)|未提供|√|√|库表级备份|
|[Full, Partial, Selective, Hot Selective restore](/intl.zh-CN/RDS MySQL 数据库/恢复/MySQL单库单表恢复.md)|未提供|√|√|库表级恢复|
|[Point-In-Time-Recovery](/intl.zh-CN/RDS MySQL 数据库/恢复/恢复MySQL数据.md)|未提供|√|√|√|
|[Cross-Region Backup](/intl.zh-CN/RDS MySQL 数据库/备份/跨地域备份数据.md)|未提供|未提供|未提供|跨地域备份|
|[Recycle bin](/intl.zh-CN/自研内核 AliSQL/安全/Recycle Bin.md)|未提供|未提供|MySQL 8.0支持|MySQL 8.0支持|
|[Flashback](/intl.zh-CN/RDS MySQL 数据库/恢复/恢复MySQL数据.md)|未提供|未提供|√|√|
|MySQL Enterprise Security|[Enterprise TDE](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/设置透明数据加密TDE.md)|本地密钥替换|√|BYOK TDE，Key Rotating|BYOK TDE，Key Rotating|
|[Enterprise Disk Data Encryption at Rest](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/设置透明数据加密TDE.md)|未提供|未提供|未提供|BYOK 落盘加密|
|[Enterprise Encryption](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/设置SSL加密.md)|SSL|√|SSL|SSL|
|[SQL Explorer](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/SQL洞察.md)|未提供|√|SQL洞察|SQL洞察|
|安全加密算法SM4|未提供|未提供|√|√|
|MySQL Enterprise Scalability|[Thread Pool](/intl.zh-CN/自研内核 AliSQL/功能/Thread Pool.md)|未提供|√|MySQL 8.0支持|MySQL 8.0支持|
|[Enterprise Readonly Request Extention](/intl.zh-CN/RDS MySQL 数据库/只读实例/MySQL只读实例简介.md)|未提供|未提供|√|只读实例|
|MySQL Enterprise Reliability|[Statement Outline](/intl.zh-CN/自研内核 AliSQL/功能/Statement Outline.md)|未提供|未提供|√|√|
|[Inventory Hint](/intl.zh-CN/自研内核 AliSQL/性能/Inventory Hint.md)|未提供|未提供|√|√|
|[Statement Concurrency Control](/intl.zh-CN/自研内核 AliSQL/稳定/Statement Concurrency Control.md)|未提供|未提供|√|√|
|[Hot SQL Firewall](/intl.zh-CN/云数据库 RDS 简介/为什么选择RDS/高安全性.md)|未提供|未提供|√|√|
|MySQL Enterprise High-Availability|[Enterprise Automatic Failover Switch](/intl.zh-CN/云数据库 RDS 简介/为什么选择RDS/高可用和容灾设计.md)|未提供|未提供|需要第三方HA机制|高可用版|
|[Multi-Source Replication](/intl.zh-CN/RDS MySQL 数据库/只读实例/MySQL只读实例简介.md)|√|√|√|只读实例高可用|

