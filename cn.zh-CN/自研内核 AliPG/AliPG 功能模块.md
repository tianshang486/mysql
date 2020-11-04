# AliPG 功能模块

本文介绍AliPG特有的功能模块，包括高权限账号、时空数据库、读写外部数据、并发控制等。

## 功能模块介绍

|类别|功能|描述|
|--|--|--|
|账号权限|[rds\_superuser](/cn.zh-CN/RDS PostgreSQL 数据库/账号/创建账号.md)|AliPG提供的rds\_superuser是介于普通用户和superuser之间的一种用户，对应的账号称为高权限账号。由于云上环境的安全原因，AliPG不直接提供superuser，但是提供rds\_superuser（主要裁剪了敏感安全权限）。rds\_superuser用户可以创建和删除插件、创建和删除普通用户以及高权限账号、操作和访问所有普通用户的表、终止连接等。|
|时空数据库|[Ganos时空引擎](/cn.zh-CN/时空数据库/简介.md)|阿里云自研Ganos时空引擎提供一系列的数据类型、函数和存储过程，用于对时间和空间数据进行高效存储、索引、查询和分析计算。|
|读写外部数据|[oss\_fdw](/cn.zh-CN/自研内核 AliPG/异构数据库访问/读写外部数据文本文件（oss_fdw）.md)|AliPG提供的oss\_fdw插件可以将OSS中的数据加载到数据库中，也可以将数据库中的数据写入OSS中，为您提供数据迁移、冷热数据分离功能。|
|并发控制|[pg\_concurrency\_control](/cn.zh-CN/自研内核 AliPG/并发控制（pg_concurrency_control）.md)|AliPG提供的pg\_concurrency\_control插件可以控制事务执行、SQL查询、存储过程和DML操作的并发，您可以自定义大查询，pg\_concurrency\_control提供对大查询的并发控制功能，优化高并发下的执行性能，使得高并发业务性能更平滑。|
|逻辑订阅故障转移|[Failover Slot](/cn.zh-CN/自研内核 AliPG/逻辑订阅故障转移（Failover Slot）.md)|社区版PostgreSQL的Logical Slot在主备切换时会导致逻辑订阅断开，AliPG对此进行优化，可以将所有的Logical Slot从主实例同步到备实例，避免逻辑订阅断开。|
|位图功能扩展|[varbitx](/cn.zh-CN/自研内核 AliPG/垂直行业/位图功能扩展（varbitx）.md)|社区版PostgreSQL内置的varbit插件支持的BIT类型操作函数比较简单，AliPG对其进行了扩展，支持更多的BIT操作，可以覆盖更多的应用场景，例如实时用户画像推荐系统、门禁广告系统、购票系统等。|
|向量检索|[PASE高效向量检索](/cn.zh-CN/自研内核 AliPG/垂直行业/高效向量检索（PASE）.md)|PASE（PostgreSQL ANN search extension）是一款为AliPG数据库研发的高性能向量检索索引插件，使用业界中成熟稳定且高效的ANN（Approximate nearest neighbor）检索算法，包括IVFFlat和HNSW算法，通过这两种算法，可以在AliPG数据库中实现极高速向量查询。PASE暂时不支持特征向量的抽取与产出，您需要自行检索实体的特征向量，PASE负责的工作是根据已产出的海量级别的向量进行相似向量的检索。|
|日志查询|[log\_fdw](/cn.zh-CN/自研内核 AliPG/异构数据库访问/查询日志（log_fdw）.md)|AliPG提供log\_fdw插件，可以直接通过外部表查询到日志内容。|
|可用性|[实例保护级别](/cn.zh-CN/RDS PostgreSQL 数据库/实例/设置实例保护级别.md)|设置实例的保护级别，提高云数据库可用性或性能。|
|安全|安全加固|AliPG内置安全加固模块，完善自定义视图，增强函数安全，防止安全陷阱，规避社区安全漏洞。|

## 相关文档

[支持插件列表](/cn.zh-CN/自研内核 AliPG/支持插件列表.md)

