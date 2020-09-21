# 云数据库 RDS 快速入门

如果您初次使用阿里云关系型数据库RDS，请参见快速入门系列文档，帮助您快速上手RDS。

-   [MySQL快速入门](/cn.zh-CN/RDS MySQL 数据库/快速入门/创建RDS MySQL实例.md)
-   [SQL Server快速入门](/cn.zh-CN/RDS SQL Server 数据库/快速入门/创建RDS SQL Server实例.md)
-   [PostgreSQL快速入门](/cn.zh-CN/RDS PostgreSQL 数据库/快速入门/创建RDS PostgreSQL实例.md)
-   [PPAS快速入门](/cn.zh-CN/RDS PPAS 数据库/快速入门/创建RDS PPAS实例.md)
-   [MariaDB快速入门](/cn.zh-CN/RDS MariaDB TX 数据库/快速入门/创建RDS MariaDB实例.md)

## 数据库引擎

以下是对五种数据库引擎的介绍：

-   云数据库RDS MySQL

    MySQL是全球最受欢迎的开源数据库，作为开源软件组合LAMP（Linux + Apache + MySQL + Perl/PHP/Python）中的重要一环，广泛应用于各类应用。

    Web 2.0时代，风靡全网的社区论坛软件系统Discuz!和博客平台WordPress均基于MySQL实现底层架构。Web 3.0时代，阿里巴巴、Facebook、Google等大型互联网公司都采用更为灵活的MySQL构建了成熟的大规模数据库集群。

    阿里云数据库RDS MySQL基于阿里巴巴的MySQL源码分支，经过双11高并发、大数据量的考验，拥有优良的性能和吞吐量。此外，阿里云数据库MySQL版还拥有经过优化的[读写分离](/cn.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/读写分离.md)、[数据库独享代理](/cn.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/数据库独享代理.md)、[智能调优](/cn.zh-CN/RDS MySQL 数据库/性能优化与诊断（自治服务）/自治服务DAS简介.md)等高级功能。

    当前RDS MySQL支持5.5、5.6、5.7和8.0版本。

-   云数据库RDS SQL Server

    SQL Server是发行最早的商用数据库产品之一，作为Windows平台（IIS + .NET + SQL Server）中的重要一环，支撑着大量的企业应用。SQL Server自带的Management Studio管理软件内置了大量图形工具和丰富的脚本编辑器。您通过可视化界面即可快速上手各种数据库操作。

    阿里云数据库RDS SQL Server不仅拥有高可用架构和任意时间点的[数据恢复](/cn.zh-CN/RDS SQL Server 数据库/恢复/恢复SQL Server数据.md)功能，强力支撑各种企业应用，同时也包含了微软的License费用，您无需再额外支出License费用。

    当前RDS SQL Server支持以下版本：

    -   SQL Server 2008 R2 企业版
    -   SQL Server 2012 Web版、标准版、企业版
    -   SQL Server 2014标准版
    -   SQL Server 2016 Web版、标准版、企业版
    -   SQL Server 2017 标准版、集群版
    -   SQL Server 2019 标准版
-   云数据库RDS PostgreSQL

    PostgreSQL是全球最先进的开源数据库。作为学院派关系型数据库管理系统的鼻祖，它的优点主要集中在对SQL规范的完整实现以及丰富多样的数据类型支持，包括JSON数据、IP数据和几何数据等，而大部分商业数据库都不支持这些数据类型。

    除了完美支持事务、子查询、多版本控制（MVCC）、数据完整性检查等特性外，阿里云数据库RDS PostgreSQL还集成了高可用和备份恢复等重要功能，减轻您的运维压力。

    当前RDS PostgreSQL支持9.4、10、11和12版本。

-   云数据库RDS PPAS

    PPAS（Postgres Plus Advanced Server）是稳定、安全且可扩展的企业级关系型数据库，基于PostgreSQL，并在性能、应用方案和兼容性等方面进行了增强，提供直接运行Oracle应用的能力。您可以在PPAS上稳定运行各种企业应用，同时得到高性价比的服务。

    阿里云数据库RDS PPAS集成了账号管理、资源监控、备份恢复和安全控制等功能，并将持续地更新完善。

    当前RDS PPAS支持9.3和10版本。

-   云数据库RDS MariaDB TX

    MariaDB是MySQL的一个分支，主要由开源社区维护，采用GPL授权许可。MariaDB的目的是完全兼容MySQL，包括API和命令行，使之能轻松成为MySQL的代替品。在存储引擎方面，MariaDB 10.0.9版起使用XtraDB（代号为Aria）来代替MySQL的InnoDB。

    阿里云引入的MariaDB TX企业级解决方案，良好兼容Oracle，对PL/SQL有优秀的兼容性。MariaDB TX是一个建立在 MariaDB Server、MariaDB MaxScale和MariaDB Cluster之上的事务性数据库平台，包括数据库连接器和管理工具，提供技术支持以及专家服务——创建了完整的企业数据库解决方案。

    当前RDS MariaDB TX支持10.3版本。


