# MySQL功能概览

本文介绍RDS MySQL各版本、系列、存储类型支持的功能，便于您根据自身需要选购实例或查询已购实例功能。

## MySQL 8.0

|类别|功能|MySQL 8.0|
|三节点企业版|高可用版|基础版|
|本地SSD盘|本地SSD盘|SSD云盘|ESSD云盘|SSD云盘|
|--|--|---------|
|------|----|---|
|------|------|-----|------|-----|
|数据迁移|[数据迁移方案概览](/intl.zh-CN/RDS MySQL 数据库/数据迁移/数据迁移方案概览.md)|√|√|√|√|√|
|数据同步|[数据同步方案概览](/intl.zh-CN/RDS MySQL 数据库/数据同步/数据同步方案概览.md)|√|√|√|√|√|
|实例管理|[创建实例](/intl.zh-CN/RDS MySQL 数据库/快速入门/创建RDS MySQL实例.md)|√|√|√|√|√|
|[变更配置](/intl.zh-CN/RDS MySQL 数据库/变更实例/变更配置.md)|√|√|√|√|√|
|[迁移可用区](/intl.zh-CN/RDS MySQL 数据库/变更实例/迁移可用区.md)|√|√|×|×|×|
|[自动/手动切换主备实例](/intl.zh-CN/RDS MySQL 数据库/变更实例/自动或手动主备切换.md)|×|√|√|√|×|
|[修改数据复制方式](/intl.zh-CN/RDS MySQL 数据库/变更实例/修改数据复制方式.md)|×|√|×|×|×|
|[使用参数模板](/intl.zh-CN/RDS MySQL 数据库/实例参数/参数模板/使用参数模板.md)|√|√|√|√|√|
|[灾备实例](/intl.zh-CN/RDS MySQL 数据库/灾备实例/创建灾备实例.md)|√|√|√|√|×|
|[重启实例](/intl.zh-CN/RDS MySQL 数据库/实例生命周期/重启实例.md)|√|√|√|√|√|
|[设置可维护时间段](/intl.zh-CN/RDS MySQL 数据库/变更实例/设置可维护时间段.md)|√|√|√|√|√|
|[释放实例](/intl.zh-CN/RDS MySQL 数据库/实例生命周期/释放实例.md)|√|√|√|√|√|
|[实例回收站](/intl.zh-CN/RDS MySQL 数据库/实例生命周期/实例回收站.md)|√|√|√|√|√|
|实例升级|[升级内核小版本](/intl.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)|√|√|√|√|√|
|[升级数据库版本](/intl.zh-CN/RDS MySQL 数据库/升级版本/升级数据库版本.md)|×|×|×|×|×|
|账号管理|[创建账号](/intl.zh-CN/RDS MySQL 数据库/账号/创建账号.md)|√|√|√|√|√|
|[重置密码](/intl.zh-CN/RDS MySQL 数据库/账号/重置密码.md)|√|√|√|√|√|
|[修改账号权限](/intl.zh-CN/RDS MySQL 数据库/账号/账号权限/修改账号权限.md)|√|√|√|√|√|
|[授权服务账号](/intl.zh-CN/RDS MySQL 数据库/账号/授权服务账号.md)|√|√|×|×|×|
|[删除账号](/intl.zh-CN/RDS MySQL 数据库/账号/删除账号.md)|√|√|√|√|√|
|[重置高权限账号](/intl.zh-CN/RDS MySQL 数据库/账号/重置高权限账号.md)|√|√|√|√|√|
|数据库管理|[创建数据库](/intl.zh-CN/RDS MySQL 数据库/数据库/创建数据库.md)|√|√|√|√|√|
|[删除数据库](/intl.zh-CN/RDS MySQL 数据库/数据库/删除数据库.md)|√|√|√|√|√|
|数据库连接|[连接实例](/intl.zh-CN/RDS MySQL 数据库/快速入门/连接MySQL实例.md)|√|√|√|√|√|
|[设置连接地址]()|√|√|√|√|√|
|[查看连接地址/端口](/intl.zh-CN/RDS MySQL 数据库/数据库连接/查看或修改内外网地址和端口.md)|√|√|√|√|√|
|[申请外网地址](/intl.zh-CN/RDS MySQL 数据库/数据库连接/申请或释放外网地址.md)|√|√|√|√|√|
|监控报警|[查看监控](/intl.zh-CN/RDS MySQL 数据库/监控与报警/查看资源和引擎监控.md)|√|√|√|√|√|
|[设置监控频率](/intl.zh-CN/RDS MySQL 数据库/监控与报警/设置监控频率.md)|√|√|√|√|√|
|[设置报警规则](/intl.zh-CN/RDS MySQL 数据库/监控与报警/设置报警规则.md)|√|√|√|√|√|
|网络管理|[切换网络类型](/intl.zh-CN/RDS MySQL 数据库/数据库连接/切换网络类型.md)|√|√|×|×|×|
|[切换专有网络VPC和虚拟交换机](/intl.zh-CN/RDS MySQL 数据库/数据库连接/切换专有网络VPC和虚拟交换机.md)|√|√|×|×|×|
|只读实例与读写分离|[创建只读实例](/intl.zh-CN/RDS MySQL 数据库/只读实例/创建MySQL只读实例.md)|√|√|√|√|×|
|[开通读写分离](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/共享代理（下线中）/开通读写分离（共享代理）.md)|√|√|√|√|×|
|[切换读写分离地址类型](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/数据库独享代理.md)|√|√|√|√|×|
|安全管理|[设置白名单](/intl.zh-CN/RDS MySQL 数据库/快速入门/设置白名单.md)|√|√|√|√|√|
|[切换高安全白名单模式](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/切换为高安全白名单模式.md)|×|×|×|×|×|
|[设置SSL加密](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/设置SSL加密.md)|√|√|√|√|×|
|[设置透明数据加密TDE](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/设置透明数据加密TDE.md)|×|√|×|×|×|
|审计|[SQL洞察](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/SQL洞察.md)|√|√|√|√|×|
|[日志管理](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/查看日志.md)|√|√|√|√|×|
|数据库备份|[备份数据](/intl.zh-CN/RDS MySQL 数据库/备份/备份MySQL数据.md)|√|√|√|√|√|
|[免费额度](/intl.zh-CN/RDS MySQL 数据库/备份/查看备份空间免费额度.md)|√|√|√|√|√|
|[下载备份](/intl.zh-CN/RDS MySQL 数据库/备份/下载数据备份和日志备份.md)|√|√|√|√|√|
|[跨地域备份](/intl.zh-CN/RDS MySQL 数据库/备份/跨地域备份数据.md)|×|√|×|×|×|
|数据库恢复|[恢复数据](/intl.zh-CN/RDS MySQL 数据库/恢复/恢复MySQL数据.md)|√|√|√|√|√|
|[单库单表恢复](/intl.zh-CN/RDS MySQL 数据库/恢复/MySQL单库单表恢复.md)|×|√|×|×|×|
|[跨地域恢复](/intl.zh-CN/RDS MySQL 数据库/恢复/跨地域恢复数据.md)|×|√|×|×|×|
|独享代理|[数据库独享代理](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/数据库独享代理.md)|√|√|√|√|×|
|AliSQL|[AliSQL](/intl.zh-CN/自研内核 AliSQL/AliSQL 功能概览.md)|√|√|√|√|√|
|标签管理|[创建标签](/intl.zh-CN/RDS MySQL 数据库/标签/创建标签.md)|√|√|√|√|√|
|[删除标签](/intl.zh-CN/RDS MySQL 数据库/标签/删除标签.md)|√|√|√|√|√|
|[根据标签筛选实例](/intl.zh-CN/RDS MySQL 数据库/标签/根据标签筛选实例.md)|√|√|√|√|√|

