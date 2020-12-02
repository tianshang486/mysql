# API概览

云数据库RDS提供以下相关API接口。

## 热门API TOP 10

|API|描述|
|---|--|
|[CreateDBInstance](/intl.zh-CN/API 参考/实例/创建RDS实例.md)|创建一个RDS实例。|
|[DescribeDBInstances](/intl.zh-CN/API 参考/实例/查询实例列表.md)|查询RDS实例列表或被RAM授权的实例列表。|
|[DescribeDBInstanceAttribute](/intl.zh-CN/API 参考/实例/查询实例详细信息.md)|查询RDS实例的详细信息。|
|[DescribeDBInstancePerformance](/intl.zh-CN/API 参考/监控/查询性能数据.md)|查询实例性能数据。|
|[DescribeSlowLogRecords](/intl.zh-CN/API 参考/日志/查看慢日志明细.md)|查询实例的慢日志明细。|
|[DescribeSlowLogs](/intl.zh-CN/API 参考/日志/查询慢日志统计.md)|查询慢日志统计情况。|
|[DescribeBackups](/intl.zh-CN/API 参考/备份/查看备份列表.md)|查询备份集列表。|
|[DescribeResourceUsage](/intl.zh-CN/API 参考/监控/查询空间使用信息.md)|查询实例的空间使用信息。|
|[CreateAccount](/intl.zh-CN/API 参考/账号/创建数据库账号.md)|创建管理数据库的账号。|
|[CreateDatabase](/intl.zh-CN/API 参考/数据库/创建数据库.md)|创建数据库。|

## 费用

|API|描述|
|---|--|
|[DescribeAvailableResource](/intl.zh-CN/API 参考/费用/查询可售卖资源.md)|查询某地域可售卖资源信息。|
|[DescribeRenewalPrice](/intl.zh-CN/API 参考/费用/查询续费费用.md)|查询RDS实例续费的费用。|
|[TransformDBInstancePayType](/intl.zh-CN/API 参考/费用/变更计费方式.md)|变更RDS实例的计费方式。|
|[RenewInstance](/intl.zh-CN/API 参考/费用/手动续费.md)|手动续费。|

## 实例

|API|描述|
|---|--|
|[CreateDBInstance](/intl.zh-CN/API 参考/实例/创建RDS实例.md)|创建一个RDS实例。|
|[DeleteDBInstance](/intl.zh-CN/API 参考/实例/释放RDS实例.md)|释放RDS实例。|
|[RestartDBInstance](/intl.zh-CN/API 参考/实例/重启实例.md)|重启RDS实例。|
|[ModifyDBInstanceSpec](/intl.zh-CN/API 参考/实例/变更实例.md)|变更RDS实例（包括常规实例和只读实例，不包括灾备实例和临时实例）的规格或存储空间。|
|[DescribeAvailableZones](/intl.zh-CN/API 参考/实例/查询可用区资源.md)|查询RDS可用区资源。|
|[DescribeDBInstanceAttribute](/intl.zh-CN/API 参考/实例/查询实例详细信息.md)|查询RDS实例的详细信息。|
|[DescribeDBInstances](/intl.zh-CN/API 参考/实例/查询实例列表.md)|查询RDS实例列表或被RAM授权的实例列表。|
|[DescribeRegions](/intl.zh-CN/API 参考/实例/查询可用地域信息.md)|查询当前可选的RDS地域和可用区信息。|
|[MigrateToOtherZone](/intl.zh-CN/API 参考/实例/迁移可用区.md)|迁移RDS实例至其他可用区。|
|[ModifyDBInstanceDescription](/intl.zh-CN/API 参考/实例/修改实例名称.md)|修改RDS实例的描述。|
|[ModifyDBInstanceMaintainTime](/intl.zh-CN/API 参考/实例/修改可维护时间段.md)|修改RDS实例可维护时间段。|

## 升级版本

