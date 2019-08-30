# AliSQL功能概览 {#concept_1663672 .concept}

本文介绍AliSQL和其他版本的功能对比。

## AliSQL介绍 {#section_sm6_k9l_k48 .section}

AliSQL是阿里云深度定制的独立MySQL分支，除了社区版的所有功能外，AliSQL提供了类似于MySQL企业版的诸多功能，如企业级备份恢复、线程池、并行查询等，并且AliSQL还提供兼容Oracle的能力，如sequence引擎等。RDS for MySQL使用AliSQL内核，为用户提供了MySQL所有的功能，同时提供了企业级的安全、备份、恢复、监控、性能优化、只读实例等高级特性。

## 功能列表 {#section_z31_bjb_kr7 .section}

|分类|功能|社区版|官方企业版|AliSQL内核（5.7&8.0）|阿里云 RDS for MySQL|
|--|--|---|-----|-----------------|-----------------|
|企业增值服务|[24\*7 支持](https://www.aliyun.com/product/dbes)|未提供|√|√|√|
|[紧急故障救援](https://www.aliyun.com/product/dbes)|未提供|√|√|√|
|[专家服务顾问支持](https://www.aliyun.com/product/dbes)|未提供|√|√|√|
|MySQL Features|[MySQL Database Server](../../../../cn.zh-CN/RDS for MySQL 快速入门/创建RDS for MySQL实例.md#)|√|√|√|√|
|MySQL Document Store|√|√|MySQL 8.0支持|MySQL 8.0支持|
|MySQL Connectors|√|√|支持公开发行版|支持公开发行版|
|[MySQL Replication](cn.zh-CN/云数据库RDS简介/产品系列/产品系列概述.md#)|√|√|√|√|
|MySQL Router|√|√|MaxScale（MySQL 8.0支持）|数据库单租户代理|
|MySQL Partitioning|√|√|√|√|
|[Storage Engine](cn.zh-CN/云数据库RDS简介/什么是云数据库RDS.md#)| InnoDB

 MyISAM

 NDB

 | InnoDB

 MyISAM

 NDB

 | InnoDB

 X-Engine

 | InnoDB

 X-Engine

 |
|Oracle Compatibility|[Sequence Engine](cn.zh-CN/AliSQL内核/Sequence Engine.md#)|未提供|未提供|MySQL 8.0支持|MySQL 8.0支持|
|MySQL Enterprise Monitor|[Enterprise Dashboard](../../../../cn.zh-CN/RDS for MySQL 用户指南/监控与报警/查看资源和引擎监控.md#)|未提供|√|开发中|Enhanced Monitor|
|[Enterprise Advisors](../../../../cn.zh-CN/RDS for MySQL 用户指南/CloudDBA（新）/实时性能.md#)|未提供|√|开发中|CloudDBA|
|[Query Analyzer](../../../../cn.zh-CN/RDS for MySQL 用户指南/SQL审计与历史事件/SQL洞察.md#)|未提供|√|开发中|Performance Insight|
|[Replication Monitor](../../../../cn.zh-CN/RDS for MySQL 用户指南/监控与报警/查看资源和引擎监控.md#)|未提供|√|开发中|√|
|[Enhanced OS Metrics](../../../../cn.zh-CN/RDS for MySQL 用户指南/监控与报警/查看资源和引擎监控.md#)|未提供|未提供|未提供|Enhanced Monitor|
|MySQL Enterprise Backup|[Hot backup for InnoDB](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据库备份/备份MySQL数据.md#)|未提供|√|√|√|
|[Full, Incremental, Partial, Optimistic Backups](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据库恢复/MySQL单库单表恢复.md#)|未提供|√|√|库表级备份|
|[Full, Partial, Selective, Hot Selective restore](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据库恢复/MySQL单库单表恢复.md#)|未提供|√|√|库表级恢复|
|[Point-In-Time-Recovery](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据库恢复/恢复MySQL数据.md#)|未提供|√|√|√|
|[Cross-Region Backup](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据库备份/跨地域备份.md#)|未提供|未提供|未提供|跨地域备份|
|[Recycle bin](cn.zh-CN/AliSQL内核/Recycle Bin.md#)|未提供|未提供|MySQL 8.0支持|MySQL 8.0支持|
|[Flashback](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据库恢复/恢复MySQL数据.md#)|未提供|未提供|√|√|
|MySQL Enterprise Security|[Enterprise TDE](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置透明数据加密TDE.md#)|本地秘钥替换|√|BYOK TDE，Key Rotating|BYOK TDE，Key Rotating|
|[Enterprise Disk Data Encryption at Rest](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置透明数据加密TDE.md#)|未提供|未提供|未提供|BYOK 落盘加密|
|[Enterprise Encryption](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置SSL加密.md#)|SSL|√|SSL|SSL|
|[Enterprise Audit](../../../../cn.zh-CN/RDS for MySQL 用户指南/SQL审计与历史事件/SQL洞察.md#)|未提供|√|SQL洞察|SQL洞察|
|国内安全加密算法SM4|未提供|未提供|√|√|
|MySQL Enterprise Scalability|[Thread Pool](cn.zh-CN/AliSQL内核/Thread Pool.md#)|未提供|√|MySQL 8.0支持|MySQL 8.0支持|
|[Enterprise Readonly Request Extention](../../../../cn.zh-CN/RDS for MySQL 快速入门/扩展实例/只读实例/MySQL只读实例简介.md#)|未提供|未提供|√|只读实例|
|MySQL Enterprise Reliability|[Zero Data Loss](cn.zh-CN/云数据库RDS简介/产品系列/三节点企业版.md#)|未提供|未提供|√|三节点企业版|
|[SQL Outline](cn.zh-CN/AliSQL内核/Statement Outline.md#)|未提供|未提供|√|√|
|[Hot Massive Update](../../../../cn.zh-CN/RDS for MySQL 用户指南/实例管理/升级内核小版本.md#)|未提供|未提供|√|√|
|[Hot SQL Limit](cn.zh-CN/AliSQL内核/Statement Concurrency Control.md#)|未提供|未提供|√|√|
|[Hot SQL Firewall](cn.zh-CN/云数据库RDS简介/产品优势/高安全性.md#)|未提供|未提供|√|√|
|MySQL Enterprise High-Availability|[Enterprise Automatic Failover Switch](cn.zh-CN/云数据库RDS简介/产品优势/灾备设计.md#)|未提供|未提供|需要第三方HA机制|高可用版|
|[InnoDB Cluster](cn.zh-CN/云数据库RDS简介/产品系列/三节点企业版.md#)|√|√|√|三节点企业版|
|[Multi-Source Replication](../../../../cn.zh-CN/RDS for MySQL 快速入门/扩展实例/只读实例/MySQL只读实例简介.md#)|√|√|√|只读实例高可用|
|[Cross-Region Standby](../../../../cn.zh-CN/RDS for MySQL 快速入门/扩展实例/灾备实例.md#)|未提供|未提供|未提供|灾备实例|

## 版本支持情况 {#section_3bc_sfd_f6u .section}

|版本|功能|
|--|--|
|MySQL 8.0|[Performance Insight](cn.zh-CN/AliSQL内核/Performance Insight.md#)|
|[Recycle Bin](cn.zh-CN/AliSQL内核/Recycle Bin.md#)|
|[Sequence Engine](cn.zh-CN/AliSQL内核/Sequence Engine.md#)|
|[Statement Outline](cn.zh-CN/AliSQL内核/Statement Outline.md#)|
|[Statement Concurrency Control](cn.zh-CN/AliSQL内核/Statement Concurrency Control.md#)|
|[Thread Pool](cn.zh-CN/AliSQL内核/Thread Pool.md#)|
|[Purge Large File Asynchronously](cn.zh-CN/AliSQL内核/Purge Large File Asynchronously.md#)|
|[优化实例锁状态](cn.zh-CN/AliSQL内核/AliSQL Release Notes.md#section_qws_5xk_n2b)|
|MySQL 5.7|[合并官方5.7.26版本](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-26.html)|
|[优化实例锁状态](cn.zh-CN/AliSQL内核/AliSQL Release Notes.md#section_4d5_4iq_4a4)|
|MySQL 5.6|[优化实例锁状态](cn.zh-CN/AliSQL内核/AliSQL Release Notes.md#section_d3k_zxk_n2b)|

