# PostgreSQL CloudDBA简介 {#concept_wpx_tqn_wdb .concept}

PostgreSQL CloudDBA是监控和管理RDS实例性能及运行状况的服务，针对SQL语句的性能、CPU使用率、IOPS使用率、内存使用率、磁盘空间使用率、连接数、锁信息、热点表等，CloudDBA提供了智能的诊断及优化功能，能最大限度发现数据库存在的或潜在的健康问题。CloudDBA的诊断基于单个实例，该诊断会提供问题详情及相应的解决方案，可为您管理实例运行状况带来极大的便利。

## 功能介绍 {#section_h5s_wqn_wdb .section}

PostgreSQL CloudDBA主要包含如下功能：

-   智能优化：提供实例性能监控和综合评分的概况，主要如下4个部分构成。

    -   实例基本信息：CloudDBA所监控和诊断的实例ID、类型、所在地域、可用区、链路类型等。

    -   [查看实例运行状况](cn.zh-CN/RDS for PostgreSQL 用户指南/性能优化__诊断（CloudDBA）/智能优化/查看实例运行状况.md#)：提供了连接、QPS、表扫描、索引扫描和临时文件的监控图，该数据每5秒刷新一次，如下图所示（本文图示仅为示例，请以实际界面为准）。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62233/156687682533833_zh-CN.png)

    -   实例核心资源使用率：显示了实例当前CPU、内存、连接数、IOPS和磁盘空间的使用率，该数据每20秒刷新一次，如下图所示（本文图示仅为示例，请以实际界面为准）。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62233/156687682733835_zh-CN.png)

    -   [诊断实例性能](cn.zh-CN/RDS for PostgreSQL 用户指南/性能优化__诊断（CloudDBA）/智能优化/诊断实例性能.md#)：显示实例性能的诊断评分和诊断结果。系统不会自动进行诊断，您需要手动进行一键诊断，如下图所示（本文图示仅为示例，请以实际界面为准）。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7899/15668768273053_zh-CN.png)

-   问题诊断：提供实例诊断详情，包括CPU、空间和诊断历史，详情如下所示。

    -   [查询和终止实时会话](cn.zh-CN/RDS for PostgreSQL 用户指南/性能优化__诊断（CloudDBA）/问题诊断/查询和终止实时会话.md#)：显示CPU、内存的使用状态，以及当前实例的实时会话列表。另外，您还可以终止会话并查询过滤历史。

    -   [查看空间使用详情](cn.zh-CN/RDS for PostgreSQL 用户指南/性能优化__诊断（CloudDBA）/问题诊断/查看空间使用详情.md#)：显示当前实例数据空间和日志空间的使用状态，以及数据库中所有表的详情。

    -   [查看诊断历史](cn.zh-CN/RDS for PostgreSQL 用户指南/性能优化__诊断（CloudDBA）/问题诊断/查看诊断历史.md#)：您可以查看所有类型的诊断历史及诊断详情。

-   SQL优化：系统可以根据您输入的SQL语句给出诊断优化意见。

-   [查看实例性能诊断报告](cn.zh-CN/RDS for PostgreSQL 用户指南/性能优化__诊断（CloudDBA）/查看实例性能诊断报告.md#)：您可以创建、查看实例的诊断报告。诊断报告生成时间大约需要10分钟左右，诊断报告列表中可显示最近30天内的报告数据。

-   [性能洞察](cn.zh-CN/RDS for PostgreSQL 用户指南/性能优化__诊断（CloudDBA）/性能洞察.md#)：专注于RDS实例负载监控、关联分析、性能调优的利器，以简单直观的方式帮助您迅速评估数据库负载，找到性能问题的源头，提升数据库的稳定性。

