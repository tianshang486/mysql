# RDS for PostgreSQL使用限制 {#concept_zvw_n1g_wdb .concept}

为保障实例的稳定及安全，云数据库PostgreSQL有部分使用上的约束。

RDS for PostgreSQL的使用限制详情如下表所示。

|操作|RDS 使用约束|
|--|--------|
|数据库的root权限|RDS无法向用户提供superuser权限。|
|数据库备份|只支持通过pg\_dump进行数据备份。|
|搭建数据库复制|系统自动搭建了基于PostgreSQL流复制的HA模式，无需用户手动搭建。PostgreSQL Standby节点对用户不可见，不能直接用于访问。|
|重启RDS实例|必须通过控制台或OpenAPI操作重启实例。|
|网络设置|若实例的[代理模式](../../../../cn.zh-CN/RDS for PostgreSQL 用户指南/关闭数据库代理模式.md#)是高安全模式，禁止在SNAT模式下开启net.ipv4.tcp\_timestamps。|
|创建实例| -   如果要创建PostgreSQL 10高可用版（本地盘）、PostgreSQL 10基础版和PostgreSQL 9.4，请使用[RDS控制台](https://rds.console.aliyun.com/?spm=5176.doc43185.2.7.mR2Syx)。
-   如果要创建PostgreSQL 11高可用版（云盘）、PostgreSQL 10高可用版（云盘），请使用[新版PostgreSQL控制台](https://postgresql.console.aliyun.com/)。

 |