## MySQL 5.7

|类别|功能|MySQL 5.7|
|三节点企业版|高可用版|基础版|
|本地SSD盘|本地SSD盘|SSD云盘|ESSD云盘|SSD云盘|
|--|--|---------|
|------|----|---|
|------|------|-----|------|-----|
|数据迁移|[数据迁移方案概览](/intl.zh-CN/RDS MySQL 数据库/数据迁移/数据迁移方案概览.md)|√|√|√|√|√|
|数据同步|[数据同步方案概览](/intl.zh-CN/RDS MySQL 数据库/数据同步/数据同步方案概览.md)|√|√|√|√|√|
|实例管理|[创建实例](/intl.zh-CN/RDS MySQL 数据库/快速入门/创建RDS MySQL实例.md)|√|√|√|√|√|
|[变更配置](/intl.zh-CN/RDS MySQL 数据库/变更实例/变更配置.md)|√|√|√|√|√|
|[迁移可用区](/intl.zh-CN/RDS MySQL 数据库/变更实例/迁移可用区.md)|√|√|×|×|×|
|[自动/手动切换主备实例](/intl.zh-CN/RDS MySQL 数据库/变更实例/自动或手动主备切换.md)|×|√|√|√|×|
|[修改数据复制方式](/intl.zh-CN/RDS MySQL 数据库/变更实例/修改数据复制方式.md)|×|√|×|×|×|
|[使用参数模板](/intl.zh-CN/RDS MySQL 数据库/实例参数/参数模板/使用参数模板.md)|√|√|√|√|√|
|[灾备实例](/intl.zh-CN/RDS MySQL 数据库/灾备实例/创建灾备实例.md)|√|√|√|√|×|
|[重启实例](/intl.zh-CN/RDS MySQL 数据库/实例生命周期/重启实例.md)|√|√|√|√|√|
|[设置可维护时间段](/intl.zh-CN/RDS MySQL 数据库/变更实例/设置可维护时间段.md)|√|√|√|√|√|
|[释放实例](/intl.zh-CN/RDS MySQL 数据库/实例生命周期/释放实例.md)|√|√|√|√|√|
|[实例回收站](/intl.zh-CN/RDS MySQL 数据库/实例生命周期/实例回收站.md)|√|√|√|√|√|
|实例升级|[升级内核小版本](/intl.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)|√|√|√|√|√|
|[升级数据库版本](/intl.zh-CN/RDS MySQL 数据库/升级版本/升级数据库版本.md)|×|×|×|×|×|
|账号管理|[创建账号](/intl.zh-CN/RDS MySQL 数据库/账号/创建账号.md)|√|√|√|√|√|
|[重置密码](/intl.zh-CN/RDS MySQL 数据库/账号/重置密码.md)|√|√|√|√|√|
|[修改账号权限](/intl.zh-CN/RDS MySQL 数据库/账号/账号权限/修改账号权限.md)|√|√|√|√|√|
|[授权服务账号](/intl.zh-CN/RDS MySQL 数据库/账号/授权服务账号.md)|√|√|×|×|×|
|[删除账号](/intl.zh-CN/RDS MySQL 数据库/账号/删除账号.md)|√|√|√|√|√|
|[重置高权限账号](/intl.zh-CN/RDS MySQL 数据库/账号/重置高权限账号.md)|√|√|√|√|√|
|数据库管理|[创建数据库](/intl.zh-CN/RDS MySQL 数据库/数据库/创建数据库.md)|√|√|√|√|√|
|[删除数据库](/intl.zh-CN/RDS MySQL 数据库/数据库/删除数据库.md)|√|√|√|√|√|
|数据库连接|[连接实例](/intl.zh-CN/RDS MySQL 数据库/快速入门/连接MySQL实例.md)|√|√|√|√|√|
|[设置连接地址]()|√|√|√|√|√|
|[查看连接地址/端口](/intl.zh-CN/RDS MySQL 数据库/数据库连接/查看或修改内外网地址和端口.md)|√|√|√|√|√|
|[申请外网地址](/intl.zh-CN/RDS MySQL 数据库/数据库连接/申请或释放外网地址.md)|√|√|√|√|√|
|监控报警|[查看监控](/intl.zh-CN/RDS MySQL 数据库/监控与报警/查看资源和引擎监控.md)|√|√|√|√|√|
|[设置监控频率](/intl.zh-CN/RDS MySQL 数据库/监控与报警/设置监控频率.md)|√|√|√|√|√|
|[设置报警规则](/intl.zh-CN/RDS MySQL 数据库/监控与报警/设置报警规则.md)|√|√|√|√|√|
|网络管理|[切换网络类型](/intl.zh-CN/RDS MySQL 数据库/数据库连接/切换网络类型.md)|√|√|×|×|√|
|[切换专有网络VPC和虚拟交换机](/intl.zh-CN/RDS MySQL 数据库/数据库连接/切换专有网络VPC和虚拟交换机.md)|√|√|×|×|×|
|只读实例与读写分离|[创建只读实例](/intl.zh-CN/RDS MySQL 数据库/只读实例/创建MySQL只读实例.md)|√|√|√|√|×|
|[开通读写分离](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/共享代理（下线中）/开通读写分离（共享代理）.md)|√|√|√|√|×|
|[切换读写分离地址类型](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/数据库独享代理.md)|√|√|√|√|×|
|安全管理|[设置白名单](/intl.zh-CN/RDS MySQL 数据库/快速入门/设置白名单.md)|√|√|√|√|√|
|[切换高安全白名单模式](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/切换为高安全白名单模式.md)|√|√|√|√|×|
|[设置SSL加密](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/设置SSL加密.md)|√|√|√|√|×|
|[设置透明数据加密TDE](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/设置透明数据加密TDE.md)|×|√|×|×|×|
|审计|[SQL洞察](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/SQL洞察.md)|√|√|√|√|×|
|[日志管理](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/查看日志.md)|√|√|√|√|×|
|数据库备份|[备份数据](/intl.zh-CN/RDS MySQL 数据库/备份/备份MySQL数据.md)|√|√|√|√|√|
|[免费额度](/intl.zh-CN/RDS MySQL 数据库/备份/查看备份空间免费额度.md)|√|√|√|√|√|
|[下载备份](/intl.zh-CN/RDS MySQL 数据库/备份/下载数据备份和日志备份.md)|√|√|√|√|√|
|[跨地域备份](/intl.zh-CN/RDS MySQL 数据库/备份/跨地域备份数据.md)|×|√|×|×|×|
|数据库恢复|[恢复数据](/intl.zh-CN/RDS MySQL 数据库/恢复/恢复MySQL数据.md)|√|√|√|√|√|
|[单库单表恢复](/intl.zh-CN/RDS MySQL 数据库/恢复/MySQL单库单表恢复.md)|×|√|×|×|×|
|[跨地域恢复](/intl.zh-CN/RDS MySQL 数据库/恢复/跨地域恢复数据.md)|×|√|×|×|×|
|独享代理|[数据库独享代理](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/数据库独享代理.md)|√|√|√|√|×|
|AliSQL|[AliSQL](/intl.zh-CN/自研内核 AliSQL/AliSQL 功能概览.md)|√|√|√|√|√|
|标签管理|[创建标签](/intl.zh-CN/RDS MySQL 数据库/标签/创建标签.md)|√|√|√|√|√|
|[删除标签](/intl.zh-CN/RDS MySQL 数据库/标签/删除标签.md)|√|√|√|√|√|
|[根据标签筛选实例](/intl.zh-CN/RDS MySQL 数据库/标签/根据标签筛选实例.md)|√|√|√|√|√|