|API|描述|
|---|--|
|[UpgradeDBInstanceEngineVersion](/intl.zh-CN/API 参考/升级版本/升级数据库版本.md)|升级实例数据库版本。|
|[UpgradeDBInstanceKernelVersion](/intl.zh-CN/API 参考/升级版本/升级内核小版本.md)|升级RDS MySQL实例的内核小版本。|
|[ModifyDBInstanceAutoUpgradeMinorVersion](/intl.zh-CN/API 参考/升级版本/修改小版本升级方式.md)|修改RDS实例升级内核小版本的方式。|

## 连接地址

|API|描述|
|---|--|
|[AllocateInstancePublicConnection](/intl.zh-CN/API 参考/连接地址/申请外网地址.md)|申请实例的外网地址。|
|[DescribeDBInstanceNetInfo](/intl.zh-CN/API 参考/连接地址/查询连接地址.md)|查询实例的所有连接地址信息。|
|[ModifyDBInstanceConnectionString](/intl.zh-CN/API 参考/连接地址/修改连接地址.md)|修改实例的连接地址和端口。|
|[ModifyDBInstanceNetworkExpireTime](/intl.zh-CN/API 参考/连接地址/修改地址过期时间.md)|修改连接地址过期时间。|
|[SwitchDBInstanceNetType](/intl.zh-CN/API 参考/连接地址/切换内外网地址.md)|切换内外网地址。|
|[ReleaseInstancePublicConnection](/intl.zh-CN/API 参考/连接地址/释放外网地址.md)|释放实例的外网连接地址。|

## 主备高可用和数据复制方式

|API|描述|
|---|--|
|[ModifyDBInstanceHAConfig](/intl.zh-CN/API 参考/主备高可用/数据复制方式/修改高可用模式.md)|修改实例的高可用模式和数据复制方式。|
|[DescribeDBInstanceHAConfig](/intl.zh-CN/API 参考/主备高可用/数据复制方式/查询高可用模式.md)|查询RDS实例高可用模式和数据复制方式。|
|[SwitchDBInstanceHA](/intl.zh-CN/API 参考/主备高可用/数据复制方式/切换主备实例.md)|切换RDS实例的主备实例。|
|[ModifyHASwitchConfig](/intl.zh-CN/API 参考/主备高可用/数据复制方式/设置主备自动切换.md)|开启或关闭RDS实例的主备自动切换功能。|
|[DescribeHASwitchConfig](/intl.zh-CN/API 参考/主备高可用/数据复制方式/查询主备切换设置.md)|查询RDS实例主备自动切换设置。|

## 历史事件

|API|描述|
|---|--|
|[DescribeEvents](/intl.zh-CN/API 参考/历史事件/查询历史事件.md)|查询RDS事件记录列表。|
|[DescribeActionEventPolicy](/intl.zh-CN/API 参考/历史事件/查询历史事件是否开启.md)|查询RDS历史事件功能开启情况。|
|[ModifyActionEventPolicy](/intl.zh-CN/API 参考/历史事件/开关历史事件.md)|开启或关闭RDS历史事件功能。|

## 账号

|API|描述|
|---|--|
|[CreateAccount](/intl.zh-CN/API 参考/账号/创建数据库账号.md)|创建管理数据库的账号。|
|[DeleteAccount](/intl.zh-CN/API 参考/账号/删除数据库账号.md)|删除数据库账号。|
|[ResetAccountPassword](/intl.zh-CN/API 参考/账号/重置数据库账号密码.md)|重置账号密码。|
|[LockAccount](/intl.zh-CN/API 参考/账号/锁定账号.md)|锁定RDS PostgreSQL实例的账号。|
|[UnlockAccount](/intl.zh-CN/API 参考/账号/解锁账号.md)|解锁RDS PostgreSQL实例的账号。|
|[DescribeAccounts](/intl.zh-CN/API 参考/账号/查询账号信息.md)|查询实例的账号信息。|
|[ModifyAccountDescription](/intl.zh-CN/API 参考/账号/修改数据库账号描述.md)|修改数据库账号的描述。|
|[GrantAccountPrivilege](/intl.zh-CN/API 参考/账号/账号权限/授权账号.md)|授权账号访问数据库。|
|[RevokeAccountPrivilege](/intl.zh-CN/API 参考/账号/账号权限/撤销账号权限.md)|撤销账号对数据库的访问权限。|
|[ResetAccount](/intl.zh-CN/API 参考/账号/账号权限/重置高权限账号权限.md)|重置高权限账号的权限。|

