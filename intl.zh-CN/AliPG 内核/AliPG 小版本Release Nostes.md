# AliPG 小版本Release Nostes

本文介绍AliPG的内核版本更新说明。

## PostgreSQL 12

20200830

-   新特性
    -   [ganos](/intl.zh-CN/时空数据库/简介.md)插件升级到3.0版本。
    -   支持[SQL防火墙](/intl.zh-CN/AliPG 内核/SQL防火墙（sql_firewall插件）.md)插件，用于防止恶意SQL注入。
    -   支持[bigm](/intl.zh-CN/AliPG 内核/文本搜索与模糊查询（pg_bigm插件）.md)插件，用于模糊查询。
    -   支持[TimescaleDB](/intl.zh-CN/AliPG 内核/垂直行业/使用TimescaleDB插件.md)插件，用于时序数据处理。
-   Bug修复
    -   修复一个`rds_`前缀后台参数不识别的错误。
    -   修复pg\_cron插件无法正常创建使用的错误。
    -   打包了RDKit插件的若干依赖，修复缺少依赖无法载入的错误。

20200421

-   新特性
    -   内核升级到兼容社区12.2版本。
    -   [ganos](/intl.zh-CN/时空数据库/简介.md)插件升级到2.7版本。
    -   新增[hll](/intl.zh-CN/AliPG 内核/近似计算（hll插件）.md)插件2.14版本。
    -   新增[plproxy](/intl.zh-CN/AliPG 内核/分片代理（PL/Proxy插件）.md)插件2.9.0版本。
    -   新增tsm\_system\_rows插件1.0版本。
    -   新增tsm\_system\_time插件1.0版本。
    -   新增[smlar](/intl.zh-CN/AliPG 内核/垂直行业/使用smlar插件.md)插件1.0版本。
    -   新增[tds\_fdw](/intl.zh-CN/AliPG 内核/异构数据库访问/使用tds_fdw插件.md)插件1.0版本。
-   Bug修复

    修复逻辑订阅超时导致的实例重启问题。


20200221

-   新特性
    -   支持为rds\_superuser角色预留指定连接数，以便连接数不足时可以连接实例排查故障。
    -   支持[wal2json](/intl.zh-CN/AliPG 内核/逻辑数据同步（wal2json插件）.md)插件。
    -   升级[ganos](/intl.zh-CN/时空数据库/简介.md)插件到2.6版本。
-   Bug修复

    修复部分权限问题。


20191230

新特性

-   支持[pg\_roaringbitmap](/intl.zh-CN/AliPG 内核/垂直行业/使用roaringbitmap插件.md)、rdkit、[mysql\_fdw](/intl.zh-CN/AliPG 内核/异构数据库访问/使用mysql_fdw插件读写MySQL数据.md)、ganos插件。
-   支持用户高权限账号一次发布所有表和创建订阅。

## PostgreSQL 11

20200830

-   新特性
    -   [ganos](/intl.zh-CN/时空数据库/简介.md)插件升级到3.0版本。
    -   支持[SQL防火墙](/intl.zh-CN/AliPG 内核/SQL防火墙（sql_firewall插件）.md)插件，用于防止恶意SQL注入。
    -   支持[bigm](/intl.zh-CN/AliPG 内核/文本搜索与模糊查询（pg_bigm插件）.md)插件，用于模糊查询。
    -   支持[ZomboDB](/intl.zh-CN/AliPG 内核/Elasticsearch索引接口（ZomboDB插件）.md)插件，用于文本搜索和分析。
-   Bug修复
    -   修复一个`rds_`前缀后台参数不识别的错误。
    -   修复Failover Slot同名流复制槽导致备库崩溃的错误
    -   修复pg\_cron插件无法正常创建使用的错误。
    -   修复PASE插件一个全局变量引起的正确性错误。

20200610

新特性

-   支持[timescaledb](/intl.zh-CN/AliPG 内核/垂直行业/使用TimescaleDB插件.md)插件1.7.1版本。
-   支持rds\_superuser使用插件pageinspect。
-   支持rds\_superuser赋予其他用户replication权限。

