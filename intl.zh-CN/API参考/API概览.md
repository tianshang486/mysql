# API概览 {#doc_api_overview .concept}

云数据库RDS提供以下相关API接口。

## 实例管理 { .section}

|API|描述|
|---|--|
|[CreateDBInstance](intl.zh-CN/API参考/实例管理/CreateDBInstance.md#)|创建RDS实例。|
|[DeleteDBInstance](intl.zh-CN/API参考/实例管理/DeleteDBInstance.md#)|释放RDS实例。|
|[RestartDBInstance](intl.zh-CN/API参考/实例管理/RestartDBInstance.md#)|重启RDS实例。|
|[RenewInstance](intl.zh-CN/API参考/实例管理/RenewInstance.md#)|续费RDS实例。|
|[DescribeDBInstanceAttribute](intl.zh-CN/API参考/实例管理/DescribeDBInstanceAttribute.md#)|查看RDS实例的详细信息。|
|[DescribeDBInstances](intl.zh-CN/API参考/实例管理/DescribeDBInstances.md#)|查看RDS实例列表或被RAM授权的实例列表。|
|[ModifyDBInstanceSpec](intl.zh-CN/API参考/实例管理/ModifyDBInstanceSpec.md#)|变更RDS实例的规格或存储空间。|
|[DescribeRegions](intl.zh-CN/API参考/实例管理/DescribeRegions.md#)|查询当前可选的RDS地域和可用区信息。|
|[DescribeDBInstanceHAConfig](intl.zh-CN/API参考/实例管理/DescribeDBInstanceHAConfig.md#)|查询RDS实例高可用模式和数据复制方式。|
|[MigrateToOtherZone](intl.zh-CN/API参考/实例管理/MigrateToOtherZone.md#)|将RDS实例迁移至其他可用区。|
| [PurgeDBInstanceLog](~~8096#Rds_PurgeDBInstanceLog~~)

 |清理或收缩RDS实例日志。|
|[UpgradeDBInstanceEngineVersion](intl.zh-CN/API参考/实例管理/UpgradeDBInstanceEngineVersion.md#)|升级实例数据库版本。|
|[ModifyDBInstanceDescription](intl.zh-CN/API参考/实例管理/ModifyDBInstanceDescription.md#)|修改RDS实例的描述。|
|[ModifyDBInstanceMaintainTime](intl.zh-CN/API参考/实例管理/ModifyDBInstanceMaintainTime.md#)|修改RDS实例可维护时间段。|
|[ModifyDBInstanceHAConfig](intl.zh-CN/API参考/实例管理/ModifyDBInstanceHAConfig.md#)|修改实例的高可用模式和数据复制方式。|
|[SwitchDBInstanceHA](intl.zh-CN/API参考/实例管理/SwitchDBInstanceHA.md#)|切换RDS实例的主备实例。|
|[CreateReadOnlyDBInstance](intl.zh-CN/API参考/实例管理/CreateReadOnlyDBInstance.md#)|为某个实例创建一个只读实例。|

## CloudDBA数据库性能优化 { .section}

|API|描述|
|---|--|
|[CreateDiagnosticReport](intl.zh-CN/API参考/CloudDBA数据库性能优化/CreateDiagnosticReport.md#)|创建诊断报告。|
|[DescribeDiagnosticReportList](intl.zh-CN/API参考/CloudDBA数据库性能优化/DescribeDiagnosticReportList.md#)|获取诊断报告列表。|

## 数据库管理 { .section}

|API|描述|
|---|--|
|[ModifyCollationTimeZone](intl.zh-CN/API参考/数据库管理/ModifyCollationTimeZone.md#)|修改系统库的字符集排序规则和时区。|
|[CreateDatabase](intl.zh-CN/API参考/数据库管理/CreateDatabase.md#)|创建数据库。|
|[DeleteDatabase](intl.zh-CN/API参考/数据库管理/DeleteDatabase.md#)|删除数据库。|
|[DescribeDatabases](intl.zh-CN/API参考/数据库管理/DescribeDatabases.md#)|查看数据库信息。|
|[ModifyDBDescription](intl.zh-CN/API参考/数据库管理/ModifyDBDescription.md#)|修改数据库备注。|
|[CopyDatabase](intl.zh-CN/API参考/数据库管理/CopyDatabase.md#)|复制SQL Server 2008 R2版数据库。|
|[CopyDatabaseBetweenInstances](intl.zh-CN/API参考/数据库管理/CopyDatabaseBetweenInstances.md#)|在实例间复制数据库。|
|[DescribeCollationTimeZones](intl.zh-CN/API参考/数据库管理/DescribeCollationTimeZones.md#)|查看支持的字符集排序规则和时区。|

## 数据库代理 { .section}

|API|描述|
|---|--|
|[ModifyDBInstanceProxyConfiguration](intl.zh-CN/API参考/数据库代理/ModifyDBInstanceProxyConfiguration.md#)|设置数据库代理。|
|[DescribeDBInstanceProxyConfiguration](intl.zh-CN/API参考/数据库代理/DescribeDBInstanceProxyConfiguration.md#)|查看数据库代理设置。|
|[AllocateReadWriteSplittingConnection](intl.zh-CN/API参考/数据库代理/AllocateReadWriteSplittingConnection.md#)|申请读写分离地址。|
|[CalculateDBInstanceWeight](intl.zh-CN/API参考/数据库代理/CalculateDBInstanceWeight.md#)|查询系统权重分配值。|
|[ModifyReadWriteSplittingConnection](intl.zh-CN/API参考/数据库代理/ModifyReadWriteSplittingConnection.md#)|修改读写分离链路的延迟阈值和各个实例的读权重。|
|[ReleaseReadWriteSplittingConnection](intl.zh-CN/API参考/数据库代理/ReleaseReadWriteSplittingConnection.md#)|释放读写分离地址。|

## 账号管理 { .section}

|API|描述|
|---|--|
| [CreateAccount](~~8118#Rds_CreateAccount~~)

 |创建管理数据库的账号。|
| [DeleteAccount](~~8119#Rds_DeleteAccount~~)

 |删除数据库账号。|
| [DescribeAccounts](~~8120#Rds_DescribeAccounts~~)

 |查看实例的帐号信息。|
| [GrantAccountPrivilege](~~8121#Rds_GrantAccountPrivilege~~)

 |授权账号访问数据库。|
| [RevokeAccountPrivilege](~~8122#Rds_RevokeAccountPrivilege~~)

 |撤销账号对数据库的访问权限。|
| [ModifyAccountDescription](~~8123#Rds_ModifyAccountDescription~~)

 |修改数据库账号的描述。|
| [ResetAccountPassword](~~8124#Rds_ResetAccountPassword~~)

 |重置账号密码。|
| [ResetAccount](~~8125#Rds_ResetAccount~~)

 |重置高权限账号的权限。|

## 安全管理 { .section}

|API|描述|
|---|--|
| [DescribeDBInstanceSSL](~~8128#Rds_DescribeDBInstanceSSL~~)

 |查询实例SSL设置。|
| [DescribeDBInstanceIPArrayList](~~8127#Rds_DescribeDBInstanceIPArrayList~~)

 |查看RDS实例IP白名单。|
| [DescribeDBInstanceTDE](~~8129#Rds_DescribeDBInstanceTDE~~)

 |查询实例数据加密状态。|
| [ModifyDBInstanceSSL](~~8130#Rds_ModifyDBInstanceSSL~~)

 |修改实例SSL链路。|
| [ModifyDBInstanceTDE](~~8131#Rds_ModifyDBInstanceTDE~~)

 |修改实例数据加密状态。|
| [ModifySecurityIps](~~8132#Rds_ModifySecurityIps~~)

 |修改白名单。|
| [MigrateSecurityIPMode](~~17783#Rds_MigrateSecurityIPMode~~)

 |把白名单从通用模式切换为高安全模式。|

## 网络管理 { .section}

|API|描述|
|---|--|
| [DescribeDBInstanceNetInfo](~~8135#Rds_DescribeDBInstanceNetInfo~~)

 |查看实例的所有连接地址信息。|
| [AllocateInstancePublicConnection](~~8134#Rds_AllocateInstancePublicConnection~~)

 |申请实例的外网地址。|
| [ReleaseInstancePublicConnection](~~8139#Rds_ReleaseInstancePublicConnection~~)

 |释放实例的外网连接地址。|
| [ModifyDBInstanceNetworkExpireTime](~~8137#Rds_ModifyDBInstanceNetworkExpireTime~~)

 |修改连接地址过期时间。|
| [ModifyDBInstanceConnectionString](~~8136#Rds_ModifyDBInstanceConnectionString~~)

 |修改实例的连接地址和端口。|
| [ModifyDBInstanceNetworkType](~~8138#Rds_ModifyDBInstanceNetworkType~~)

 |切换RDS实例网络类型。|
| [SwitchDBInstanceNetType](~~8140#Rds_SwitchDBInstanceNetType~~)

 |切换内外网地址。|

## 日志管理 { .section}

|API|描述|
|---|--|
| [DescribeSlowLogs](~~8142#Rds_DescribeSlowLogs~~)

 |查看慢日志统计情况。|
| [DescribeSlowLogRecords](~~8143#Rds_DescribeSlowLogRecords~~)

 |查看实例的慢日志明细。|
| [DescribeErrorLogs](~~8144#Rds_DescribeErrorLogs~~)

 |查看错误日志。|
| [DescribeBinlogFiles](~~8145#Rds_DescribeBinlogFiles~~)

 |查看Binlog日志。|
|[DescribeSQLCollectorPolicy](intl.zh-CN/API参考/日志管理/DescribeSQLCollectorPolicy.md#)|查看实例的SQL采集功能是否打开。|
| [ModifySQLCollectorPolicy](~~8147#Rds_ModifySQLCollectorPolicy~~)

 |开启或关闭实例的SQL审计功能。|
| [DescribeSQLLogRecords](~~8148#Rds_DescribeSQLLogRecords~~)

 |查询实例的SQL审计日志。|
| [DescribeSQLLogFiles](~~8149#Rds_DescribeSQLLogFiles~~)

 |查询SQL审计文件列表。|

## 备份恢复 { .section}

|API|描述|
|---|--|
| [CreateBackup](~~8151#Rds_CreateBackup~~)

 |创建备份集。|
| [CloneDBInstance](~~8152#Rds_CloneDBInstance~~)

 |将历史数据恢复至一个新实例（称为克隆实例）。|
| [DescribeBackups](~~8153#Rds_DescribeBackups~~)

 |查看备份集列表。|
|[DescribeBackupTasks](intl.zh-CN/API参考/备份恢复/DescribeBackupTasks.md#)|查询实例的备份任务列表。|
| [CreateTempDBInstance](~~8154#Rds_CreateTempDBInstance~~)

 |创建临时实例。|
| [DescribeBackupPolicy](~~8155#Rds_DescribeBackupPolicy~~)

 |查看实例备份设置。|
| [ModifyBackupPolicy](~~8156#Rds_ModifyBackupPolicy~~)

 |修改备份设置。|
| [RestoreDBInstance](~~8157#Rds_RestoreDBInstance~~)

 |恢复备份集到原实例（覆盖性恢复）。|
| [DeleteBackup](~~8158#Rds_DeleteBackup~~)

 |删除数据备份文件。|
| [RecoveryDBInstance](~~15241#Rds_RecoveryDBInstance~~)

 |恢复数据库。|
| [DescribeLogBackupFiles](~~21114#Rds_DescribeLogBackupFiles~~)

 |查询实例的日志备份文件。|
| [DescribeBackupDatabase](~~41885#Rds_DescribeBackupDatabase~~)

 |查询备份集下的数据库列表。|

## SQL Server备份文件上云 { .section}

|API|描述|
|---|--|
| [CreateMigrateTask](~~8160#Rds_CreateMigrateTask~~)

 |将OSS上的备份文件还原到RDS实例。|
|[CreateOnlineDatabaseTask](intl.zh-CN/API参考/SQL Server备份文件上云/CreateOnlineDatabaseTask.md#)|打开数据库。|
| [DescribeMigrateTasks](~~8161#Rds_DescribeMigrateTasks~~)

 |查询备份数据上云任务列表。|
| [DescribeOssDownloads](~~8162#Rds_DescribeOssDownloads~~)

 |查看备份数据上云任务的文件详情。|

## 监控管理 { .section}

|API|描述|
|---|--|
| [DescribeResourceUsage](~~8164#Rds_DescribeResourceUsage~~)

 |查看实例的空间利用信息。|
| [DescribeDBInstancePerformance](~~8165#Rds_DescribeDBInstancePerformance~~)

 |查看实例性能数据。|
| [DescribeDBInstanceMonitor](~~8166#Rds_DescribeDBInstanceMonitor~~)

 |查询监控频率。|
| [ModifyDBInstanceMonitor](~~8167#Rds_ModifyDBInstanceMonitor~~)

 |修改监控频率。|

## 参数管理 { .section}

|API|描述|
|---|--|
| [DescribeParameterTemplates](~~8169#Rds_DescribeParameterTemplates~~)

 |查看数据库参数模板。|
| [DescribeParameters](~~8170#Rds_DescribeParameters~~)

 |查询实例当前的参数配置。|
| [ModifyParameter](~~8171#Rds_ModifyParameter~~)

 |修改实例参数。|

## 数据迁移 { .section}

|API|描述|
|---|--|
|[CreateUploadPathForSQLServer](intl.zh-CN/API参考/数据迁移/CreateUploadPathForSQLServer.md#)|创建文件服务器的账号、密码以及上传文件的路径信息。|
|[DescribeFilesForSQLServer](intl.zh-CN/API参考/数据迁移/DescribeFilesForSQLServer.md#)|查看文件服务器的文件列表。|
|[DescribeImportsForSQLServer](intl.zh-CN/API参考/数据迁移/DescribeImportsForSQLServer.md#)|查看SQL Server数据库导入列表以及导入任务情况|
| [ImportDatabaseBetweenInstances](~~8176#Rds_ImportDatabaseBetweenInstances~~)

 |从其它RDS实例迁入数据。|
| [CancelImport](~~8177#Rds_CancelImport~~)

 |取消RDS实例迁移任务。|

## 标签管理 { .section}

|API|描述|
|---|--|
| [AddTagsToResource](~~8179#Rds_AddTagsToResource~~)

 |为RDS实例绑定标签。|
| [DescribeTags](~~8180#Rds_DescribeTags~~)

 |查询RDS实例的标签。|
| [RemoveTagsFromResource](~~8181#Rds_RemoveTagsFromResource~~)

 |解绑RDS实例的标签。|

