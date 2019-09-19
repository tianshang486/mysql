# RDS for PPAS使用限制 {#concept_u5s_f4g_wdb .concept}

为保障实例的稳定及安全，云数据库PPAS有部分使用上的约束。

RDS for PPAS的使用限制详情如下表所示。

|操作|使用约束|
|--|----|
|修改数据库参数设置|暂不支持。|
|数据库的root权限|RDS无法向用户提供superuser权限。|
|数据库备份|只支持通过pg\_dump进行数据备份。|
|数据迁入|只支持通过psql还原由pg\_dump备份的数据。|
|搭建数据库复制| -   系统自动搭建了基于PPAS流复制的HA模式，无需用户手动搭建
-   PPAS Standby节点对用户不可见，不能直接用于访问。

 |
|重启RDS实例|必须通过控制台或API重启实例。|
|网络设置|若实例的[代理模式](../../../../cn.zh-CN/RDS for PPAS 用户指南/关闭数据库代理.md#)是高安全模式，禁止在SNAT模式下开启net.ipv4.tcp\_timestamps。|