20200511

-   新特性

    [ganos](/intl.zh-CN/时空数据库/简介.md)插件升级到2.8版本。

-   Bug修复

    PASE插件解决HNSW索引执行insert操作慢的问题。


20200421

新特性

-   支持[逻辑订阅故障转移（Failover Slot）](/intl.zh-CN/AliPG 内核/逻辑订阅故障转移（Failover Slot）.md)功能。
-   新增[plproxy](/intl.zh-CN/AliPG 内核/分片代理（PL/Proxy插件）.md)插件2.9.0版本。
-   新增tsm\_system\_rows插件1.0版本。
-   新增tsm\_system\_time插件1.0版本。
-   新增[smlar](/intl.zh-CN/AliPG 内核/垂直行业/使用smlar插件.md)插件1.0版本。

20200402

-   新特性
    -   支持[hll](/intl.zh-CN/AliPG 内核/近似计算（hll插件）.md)插件（2.14版本），增hll数据类型，毫秒级别响应，近似数据分析业务，例如实时PV、UV查询，或者特征标签contain判定，低成本、高效率，解决近似分析的问题。
    -   支持[oss\_fdw](/intl.zh-CN/AliPG 内核/异构数据库访问/使用oss_fdw读写外部数据文本文件.md)插件（1.1版本），可用于数据库OSS扩展存储，您可以将查询量少的历史数据存储在OSS，降低存储成本，同时满足低频的查询需求。
    -   支持[tds\_fdw](/intl.zh-CN/AliPG 内核/异构数据库访问/使用tds_fdw插件.md)插件（2.0.1版本），不需要etl程序，即可在PostgreSQL数据库中实时查询Sybase、SQL Server数据，满足多数据库种类跨库查询、迁移数据的需求。
-   插件升级
    -   [ganos](/intl.zh-CN/时空数据库/简介.md)升级到2.7版本。
    -   [wal2json](/intl.zh-CN/AliPG 内核/逻辑数据同步（wal2json插件）.md)升级2.2版本。
-   性能优化

    `shutdown -m fast`命令优化。


20191218

新特性

-   支持[PASE索引插件](/intl.zh-CN/AliPG 内核/垂直行业/使用PASE插件.md)，提供图像识别索引。
-   支持用户高权限账号一次发布所有表和创建订阅。

## PostgreSQL 10

20200830

-   新特性
    -   [ganos](/intl.zh-CN/时空数据库/简介.md)插件升级到3.0版本。
    -   支持[SQL防火墙](/intl.zh-CN/AliPG 内核/SQL防火墙（sql_firewall插件）.md)插件，用于防止恶意SQL注入。
    -   支持[bigm](/intl.zh-CN/AliPG 内核/文本搜索与模糊查询（pg_bigm插件）.md)插件，用于模糊查询。
-   Bug修复

    修复pg\_cron插件无法正常创建使用的错误。


20200212

-   新特性
    -   支持为rds\_superuser角色预留指定连接数，以便连接数不足时可以连接实例排查故障。
    -   升级[ganos](/intl.zh-CN/时空数据库/简介.md)插件到2.6版本。
-   Bug修复

    修复流复制中等待时间长的问题。


20190703

-   新特性
    -   版本更新为10.9。
    -   支持在超时时将同步复制更改为异步复制。
-   Bug修复
    -   修复make pg\_hint\_plan错误问题。
    -   修复外部rum失败问题。

## PostgreSQL 9.4

20200623

-   新特性
    -   [wal2json](/intl.zh-CN/AliPG 内核/逻辑数据同步（wal2json插件）.md)升级2.2版本。
    -   支持xml2插件1.0版本。
-   Bug修复

    修复使用wal2json插件导致内存耗尽的问题。


20200210

支持为rds\_superuser角色预留指定连接数，以便连接数不足时可以连接实例排查故障。

20190601

版本更新为9.4.19。