## 数据库

|API|描述|
|---|--|
|[CreateDatabase](/intl.zh-CN/API 参考/数据库/创建数据库.md)|创建数据库。|
|[DeleteDatabase](/intl.zh-CN/API 参考/数据库/删除数据库.md)|删除实例下的某个数据库。|
|[ModifyDBDescription](/intl.zh-CN/API 参考/数据库/修改数据库备注.md)|修改数据库备注。|
|[CopyDatabaseBetweenInstances](/intl.zh-CN/API 参考/数据库/复制数据库.md)|在实例间复制数据库。|
|[DescribeDatabases](/intl.zh-CN/API 参考/数据库/查询数据库信息.md)|查询实例下的数据库信息。|
|[DescribeCollationTimeZones](/intl.zh-CN/API 参考/数据库/查询排序规则和时区.md)|查询支持的字符集排序规则和时区。|

## 只读实例

|API|描述|
|---|--|
|[CreateReadOnlyDBInstance](/intl.zh-CN/API 参考/只读实例/创建只读实例.md)|为某个实例创建一个只读实例。|
|[DescribeReadDBInstanceDelay](/intl.zh-CN/API 参考/只读实例/查询只读实例延迟信息.md)|查询RDS只读实例的延迟信息。|
|[ModifyReadonlyInstanceDelayReplicationTime](/intl.zh-CN/API 参考/只读实例/设置只读实例延迟复制.md)|修改RDS只读实例的延迟复制时间。|

## 数据库共享代理（下线中）

|API|描述|
|---|--|
|[AllocateReadWriteSplittingConnection](/intl.zh-CN/API 参考/数据库共享代理（下线中）/申请只读地址.md)|申请读写分离地址。|
|[ReleaseReadWriteSplittingConnection](/intl.zh-CN/API 参考/数据库共享代理（下线中）/释放读写分离地址.md)|释放读写分离地址。|
|[CalculateDBInstanceWeight](/intl.zh-CN/API 参考/数据库共享代理（下线中）/查询系统权重分配值.md)|查询系统权重分配值。|
|[ModifyReadWriteSplittingConnection](/intl.zh-CN/API 参考/数据库共享代理（下线中）/修改读权重和延迟阈值.md)|修改读写分离链路的延迟阈值和各个实例的读权重。|
|[DescribeDBInstanceProxyConfiguration](/intl.zh-CN/API 参考/数据库共享代理（下线中）/查询数据库代理设置.md)|查询数据库代理设置。|

## 数据库独享代理（读写分离）

|API|描述|
|---|--|
|[ModifyDBProxy](/intl.zh-CN/API 参考/数据库独享代理（读写分离）/开关独享代理.md)|开启或者关闭RDS实例的数据库独享代理功能。|
|[ModifyDBProxyInstance](/intl.zh-CN/API 参考/数据库独享代理（读写分离）/修改独享代理设置.md)|修改RDS数据库独享代理数量。|
|[ModifyDBProxyEndpoint](/intl.zh-CN/API 参考/数据库独享代理（读写分离）/修改独享代理地址.md)|修改RDS实例数据库独享代理的连接地址配置（读写分离、事务拆分、连接池）。|
|[DescribeDBProxy](/intl.zh-CN/API 参考/数据库独享代理（读写分离）/查询独享代理设置.md)|查询RDS实例的数据库独享代理详情。|
|[DescribeDBProxyEndpoint](/intl.zh-CN/API 参考/数据库独享代理（读写分离）/查询独享代理地址信息.md)|查询RDS实例独享代理的连接地址信息。|
|[DescribeDBProxyPerformance](/intl.zh-CN/API 参考/数据库独享代理（读写分离）/查询独享代理性能.md)|查询独享代理的性能数据。|
|[CreateDBProxyEndpointAddress](/intl.zh-CN/API 参考/数据库独享代理（读写分离）/创建独享代理连接地址.md)|创建RDS实例独享代理的连接地址。|
|[ModifyDBProxyEndpointAddress](/intl.zh-CN/API 参考/数据库独享代理（读写分离）/修改独享代理连接地址.md)|修改RDS实例独享代理的连接地址。|
|[DeleteDBProxyEndpointAddress](/intl.zh-CN/API 参考/数据库独享代理（读写分离）/删除独享代理连接地址.md)|删除RDS实例独享代理的连接地址。|

