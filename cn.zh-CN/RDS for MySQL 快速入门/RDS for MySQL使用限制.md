# RDS for MySQL使用限制 {#concept_hb5_px2_vdb .concept}

为保障实例的稳定及安全，云数据库MySQL有部分使用上的约束。

RDS for MySQL的使用限制详情如下表所示。

|约束项|使用约束|
|---|----|
|实例参数|大部分实例参数可以使用控制台或API进行修改，同时出于安全和稳定性考虑，部分参数不支持修改，具体请参见[使用控制台设置参数](../../../../cn.zh-CN/用户指南/实例管理/设置实例参数/使用控制台设置参数.md#)。|
|数据库root权限|不提供root或者sa权限。|
|数据库备份| -   可使用命令行或图形界面进行逻辑备份。
-   仅限通过控制台或API进行物理备份。

 |
|数据库还原| -   可使用命令行或图形界面进行逻辑数据还原。
-   仅限通过控制台或API进行物理还原。

 |
|MySQL存储引擎|目前仅支持InnoDB引擎。 -   出于性能和安全性考虑，建议尽量采用InnoDB存储引擎。
-   不支持TokuDB引擎。由于Percona已经不再对TokuDB提供支持，很多已知BUG无法修正，极端情况下会导致业务受损，因此RDS for MySQL在2019年8月1日后将不再支持TokuDB引擎。引擎转换请参见[【通知】TokuDB引擎转换为InnoDB引擎](../../../../cn.zh-CN/云数据库RDS简介/【通知】TokuDB引擎转换为InnoDB引擎.md#)。
-   不支持MyISAM引擎。由于MyISAM引擎的自身缺陷，存在数据丢失的风险，实例的MyISAM引擎表会自动转换为InnoDB引擎表。详情请参见文档[为什么 RDS for MySQL 不支持 MyISAM 引擎？](../../../../cn.zh-CN/RDS for MySQL 用户指南/MySQL FAQ/为什么 RDS for MySQL 不支持 MyISAM 引擎？.md#)。
-   不支持Memory引擎。Memory引擎的表将会自动转换成InnoDB引擎的表。

 |
|数据库复制|RDS for MySQL提供主备复制架构，其中的备（slave）实例不对用户开放，用户应用不能直接访问。|
|实例重启|必须通过控制台或API重启实例。|
|网络设置|若MySQL 5.5或MySQL 5.6实例位于经典网络且开启了数据库代理，禁止在SNAT模式下开启net.ipv4.tcp\_timestamps。|
|空间存储| 若存储空间使用率过高，为防止用户误操作导致数据丢失，将会锁定实例，具体原因及解决办法请参见文档[MySQL 实例空间使用率过高的原因和解决方法](https://help.aliyun.com/knowledge_detail/51682.html)。

 |
|监控报警|MySQL 5.7高可用云盘实例暂不支持[报警](../../../../cn.zh-CN/RDS for MySQL 用户指南/监控与报警/设置报警规则.md#)功能。|

