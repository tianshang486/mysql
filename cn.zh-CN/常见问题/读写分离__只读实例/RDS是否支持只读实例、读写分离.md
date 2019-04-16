# RDS是否支持只读实例、读写分离 {#concept_185108 .concept}

## 只读实例 {#section_eol_6op_itv .section}

部分RDS产品已经推出只读实例功能，实现读取能力的弹性扩展，分担数据库压力。详情请参见：

-   [MySQL只读实例简介](../../../../cn.zh-CN/RDS for MySQL 快速入门/扩展实例/只读实例/MySQL只读实例简介.md#)
-   [SQL Server只读实例简介](../../../../cn.zh-CN/RDS for SQL Server 快速入门/只读实例/SQL Server只读实例简介.md#)
-   [PostgreSQL只读实例简介](../../../../cn.zh-CN/RDS for PostgreSQL 快速入门/只读实例/PostgreSQL只读实例简介.md#)
-   [PPAS只读实例简介](../../../../cn.zh-CN/RDS for PPAS 快速入门/只读实例/PPAS只读实例简介.md#)

## 读写分离 {#section_2aw_q50_y5q .section}

MySQL、SQL Server目前已经推出读写分离功能，您不需要自己做读写分离，只要主实例下有只读实例以及开通读写分离功能，使用生成的读写分离地址即可。详情请参见：

-   [MySQL读写分离简介](../../../../cn.zh-CN/RDS for MySQL 用户指南/只读实例与读写分离/读写分离简介.md#)
-   [SQL Server读写分离简介](../../../../cn.zh-CN/RDS for SQL Server 用户指南/SQL Server读写分离/读写分离简介.md#)

**说明：** RDS产品是主备架构，但是备库不支持读写请求，只用于高可用服务。