## 安全加密

|API|描述|
|---|--|
|[DescribeSecurityGroupConfiguration](/intl.zh-CN/API 参考/安全加密/查询安全组.md)|查询指定RDS实例和ECS安全组的关联信息。|
|[ModifySecurityGroupConfiguration](/intl.zh-CN/API 参考/安全加密/修改安全组.md)|修改指定RDS实例和ECS安全组的关联信息。|
|[DescribeDBInstanceIPArrayList](/intl.zh-CN/API 参考/安全加密/查询IP白名单.md)|查询RDS实例IP白名单。|
|[ModifySecurityIps](/intl.zh-CN/API 参考/安全加密/修改IP白名单.md)|修改IP白名单。|
|[DescribeDBInstanceSSL](/intl.zh-CN/API 参考/安全加密/查询SSL设置.md)|查询实例SSL设置。|
|[ModifyDBInstanceSSL](/intl.zh-CN/API 参考/安全加密/修改SSL设置.md)|修改实例SSL链路。|
|[DescribeDBInstanceTDE](/intl.zh-CN/API 参考/安全加密/查询TDE设置.md)|查询实例数据加密状态。|
|[ModifyDBInstanceTDE](/intl.zh-CN/API 参考/安全加密/开启TDE.md)|开启RDS实例透明数据加密功能。|
|[MigrateSecurityIPMode](/intl.zh-CN/API 参考/安全加密/切换高安全模式.md)|白名单从通用模式切换为高安全模式。|
|[DescribeDBInstanceIpHostname](/intl.zh-CN/API 参考/安全加密/查询底层ECS实例.md)|查询RDS实例的底层ECS实例的hostname。|
|[DescribeDTCSecurityIpHostsForSQLServer](/intl.zh-CN/API 参考/安全加密/查询分布式事务白名单.md)|查询RDS实例的分布式事务白名单信息。|
|[ModifyDTCSecurityIpHostsForSQLServer](/intl.zh-CN/API 参考/安全加密/设置分布式事务白名单.md)|设置分布式事务白名单。|

## 网络

|API|描述|
|---|--|
|[ModifyDBInstanceNetworkType](/intl.zh-CN/API 参考/网络/切换网络类型.md)|切换RDS实例网络类型。|

## 日志

|API|描述|
|---|--|
|[ModifySQLCollectorPolicy](/intl.zh-CN/API 参考/日志/开关SQL洞察（SQL审计）.md)|开启或关闭实例的SQL洞察（SQL审计）功能。|
|[DescribeSQLCollectorPolicy](/intl.zh-CN/API 参考/日志/查询SQL洞察（SQL审计）状态.md)|查询RDS实例的SQL审计或SQL洞察功能是否开启。|
|[DescribeSQLLogRecords](/intl.zh-CN/API 参考/日志/查询SQL洞察（SQL审计）日志.md)|查询实例的SQL洞察（SQL审计）日志。|
|[DescribeSQLLogFiles](/intl.zh-CN/API 参考/日志/查询SQL洞察（SQL审计）列表.md)|查询SQL洞察（SQL审计）文件列表。|
|[ModifySQLCollectorRetention](/intl.zh-CN/API 参考/日志/修改SQL洞察日志保存时长.md)|修改RDS实例的SQL洞察日志保存时长。|
|[DescribeSQLCollectorRetention](/intl.zh-CN/API 参考/日志/查询SQL洞察日志保存时长.md)|查询RDS实例的SQL洞察日志保存时长。|
|[DescribeSlowLogs](/intl.zh-CN/API 参考/日志/查询慢日志统计.md)|查询慢日志统计情况。|
|[DescribeSlowLogRecords](/intl.zh-CN/API 参考/日志/查看慢日志明细.md)|查询实例的慢日志明细。|
|[DescribeErrorLogs](/intl.zh-CN/API 参考/日志/查询错误日志.md)|查询实例某段时间内的错误日志。|
|[PurgeDBInstanceLog](/intl.zh-CN/API 参考/日志/清理日志.md)|清理或收缩RDS实例日志。|