## MySQL 5.6

|类别|功能|MySQL 5.6|
|高可用版|
|本地SSD盘|
|--|--|---------|
|----|
|------|
|数据迁移|[数据迁移方案概览](/intl.zh-CN/RDS MySQL 数据库/数据迁移/数据迁移方案概览.md)|√|
|数据同步|[数据同步方案概览](/intl.zh-CN/RDS MySQL 数据库/数据同步/数据同步方案概览.md)|√|
|实例管理|[创建实例](/intl.zh-CN/RDS MySQL 数据库/快速入门/创建RDS MySQL实例.md)|√|
|[变更配置](/intl.zh-CN/RDS MySQL 数据库/变更实例/变更配置.md)|√|
|[迁移可用区](/intl.zh-CN/RDS MySQL 数据库/变更实例/迁移可用区.md)|√|
|[自动/手动切换主备实例](/intl.zh-CN/RDS MySQL 数据库/变更实例/自动或手动主备切换.md)|√|
|[修改数据复制方式](/intl.zh-CN/RDS MySQL 数据库/变更实例/修改数据复制方式.md)|√|
|[使用参数模板](/intl.zh-CN/RDS MySQL 数据库/实例参数/参数模板/使用参数模板.md)|√|
|[重启实例](/intl.zh-CN/RDS MySQL 数据库/实例生命周期/重启实例.md)|√|
|[设置可维护时间段](/intl.zh-CN/RDS MySQL 数据库/变更实例/设置可维护时间段.md)|√|
|[释放实例](/intl.zh-CN/RDS MySQL 数据库/实例生命周期/释放实例.md)|√|
|[实例回收站](/intl.zh-CN/RDS MySQL 数据库/实例生命周期/实例回收站.md)|√|
|实例升级|[升级内核小版本](/intl.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)|√|
|[升级数据库版本](/intl.zh-CN/RDS MySQL 数据库/升级版本/升级数据库版本.md)|×|
|账号管理|[创建账号](/intl.zh-CN/RDS MySQL 数据库/账号/创建账号.md)|√|
|[重置密码](/intl.zh-CN/RDS MySQL 数据库/账号/重置密码.md)|√|
|[修改账号权限](/intl.zh-CN/RDS MySQL 数据库/账号/账号权限/修改账号权限.md)|√|
|[授权服务账号](/intl.zh-CN/RDS MySQL 数据库/账号/授权服务账号.md)|√|
|[删除账号](/intl.zh-CN/RDS MySQL 数据库/账号/删除账号.md)|√|
|[重置高权限账号](/intl.zh-CN/RDS MySQL 数据库/账号/重置高权限账号.md)|√|
|数据库管理|[创建数据库](/intl.zh-CN/RDS MySQL 数据库/数据库/创建数据库.md)|√|
|[删除数据库](/intl.zh-CN/RDS MySQL 数据库/数据库/删除数据库.md)|√|
|数据库连接|[连接实例](/intl.zh-CN/RDS MySQL 数据库/快速入门/连接MySQL实例.md)|√|
|[设置连接地址]()|√|
|[查看连接地址/端口](/intl.zh-CN/RDS MySQL 数据库/数据库连接/查看或修改内外网地址和端口.md)|√|
|[申请外网地址](/intl.zh-CN/RDS MySQL 数据库/数据库连接/申请或释放外网地址.md)|√|
|监控报警|[查看监控](/intl.zh-CN/RDS MySQL 数据库/监控与报警/查看资源和引擎监控.md)|√|
|[设置监控频率](/intl.zh-CN/RDS MySQL 数据库/监控与报警/设置监控频率.md)|√|
|[设置报警规则](/intl.zh-CN/RDS MySQL 数据库/监控与报警/设置报警规则.md)|√|
|网络管理|[切换网络类型](/intl.zh-CN/RDS MySQL 数据库/数据库连接/切换网络类型.md)|√|
|[切换专有网络VPC和虚拟交换机](/intl.zh-CN/RDS MySQL 数据库/数据库连接/切换专有网络VPC和虚拟交换机.md)|√|
|只读实例与读写分离|[创建只读实例](/intl.zh-CN/RDS MySQL 数据库/只读实例/创建MySQL只读实例.md)|√|
|[开通读写分离](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/共享代理（下线中）/开通读写分离（共享代理）.md)|√|
|[切换读写分离地址类型](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/数据库独享代理.md)|√|
|安全管理|[设置白名单](/intl.zh-CN/RDS MySQL 数据库/快速入门/设置白名单.md)|√|
|[切换高安全白名单模式](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/切换为高安全白名单模式.md)|√|
|[设置SSL加密](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/设置SSL加密.md)|√|
|[设置透明数据加密TDE](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/设置透明数据加密TDE.md)|√|
|审计|[SQL洞察](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/SQL洞察.md)|√|
|[日志管理](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/查看日志.md)|√|
|数据库备份|[备份数据](/intl.zh-CN/RDS MySQL 数据库/备份/备份MySQL数据.md)|√|
|[免费额度](/intl.zh-CN/RDS MySQL 数据库/备份/查看备份空间免费额度.md)|√|
|[下载备份](/intl.zh-CN/RDS MySQL 数据库/备份/下载数据备份和日志备份.md)|√|
|[跨地域备份](/intl.zh-CN/RDS MySQL 数据库/备份/跨地域备份数据.md)|√|
|数据库恢复|[恢复数据](/intl.zh-CN/RDS MySQL 数据库/恢复/恢复MySQL数据.md)|√|
|[单库单表恢复](/intl.zh-CN/RDS MySQL 数据库/恢复/MySQL单库单表恢复.md)|√|
|[跨地域恢复](/intl.zh-CN/RDS MySQL 数据库/恢复/跨地域恢复数据.md)|√|
|独享代理|[数据库独享代理](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/数据库独享代理.md)|×|
|AliSQL|[AliSQL](/intl.zh-CN/自研内核 AliSQL/AliSQL 功能概览.md)|√|
|标签管理|[创建标签](/intl.zh-CN/RDS MySQL 数据库/标签/创建标签.md)|√|
|[删除标签](/intl.zh-CN/RDS MySQL 数据库/标签/删除标签.md)|√|
|[根据标签筛选实例](/intl.zh-CN/RDS MySQL 数据库/标签/根据标签筛选实例.md)|√|

