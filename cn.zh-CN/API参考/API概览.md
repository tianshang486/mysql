# API概览 {#doc_api_overview .concept}

云数据库RDS提供以下相关API接口。

## 实例管理 { .section}

|API|描述|
|---|--|
| [CreateDBInstance](~~8086#Rds_CreateDBInstance~~)

 |创建RDS实例。|
| [DeleteDBInstance](~~8087#Rds_DeleteDBInstance~~)

 |释放RDS实例。|
| [RestartDBInstance](~~8088#Rds_RestartDBInstance~~)

 |重启RDS实例。|
| [RenewInstance](~~8084#Rds_RenewInstance~~)

 |续费RDS实例。|
| [DescribeDBInstanceAttribute](~~8089#Rds_DescribeDBInstanceAttribute~~)

 |查看RDS实例的详细信息。|
| [DescribeDBInstances](~~8090#Rds_DescribeDBInstances~~)

 |查看RDS实例列表或被RAM授权的实例列表。|
| [ModifyDBInstanceSpec](~~8091#Rds_ModifyDBInstanceSpec~~)

 |变更RDS实例的规格或存储空间。|
| [DescribeRegions](~~8093#Rds_DescribeRegions~~)

 |查询当前可选的RDS地域和可用区信息。|
| [DescribeDBInstanceHAConfig](~~8094#Rds_DescribeDBInstanceHAConfig~~)

 |查询RDS实例高可用模式和数据复制方式。|
| [MigrateToOtherZone](~~8095#Rds_MigrateToOtherZone~~)

 |将RDS实例迁移至其他可用区。|
| [PurgeDBInstanceLog](~~8096#Rds_PurgeDBInstanceLog~~)

 |清理或收缩RDS实例日志。|
| [UpgradeDBInstanceEngineVersion](~~8097#Rds_UpgradeDBInstanceEngineVersion~~)

 |升级实例数据库版本。|
| [ModifyDBInstanceDescription](~~8098#Rds_ModifyDBInstanceDescription~~)

 |修改RDS实例的描述。|
| [ModifyDBInstanceMaintainTime](~~8099#Rds_ModifyDBInstanceMaintainTime~~)

 |修改RDS实例可维护时间段。|
| [ModifyDBInstanceHAConfig](~~8100#Rds_ModifyDBInstanceHAConfig~~)

 |修改实例的高可用模式和数据复制方式。|
| [SwitchDBInstanceHA](~~8101#Rds_SwitchDBInstanceHA~~)

 |切换RDS实例的主备实例。|
| [CreateReadOnlyDBInstance](~~8102#Rds_CreateReadOnlyDBInstance~~)

 |为某个实例创建一个只读实例。|

## CloudDBA数据库性能优化 { .section}

|API|描述|
|---|--|
| [CreateDiagnosticReport](~~8104#Rds_CreateDiagnosticReport~~)

 |创建诊断报告。|
| [DescribeDiagnosticReportList](~~8105#Rds_DescribeDiagnosticReportList~~)

 |获取诊断报告列表。|

## 数据库管理 { .section}

|API|描述|
|---|--|
| [ModifyCollationTimeZone](~~21290#Rds_ModifyCollationTimeZone~~)

 |修改系统库的字符集排序规则和时区。|
| [CreateDatabase](~~8112#Rds_CreateDatabase~~)

 |创建数据库。|
| [DeleteDatabase](~~8113#Rds_DeleteDatabase~~)

 |删除数据库。|
| [DescribeDatabases](~~8114#Rds_DescribeDatabases~~)

 |查看数据库信息。|
| [ModifyDBDescription](~~8115#Rds_ModifyDBDescription~~)

 |修改数据库备注。|
| [CopyDatabase](~~8116#Rds_CopyDatabase~~)

 |复制SQL Server 2008 R2版数据库。|
| [CopyDatabaseBetweenInstances](~~18619#Rds_CopyDatabaseBetweenInstances~~)

 |在实例间复制数据库。|
| [DescribeCollationTimeZones](~~41886#Rds_DescribeCollationTimeZones~~)

 |查看支持的字符集排序规则和时区。|

## 数据库代理 { .section}

|API|描述|
|---|--|
| [ModifyDBInstanceConnectionMode](~~8092#Rds_ModifyDBInstanceConnectionMode~~)

 |ModifyDBInstanceConnectionMode|
| [ModifyDBInstanceProxyConfiguration](~~16813#Rds_ModifyDBInstanceProxyConfiguration~~)

 |设置数据库代理。|
| [DescribeDBInstanceProxyConfiguration](~~16812#Rds_DescribeDBInstanceProxyConfiguration~~)

 |查看数据库代理设置。|
| [AllocateReadWriteSplittingConnection](~~8107#Rds_AllocateReadWriteSplittingConnection~~)

 |申请读写分离地址。|
| [CalculateDBInstanceWeight](~~8108#Rds_CalculateDBInstanceWeight~~)

 |查询系统权重分配值。|
| [ModifyReadWriteSplittingConnection](~~8109#Rds_ModifyReadWriteSplittingConnection~~)

 |修改读写分离链路的延迟阈值和各个实例的读权重。|
| [ReleaseReadWriteSplittingConnection](~~8110#Rds_ReleaseReadWriteSplittingConnection~~)

 |释放读写分离地址。|

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