## 备份

|API|描述|
|---|--|
|[CreateBackup](/intl.zh-CN/API 参考/备份/创建备份.md)|创建一个备份集。|
|[DescribeBackups](/intl.zh-CN/API 参考/备份/查看备份列表.md)|查询备份集列表。|
|[DescribeBackupPolicy](/intl.zh-CN/API 参考/备份/查询备份设置.md)|查询实例备份设置。|
|[ModifyBackupPolicy](/intl.zh-CN/API 参考/备份/修改备份设置.md)|修改备份设置。|
|[DeleteBackup](/intl.zh-CN/API 参考/备份/删除数据备份.md)|删除数据备份文件。|
|[DescribeBackupTasks](/intl.zh-CN/API 参考/备份/查询备份任务.md)|查询实例的备份任务列表。|
|[DescribeBinlogFiles](/intl.zh-CN/API 参考/备份/查询Binlog日志.md)|查询Binlog日志。|

## 恢复

|API|描述|
|---|--|
|[RecoveryDBInstance](/intl.zh-CN/API 参考/恢复/恢复数据库.md)|恢复数据库。|
|[CloneDBInstance](/intl.zh-CN/API 参考/恢复/克隆实例.md)|将历史数据恢复至一个新实例（称为克隆实例）。|
|[CreateTempDBInstance](/intl.zh-CN/API 参考/恢复/创建临时实例.md)|创建临时实例。|
|[DescribeLocalAvailableRecoveryTime](/intl.zh-CN/API 参考/恢复/查询备份恢复范围.md)|查询RDS实例备份可恢复的时间范围。|
|[RestoreTable](/intl.zh-CN/API 参考/恢复/单库单表恢复.md)|恢复RDS实例的某些数据库或表到原实例。|

## 跨地域备份恢复

|API|描述|
|---|--|
|[CheckCreateDdrDBInstance](/intl.zh-CN/API 参考/跨地域备份恢复/预检查跨地域备份.md)|预检查某RDS实例是否可以用跨地域备份集进行跨地域恢复。|
|[CreateDdrInstance](/intl.zh-CN/API 参考/跨地域备份恢复/跨地域恢复数据.md)|跨地域恢复数据到新实例。|
|[ModifyInstanceCrossBackupPolicy](/intl.zh-CN/API 参考/跨地域备份恢复/修改跨地域备份设置.md)|修改RDS跨地域备份设置。|
|[DescribeInstanceCrossBackupPolicy](/intl.zh-CN/API 参考/跨地域备份恢复/查询跨地域备份设置.md)|查询跨地域备份设置。|
|[DescribeCrossRegionBackups](/intl.zh-CN/API 参考/跨地域备份恢复/查询跨地域数据备份文件列表.md)|查询某RDS实例跨地域数据备份文件列表。|
|[DescribeCrossRegionLogBackupFiles](/intl.zh-CN/API 参考/跨地域备份恢复/查询跨地域日志备份文件列表.md)|查询跨地域日志备份文件列表。|
|[DescribeAvailableCrossRegion](/intl.zh-CN/API 参考/跨地域备份恢复/查询可用跨地域备份地域.md)|查询所选地域当前可以进行跨地域备份的目的地域。|
|[DescribeAvailableRecoveryTime](/intl.zh-CN/API 参考/跨地域备份恢复/查询跨地域备份可恢复时间段.md)|查询某跨地域备份文件可恢复哪个时间段的数据。|
|[DescribeCrossRegionBackupDBInstance](/intl.zh-CN/API 参考/跨地域备份恢复/查询跨地域备份实例.md)|查询所选地域的哪些实例开启了跨地域备份，以及这些实例的跨地域备份设置。|

