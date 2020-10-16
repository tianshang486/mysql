# PostgreSQL功能概览

本文介绍RDS PostgreSQL各版本、系列、存储类型支持的功能，便于您根据自身需要选购实例或查询已购实例功能。

|类别|功能|PostgreSQL 12|
|高可用版|基础版|
|SSD云盘|ESSD/ESSD PL2/ESSD PL3云盘|SSD云盘|ESSD/ESSD PL2/ESSD PL3云盘|
|--|--|-------------|
|----|---|
|-----|------------------------|-----|------------------------|
|数据迁移同步|[数据迁移同步](https://www.alibabacloud.com/help/zh/doc-detail/125233.htm)|√|√|√|√|
|实例管理|[创建实例](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/创建RDS PostgreSQL实例.md)|√|√|√|√|
|[变更配置](/intl.zh-CN/RDS PostgreSQL 数据库/实例/变更配置.md)|√|√|√|√|
|[设置实例参数](/intl.zh-CN/RDS PostgreSQL 数据库/实例/设置实例参数.md)|√|√|√|√|
|[设置实例保护级别](/intl.zh-CN/RDS PostgreSQL 数据库/实例/设置实例保护级别.md)|√|√|×|×|
|[迁移可用区](/intl.zh-CN/RDS PostgreSQL 数据库/实例/迁移可用区.md)|×|×|×|×|
|[切换主备实例](/intl.zh-CN/RDS PostgreSQL 数据库/实例/自动或手动主备切换.md)|√|√|×|×|
|[重启实例](/intl.zh-CN/RDS PostgreSQL 数据库/实例/重启实例.md)|√|√|√|√|
|[设置可维护时间段](/intl.zh-CN/RDS PostgreSQL 数据库/实例/设置可维护时间段.md)|√|√|√|√|
|[释放实例](/intl.zh-CN/RDS PostgreSQL 数据库/实例/释放实例.md)|√|√|√|√|
|[实例回收站](/intl.zh-CN/RDS PostgreSQL 数据库/实例/实例回收站.md)|√|√|√|√|
|账号管理|[创建账号](/intl.zh-CN/RDS PostgreSQL 数据库/账号/创建账号.md)|√|√|√|√|
|[重置密码](/intl.zh-CN/RDS PostgreSQL 数据库/账号/重置密码.md)|√|√|√|√|
|[锁定账号](/intl.zh-CN/RDS PostgreSQL 数据库/账号/锁定/删除账号.md)|√|√|√|√|
|[删除账号](/intl.zh-CN/RDS PostgreSQL 数据库/账号/锁定/删除账号.md)|√|√|√|√|
|数据库管理|[创建数据库](/intl.zh-CN/RDS PostgreSQL 数据库/数据库/创建数据库.md)|√|√|√|√|
|[删除数据库](/intl.zh-CN/RDS PostgreSQL 数据库/数据库/删除数据库.md)|√|√|√|√|
|[插件](/intl.zh-CN/自研内核 AliPG/支持插件列表.md)|√|√|√|√|
|数据库连接|[连接PostgreSQL实例](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/连接PostgreSQL实例.md)|√|√|√|√|
|[设置连接地址]()|√|√|√|√|
|[查看连接地址/端口](/intl.zh-CN/RDS PostgreSQL 数据库/数据库连接/查看或修改内外网地址和端口.md)|√|√|√|√|
|[申请或释放外网地址](/intl.zh-CN/RDS PostgreSQL 数据库/数据库连接/申请或释放外网地址.md)|√|√|√|√|
|监控报警|[查看资源和引擎监控](/intl.zh-CN/RDS PostgreSQL 数据库/监控与报警/查看资源和引擎监控.md)|√|√|√|√|
|[设置监控频率](/intl.zh-CN/RDS PostgreSQL 数据库/监控与报警/设置监控频率.md)|√|√|√|√|
|[设置报警规则](/intl.zh-CN/RDS PostgreSQL 数据库/监控与报警/设置报警规则.md)|×|×|×|×|
|网络管理|[切换网络类型](/intl.zh-CN/RDS PostgreSQL 数据库/网络/VPC/交换机/切换网络类型.md)|×|×|×|×|
|[切换虚拟交换机](/intl.zh-CN/RDS PostgreSQL 数据库/网络/VPC/交换机/切换虚拟交换机.md)|√|√|√|√|
|只读实例|[创建只读实例](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/只读实例/创建PostgreSQL只读实例.md)|√|√|√|√|
|安全管理|[设置白名单](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/设置白名单.md)|√|√|√|√|
|[设置SSL加密](/intl.zh-CN/RDS PostgreSQL 数据库/数据安全/加密/设置数据加密.md)|√|√|√|√|
|[设置云盘加密](/intl.zh-CN/RDS PostgreSQL 数据库/数据安全/加密/设置数据加密.md)|√|√|√|√|
|[切换高安全白名单模式](/intl.zh-CN/RDS PostgreSQL 数据库/数据安全/加密/切换为高安全白名单模式.md)|×|×|×|×|
|[全加密云数据库](/intl.zh-CN/RDS PostgreSQL 数据库/数据安全/加密/全加密云数据库.md)|×|×|×|×|
|审计|[SQL审计（数据库审计）](/intl.zh-CN/RDS PostgreSQL 数据库/日志/审计/历史事件/SQL审计（数据库审计）.md)|√|√|√|√|
|[日志管理](/intl.zh-CN/RDS PostgreSQL 数据库/日志/审计/历史事件/查看日志.md)|√|√|√|√|
|[历史事件](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/历史事件.md)|√|√|√|√|
|数据库备份|[备份数据](/intl.zh-CN/RDS PostgreSQL 数据库/备份/备份PostgreSQL数据.md)|√|√|√|√|
|[免费额度](/intl.zh-CN/RDS PostgreSQL 数据库/备份/查看备份空间免费额度.md)|√|√|√|√|
|[下载备份](/intl.zh-CN/RDS PostgreSQL 数据库/备份/下载数据备份和日志备份.md)|√|√|√|√|
|数据库恢复|[恢复数据](/intl.zh-CN/RDS PostgreSQL 数据库/恢复/恢复PostgreSQL数据.md)|√|√|√|√|
|逻辑订阅|[逻辑订阅](/intl.zh-CN/RDS PostgreSQL 数据库/最佳实践/逻辑订阅.md)|√|√|√|√|
|标签管理|[创建标签](/intl.zh-CN/RDS MySQL 数据库/标签/创建标签.md)|√|√|√|√|
|[删除标签](/intl.zh-CN/RDS MySQL 数据库/标签/删除标签.md)|√|√|√|√|
|[根据标签筛选实例](/intl.zh-CN/RDS MySQL 数据库/标签/根据标签筛选实例.md)|√|√|√|√|

|类别|功能|PostgreSQL 11|
|高可用版|基础版|
|SSD云盘|ESSD/ESSD PL2/ESSD PL3云盘|SSD云盘|ESSD/ESSD PL2/ESSD PL3云盘|
|--|--|-------------|
|----|---|
|-----|------------------------|-----|------------------------|
|数据迁移同步|[数据迁移同步](https://www.alibabacloud.com/help/zh/doc-detail/125233.htm)|×|×|×|×|
|实例管理|[创建实例](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/创建RDS PostgreSQL实例.md)|√|√|√|√|
|[变更配置](/intl.zh-CN/RDS PostgreSQL 数据库/实例/变更配置.md)|√|√|√|√|
|[设置实例参数](/intl.zh-CN/RDS PostgreSQL 数据库/实例/设置实例参数.md)|√|√|√|√|
|[设置实例保护级别](/intl.zh-CN/RDS PostgreSQL 数据库/实例/设置实例保护级别.md)|√|√|×|×|
|[迁移可用区](/intl.zh-CN/RDS PostgreSQL 数据库/实例/迁移可用区.md)|×|×|×|×|
|[切换主备实例](/intl.zh-CN/RDS PostgreSQL 数据库/实例/自动或手动主备切换.md)|√|√|×|×|
|[重启实例](/intl.zh-CN/RDS PostgreSQL 数据库/实例/重启实例.md)|√|√|√|√|
|[设置可维护时间段](/intl.zh-CN/RDS PostgreSQL 数据库/实例/设置可维护时间段.md)|√|√|√|√|
|[释放实例](/intl.zh-CN/RDS PostgreSQL 数据库/实例/释放实例.md)|√|√|√|√|
|[实例回收站](/intl.zh-CN/RDS PostgreSQL 数据库/实例/实例回收站.md)|√|√|√|√|
|账号管理|[创建账号](/intl.zh-CN/RDS PostgreSQL 数据库/账号/创建账号.md)|√|√|√|√|
|[重置密码](/intl.zh-CN/RDS PostgreSQL 数据库/账号/重置密码.md)|√|√|√|√|
|[锁定账号](/intl.zh-CN/RDS PostgreSQL 数据库/账号/锁定/删除账号.md)|√|√|√|√|
|[删除账号](/intl.zh-CN/RDS PostgreSQL 数据库/账号/锁定/删除账号.md)|√|√|√|√|
|数据库管理|[创建数据库](/intl.zh-CN/RDS PostgreSQL 数据库/数据库/创建数据库.md)|√|√|√|√|
|[删除数据库](/intl.zh-CN/RDS PostgreSQL 数据库/数据库/删除数据库.md)|√|√|√|√|
|[插件](/intl.zh-CN/自研内核 AliPG/支持插件列表.md)|√|√|√|√|
|数据库连接|[连接PostgreSQL实例](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/连接PostgreSQL实例.md)|√|√|√|√|
|[设置连接地址]()|√|√|√|√|
|[查看连接地址/端口](/intl.zh-CN/RDS PostgreSQL 数据库/数据库连接/查看或修改内外网地址和端口.md)|√|√|√|√|
|[申请或释放外网地址](/intl.zh-CN/RDS PostgreSQL 数据库/数据库连接/申请或释放外网地址.md)|√|√|√|√|
|监控报警|[查看资源和引擎监控](/intl.zh-CN/RDS PostgreSQL 数据库/监控与报警/查看资源和引擎监控.md)|√|√|√|√|
|[设置监控频率](/intl.zh-CN/RDS PostgreSQL 数据库/监控与报警/设置监控频率.md)|√|√|√|√|
|[设置报警规则](/intl.zh-CN/RDS PostgreSQL 数据库/监控与报警/设置报警规则.md)|×|×|×|×|
|网络管理|[切换网络类型](/intl.zh-CN/RDS PostgreSQL 数据库/网络/VPC/交换机/切换网络类型.md)|×|×|×|×|
|[切换虚拟交换机](/intl.zh-CN/RDS PostgreSQL 数据库/网络/VPC/交换机/切换虚拟交换机.md)|√|√|√|√|
|只读实例|[创建只读实例](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/只读实例/创建PostgreSQL只读实例.md)|√|√|√|√|
|安全管理|[设置白名单](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/设置白名单.md)|√|√|√|√|
|[设置SSL加密](/intl.zh-CN/RDS PostgreSQL 数据库/数据安全/加密/设置数据加密.md)|√|√|√|√|
|[设置云盘加密](/intl.zh-CN/RDS PostgreSQL 数据库/数据安全/加密/设置数据加密.md)|√|√|√|√|
|[切换高安全白名单模式](/intl.zh-CN/RDS PostgreSQL 数据库/数据安全/加密/切换为高安全白名单模式.md)|×|×|×|×|
|[全加密云数据库](/intl.zh-CN/RDS PostgreSQL 数据库/数据安全/加密/全加密云数据库.md)|×|×|×|×|
|审计|[SQL审计（数据库审计）](/intl.zh-CN/RDS PostgreSQL 数据库/日志/审计/历史事件/SQL审计（数据库审计）.md)|√|√|√|√|
|[日志管理](/intl.zh-CN/RDS PostgreSQL 数据库/日志/审计/历史事件/查看日志.md)|√|√|√|√|
|[历史事件](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/历史事件.md)|√|√|√|√|
|数据库备份|[备份数据](/intl.zh-CN/RDS PostgreSQL 数据库/备份/备份PostgreSQL数据.md)|√|√|√|√|
|[免费额度](/intl.zh-CN/RDS PostgreSQL 数据库/备份/查看备份空间免费额度.md)|√|√|√|√|
|[下载备份](/intl.zh-CN/RDS PostgreSQL 数据库/备份/下载数据备份和日志备份.md)|√|√|√|√|
|数据库恢复|[恢复数据](/intl.zh-CN/RDS PostgreSQL 数据库/恢复/恢复PostgreSQL数据.md)|√|√|√|√|
|逻辑订阅|[逻辑订阅](/intl.zh-CN/RDS PostgreSQL 数据库/最佳实践/逻辑订阅.md)|√|√|√|√|
|标签管理|[创建标签](/intl.zh-CN/RDS MySQL 数据库/标签/创建标签.md)|√|√|√|√|
|[删除标签](/intl.zh-CN/RDS MySQL 数据库/标签/删除标签.md)|√|√|√|√|
|[根据标签筛选实例](/intl.zh-CN/RDS MySQL 数据库/标签/根据标签筛选实例.md)|√|√|√|√|

|类别|功能|PostgreSQL 10|PostgreSQL 9.4|
|高可用版|基础版|高可用版|
|本地SSD盘|SSD云盘|ESSD/ESSD PL2/ESSD PL3云盘|SSD云盘|本地SSD盘|
|--|--|-------------|--------------|
|----|---|----|
|------|-----|------------------------|-----|------|
|实例管理|[创建实例](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/创建RDS PostgreSQL实例.md)|√|√|√|√|√|
|[变更配置](/intl.zh-CN/RDS PostgreSQL 数据库/实例/变更配置.md)|√|√|√|√|√|
|[设置实例参数](/intl.zh-CN/RDS PostgreSQL 数据库/实例/设置实例参数.md)|√|√|√|√|√|
|[设置实例保护级别](/intl.zh-CN/RDS PostgreSQL 数据库/实例/设置实例保护级别.md)|×|√|√|×|×|
|[迁移可用区](/intl.zh-CN/RDS PostgreSQL 数据库/实例/迁移可用区.md)|√|×|×|×|√|
|[切换主备实例](/intl.zh-CN/RDS PostgreSQL 数据库/实例/自动或手动主备切换.md)|√|√|√|×|√|
|[重启实例](/intl.zh-CN/RDS PostgreSQL 数据库/实例/重启实例.md)|√|√|√|√|√|
|[设置可维护时间段](/intl.zh-CN/RDS PostgreSQL 数据库/实例/设置可维护时间段.md)|√|√|√|√|√|
|[释放实例](/intl.zh-CN/RDS PostgreSQL 数据库/实例/释放实例.md)|√|√|√|√|√|
|[实例回收站](/intl.zh-CN/RDS PostgreSQL 数据库/实例/实例回收站.md)|√|√|√|√|√|
|账号管理|[创建账号](/intl.zh-CN/RDS PostgreSQL 数据库/账号/创建账号.md)|√|√|√|√|√|
|[重置密码](/intl.zh-CN/RDS PostgreSQL 数据库/账号/重置密码.md)|√|√|√|√|√|
|[锁定账号](/intl.zh-CN/RDS PostgreSQL 数据库/账号/锁定/删除账号.md)|×|√|√|√|×|
|[删除账号](/intl.zh-CN/RDS PostgreSQL 数据库/账号/锁定/删除账号.md)|√|√|√|√|√|
|数据库管理|[创建数据库](/intl.zh-CN/RDS PostgreSQL 数据库/数据库/创建数据库.md)|√|√|√|√|√|
|[删除数据库](/intl.zh-CN/RDS PostgreSQL 数据库/数据库/删除数据库.md)|√|√|√|√|√|
|[插件](/intl.zh-CN/自研内核 AliPG/支持插件列表.md)|√|√|√|√|√|
|数据库连接|[连接PostgreSQL实例](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/连接PostgreSQL实例.md)|√|√|√|√|√|
|[设置连接地址]()|√|√|√|√|√|
|[查看连接地址/端口](/intl.zh-CN/RDS PostgreSQL 数据库/数据库连接/查看或修改内外网地址和端口.md)|√|√|√|√|√|
|[申请或释放外网地址](/intl.zh-CN/RDS PostgreSQL 数据库/数据库连接/申请或释放外网地址.md)|√|√|√|√|√|
|监控报警|[查看资源和引擎监控](/intl.zh-CN/RDS PostgreSQL 数据库/监控与报警/查看资源和引擎监控.md)|√|√|√|√|√|
|[设置监控频率](/intl.zh-CN/RDS PostgreSQL 数据库/监控与报警/设置监控频率.md)|√|√|√|√|√|
|[设置报警规则](/intl.zh-CN/RDS PostgreSQL 数据库/监控与报警/设置报警规则.md)|√|√|√|√|√|
|网络管理|[切换网络类型](/intl.zh-CN/RDS PostgreSQL 数据库/网络/VPC/交换机/切换网络类型.md)|√|×|×|×|√|
|[切换虚拟交换机](/intl.zh-CN/RDS PostgreSQL 数据库/网络/VPC/交换机/切换虚拟交换机.md)|×|√|√|√|×|
|只读实例|[创建只读实例](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/只读实例/创建PostgreSQL只读实例.md)|√|√|√|√|×|
|安全管理|[设置白名单](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/设置白名单.md)|√|√|√|√|√|
|[设置SSL加密](/intl.zh-CN/RDS PostgreSQL 数据库/数据安全/加密/设置数据加密.md)|×|√|√|√|×|
|[设置云盘加密](/intl.zh-CN/RDS PostgreSQL 数据库/数据安全/加密/设置数据加密.md)|×|√|√|√|×|
|[切换高安全白名单模式](/intl.zh-CN/RDS PostgreSQL 数据库/数据安全/加密/切换为高安全白名单模式.md)|√|×|×|×|√|
|[全加密云数据库](/intl.zh-CN/RDS PostgreSQL 数据库/数据安全/加密/全加密云数据库.md)|×|√|√|×|×|
|审计|[SQL审计（数据库审计）](/intl.zh-CN/RDS PostgreSQL 数据库/日志/审计/历史事件/SQL审计（数据库审计）.md)|√|√|√|√|√|
|[日志管理](/intl.zh-CN/RDS PostgreSQL 数据库/日志/审计/历史事件/查看日志.md)|√|√|√|√|√|
|[历史事件](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/历史事件.md)|√|√|√|√|√|
|数据库备份|[备份数据](/intl.zh-CN/RDS PostgreSQL 数据库/备份/备份PostgreSQL数据.md)|√|√|√|√|√|
|[免费额度](/intl.zh-CN/RDS PostgreSQL 数据库/备份/查看备份空间免费额度.md)|√|√|√|√|√|
|[下载备份](/intl.zh-CN/RDS PostgreSQL 数据库/备份/下载数据备份和日志备份.md)|√|√|√|√|√|
|数据库恢复|[恢复数据](/intl.zh-CN/RDS PostgreSQL 数据库/恢复/恢复PostgreSQL数据.md)|√|√|√|√|√|
|逻辑订阅|[逻辑订阅](/intl.zh-CN/RDS PostgreSQL 数据库/最佳实践/逻辑订阅.md)|×|√|√|√|×|
|标签管理|[创建标签](/intl.zh-CN/RDS MySQL 数据库/标签/创建标签.md)|√|√|√|√|√|
|[删除标签](/intl.zh-CN/RDS MySQL 数据库/标签/删除标签.md)|√|√|√|√|√|
|[根据标签筛选实例](/intl.zh-CN/RDS MySQL 数据库/标签/根据标签筛选实例.md)|√|√|√|√|√|