## MySQL 5.5

|类别|功能|MySQL 5.5|
|高可用版|
|本地SSD盘|
|--|--|---------|
|----|
|------|
|数据迁移|[数据迁移方案概览](/intl.zh-CN/RDS MySQL 数据库/数据迁移/数据迁移方案概览.md)|√|
|数据同步|[数据同步方案概览](/intl.zh-CN/RDS MySQL 数据库/数据同步/数据同步方案概览.md)|√|
|实例管理|[创建实例](/intl.zh-CN/RDS MySQL 数据库/快速入门/创建RDS MySQL实例.md)|√|
|[变更配置](/intl.zh-CN/RDS MySQL 数据库/变更实例/变更配置.md)|√|
|[迁移可用区](/intl.zh-CN/RDS MySQL 数据库/变更实例/迁移可用区.md)|√|
|[自动/手动切换主备实例](/intl.zh-CN/RDS MySQL 数据库/变更实例/自动或手动主备切换.md)|√|
|[修改数据复制方式](/intl.zh-CN/RDS MySQL 数据库/变更实例/修改数据复制方式.md)|√|
|[使用参数模板](/intl.zh-CN/RDS MySQL 数据库/实例参数/参数模板/使用参数模板.md)|×|
|[灾备实例](/intl.zh-CN/RDS MySQL 数据库/灾备实例/创建灾备实例.md)|×|
|[重启实例](/intl.zh-CN/RDS MySQL 数据库/实例生命周期/重启实例.md)|√|
|[设置可维护时间段](/intl.zh-CN/RDS MySQL 数据库/变更实例/设置可维护时间段.md)|√|
|[释放实例](/intl.zh-CN/RDS MySQL 数据库/实例生命周期/释放实例.md)|√|
|[实例回收站](/intl.zh-CN/RDS MySQL 数据库/实例生命周期/实例回收站.md)|√|
|实例升级|[升级内核小版本](/intl.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)|√|
|[升级数据库版本](/intl.zh-CN/RDS MySQL 数据库/升级版本/升级数据库版本.md)|√|
|账号管理|[创建账号](/intl.zh-CN/RDS MySQL 数据库/账号/创建账号.md)|√|
|[重置密码](/intl.zh-CN/RDS MySQL 数据库/账号/重置密码.md)|√|
|[修改账号权限](/intl.zh-CN/RDS MySQL 数据库/账号/账号权限/修改账号权限.md)|√|
|[授权服务账号](/intl.zh-CN/RDS MySQL 数据库/账号/授权服务账号.md)|√|
|[删除账号](/intl.zh-CN/RDS MySQL 数据库/账号/删除账号.md)|√|
|[重置高权限账号](/intl.zh-CN/RDS MySQL 数据库/账号/重置高权限账号.md)|√|
|数据库管理|[创建数据库](/intl.zh-CN/RDS MySQL 数据库/数据库/创建数据库.md)|√|
|[删除数据库](/intl.zh-CN/RDS MySQL 数据库/数据库/删除数据库.md)|√|
|数据库连接|[连接实例](/intl.zh-CN/RDS MySQL 数据库/快速入门/连接MySQL实例.md)|√|
|[设置连接地址]()|√|
|[查看连接地址/端口](/intl.zh-CN/RDS MySQL 数据库/数据库连接/查看或修改内外网地址和端口.md)|√|
|[申请外网地址](/intl.zh-CN/RDS MySQL 数据库/数据库连接/申请或释放外网地址.md)|√|
|监控报警|[查看监控](/intl.zh-CN/RDS MySQL 数据库/监控与报警/查看资源和引擎监控.md)|√|
|[设置监控频率](/intl.zh-CN/RDS MySQL 数据库/监控与报警/设置监控频率.md)|√|
|[设置报警规则](/intl.zh-CN/RDS MySQL 数据库/监控与报警/设置报警规则.md)|√|
|网络管理|[切换网络类型](/intl.zh-CN/RDS MySQL 数据库/数据库连接/切换网络类型.md)|√|
|[切换专有网络VPC和虚拟交换机](/intl.zh-CN/RDS MySQL 数据库/数据库连接/切换专有网络VPC和虚拟交换机.md)|√|
|只读实例与读写分离|[创建只读实例](/intl.zh-CN/RDS MySQL 数据库/只读实例/创建MySQL只读实例.md)|×|
|[开通读写分离](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/共享代理（下线中）/开通读写分离（共享代理）.md)|×|
|[切换读写分离地址类型](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/数据库独享代理.md)|×|
|安全管理|[设置白名单](/intl.zh-CN/RDS MySQL 数据库/快速入门/设置白名单.md)|√|
|[切换高安全白名单模式](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/切换为高安全白名单模式.md)|√|
|[设置SSL加密](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/设置SSL加密.md)|×|
|[设置透明数据加密TDE](/intl.zh-CN/RDS MySQL 数据库/数据安全/加密/设置透明数据加密TDE.md)|×|
|审计|[SQL洞察](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/SQL洞察.md)|√|
|[日志管理](/intl.zh-CN/RDS MySQL 数据库/日志/审计/历史事件/查看日志.md)|√|
|数据库备份|[备份数据](/intl.zh-CN/RDS MySQL 数据库/备份/备份MySQL数据.md)|√|
|[免费额度](/intl.zh-CN/RDS MySQL 数据库/备份/查看备份空间免费额度.md)|√|
|[下载备份](/intl.zh-CN/RDS MySQL 数据库/备份/下载数据备份和日志备份.md)|√|
|[跨地域备份](/intl.zh-CN/RDS MySQL 数据库/备份/跨地域备份数据.md)|×|
|数据库恢复|[恢复数据](/intl.zh-CN/RDS MySQL 数据库/恢复/恢复MySQL数据.md)|√|
|[单库单表恢复](/intl.zh-CN/RDS MySQL 数据库/恢复/MySQL单库单表恢复.md)|×|
|[跨地域恢复](/intl.zh-CN/RDS MySQL 数据库/恢复/跨地域恢复数据.md)|×|
|独享代理|[数据库独享代理](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/数据库独享代理.md)|×|
|AliSQL|[AliSQL](/intl.zh-CN/自研内核 AliSQL/AliSQL 功能概览.md)|x|
|标签管理|[创建标签](/intl.zh-CN/RDS MySQL 数据库/标签/创建标签.md)|√|
|[删除标签](/intl.zh-CN/RDS MySQL 数据库/标签/删除标签.md)|√|
|[根据标签筛选实例](/intl.zh-CN/RDS MySQL 数据库/标签/根据标签筛选实例.md)|√|