## SQL Server备份文件上云

|API|描述|
|---|--|
|[CreateMigrateTask](/intl.zh-CN/API 参考/SQL Server备份文件上云/创建上云任务.md)|将OSS上的备份文件还原到RDS实例，实现数据上云。|
|[DescribeMigrateTasks](/intl.zh-CN/API 参考/SQL Server备份文件上云/查询上云任务.md)|查询备份数据上云任务列表。|
|[DescribeOssDownloads](/intl.zh-CN/API 参考/SQL Server备份文件上云/查询上云任务文件.md)|查询备份数据上云任务的文件详情。|
|[CreateOnlineDatabaseTask](/intl.zh-CN/API 参考/SQL Server备份文件上云/创建打开数据库任务.md)|打开RDS SQL Server备份数据上云任务的数据库。|

## 监控

|API|描述|
|---|--|
|[DescribeResourceUsage](/intl.zh-CN/API 参考/监控/查询空间使用信息.md)|查询实例的空间使用信息。|
|[DescribeDBInstancePerformance](/intl.zh-CN/API 参考/监控/查询性能数据.md)|查询实例性能数据。|
|[DescribeDBInstanceMonitor](/intl.zh-CN/API 参考/监控/查询监控频率.md)|查询监控频率。|
|[ModifyDBInstanceMonitor](/intl.zh-CN/API 参考/监控/修改监控频率.md)|修改监控频率。|

## 参数

|API|描述|
|---|--|
|[DescribeParameters](/intl.zh-CN/API 参考/参数/查询参数配置.md)|查询实例当前的参数配置。|
|[ModifyParameter](/intl.zh-CN/API 参考/参数/修改实例参数.md)|修改实例参数。|
|[DescribeModifyParameterLog](/intl.zh-CN/API 参考/参数/查询参数修改日志.md)|查询RDS实例的参数修改日志。|
|[DescribeParameterTemplates](/intl.zh-CN/API 参考/参数/查询参数模板.md)|查询数据库参数模板。|
|[CreateParameterGroup](/intl.zh-CN/API 参考/参数/创建参数模板.md)|创建RDS参数模板。|
|[ModifyParameterGroup](/intl.zh-CN/API 参考/参数/修改参数模板.md)|修改RDS参数模板。|
|[CloneParameterGroup](/intl.zh-CN/API 参考/参数/复制参数模板.md)|复制RDS参数模板到当前地域或其他地域内。|
|[DescribeParameterGroups](/intl.zh-CN/API 参考/参数/查询参数模板列表.md)|查询目标地域的参数模板列表。|
|[DescribeParameterGroup](/intl.zh-CN/API 参考/参数/查询参数模板信息.md)|查询指定的RDS参数模板信息。|
|[DeleteParameterGroup](/intl.zh-CN/API 参考/参数/删除参数模板.md)|删除RDS参数模板。|

## 数据迁移

|API|描述|
|---|--|
|[ImportDatabaseBetweenInstances](/intl.zh-CN/API 参考/数据迁移/迁入实例.md)|从其它RDS实例迁入数据。|
|[CancelImport](/intl.zh-CN/API 参考/数据迁移/取消迁移任务.md)|取消RDS实例迁移任务。|

## 标签

|API|描述|
|---|--|
|[TagResources](/intl.zh-CN/API 参考/标签/创建标签.md)|为指定的RDS实例创建并绑定标签。|
|[UntagResources](/intl.zh-CN/API 参考/标签/解绑标签.md)|为指定的RDS实例解绑标签。|
|[ListTagResources](/intl.zh-CN/API 参考/标签/查询标签.md)|查询一个或多个RDS实例已经绑定的标签列表。|

