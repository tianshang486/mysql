# API概览 {#doc_api_overview .concept}

云数据库RDS提供以下相关API接口。更多API资源和SDK Demo示例代码，请访问[API Explorer](https://api.aliyun.com)。

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
|[PurgeDBInstanceLog](intl.zh-CN/API参考/实例管理/PurgeDBInstanceLog.md#)|清理或收缩RDS实例日志。|
|[UpgradeDBInstanceEngineVersion](intl.zh-CN/API参考/实例管理/UpgradeDBInstanceEngineVersion.md#)|升级实例数据库版本。|
|[ModifyDBInstanceDescription](intl.zh-CN/API参考/实例管理/ModifyDBInstanceDescription.md#)|修改RDS实例的描述。|
|[ModifyDBInstanceMaintainTime](intl.zh-CN/API参考/实例管理/ModifyDBInstanceMaintainTime.md#)|修改RDS实例可维护时间段。|
|[ModifyDBInstanceHAConfig](intl.zh-CN/API参考/实例管理/ModifyDBInstanceHAConfig.md#)|修改实例的高可用模式和数据复制方式。|
|[SwitchDBInstanceHA](intl.zh-CN/API参考/实例管理/SwitchDBInstanceHA.md#)|切换RDS实例的主备实例。|
|[CreateReadOnlyDBInstance](intl.zh-CN/API参考/实例管理/CreateReadOnlyDBInstance.md#)|为某个实例创建一个只读实例。|

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

## 读写分离 { .section}

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
|[CreateAccount](intl.zh-CN/API参考/账号管理/CreateAccount.md#)|创建管理数据库的账号。|
|[DeleteAccount](intl.zh-CN/API参考/账号管理/DeleteAccount.md#)|删除数据库账号。|
|[DescribeAccounts](intl.zh-CN/API参考/账号管理/DescribeAccounts.md#)|查看实例的帐号信息。|
|[GrantAccountPrivilege](intl.zh-CN/API参考/账号管理/GrantAccountPrivilege.md#)|授权账号访问数据库。|
|[RevokeAccountPrivilege](intl.zh-CN/API参考/账号管理/RevokeAccountPrivilege.md#)|撤销账号对数据库的访问权限。|
|[ModifyAccountDescription](intl.zh-CN/API参考/账号管理/ModifyAccountDescription.md#)|修改数据库账号的描述。|
|[ResetAccountPassword](intl.zh-CN/API参考/账号管理/ResetAccountPassword.md#)|重置账号密码。|
|[ResetAccount](intl.zh-CN/API参考/账号管理/ResetAccount.md#)|重置高权限账号的权限。|

## 安全管理 { .section}

|API|描述|
|---|--|
|[DescribeDBInstanceSSL](intl.zh-CN/API参考/安全管理/DescribeDBInstanceSSL.md#)|查询实例SSL设置。|
|[DescribeDBInstanceIPArrayList](intl.zh-CN/API参考/安全管理/DescribeDBInstanceIPArrayList.md#)|查看RDS实例IP白名单。|
|[DescribeDBInstanceTDE](intl.zh-CN/API参考/安全管理/DescribeDBInstanceTDE.md#)|查询实例数据加密状态。|
|[ModifyDBInstanceSSL](intl.zh-CN/API参考/安全管理/ModifyDBInstanceSSL.md#)|修改实例SSL链路。|
|[ModifyDBInstanceTDE](intl.zh-CN/API参考/安全管理/ModifyDBInstanceTDE.md#)|修改实例数据加密状态。|
|[ModifySecurityIps](intl.zh-CN/API参考/安全管理/ModifySecurityIps.md#)|修改白名单。|
|[MigrateSecurityIPMode](intl.zh-CN/API参考/安全管理/MigrateSecurityIPMode.md#)|把白名单从通用模式切换为高安全模式。|

## 网络管理 { .section}

|API|描述|
|---|--|
|[DescribeDBInstanceNetInfo](intl.zh-CN/API参考/网络管理/DescribeDBInstanceNetInfo.md#)|查看实例的所有连接地址信息。|
|[AllocateInstancePublicConnection](intl.zh-CN/API参考/网络管理/AllocateInstancePublicConnection.md#)|申请实例的外网地址。|
|[ReleaseInstancePublicConnection](intl.zh-CN/API参考/网络管理/ReleaseInstancePublicConnection.md#)|释放实例的外网连接地址。|
|[ModifyDBInstanceNetworkExpireTime](intl.zh-CN/API参考/网络管理/ModifyDBInstanceNetworkExpireTime.md#)|修改连接地址过期时间。|
|[ModifyDBInstanceConnectionString](intl.zh-CN/API参考/网络管理/ModifyDBInstanceConnectionString.md#)|修改实例的连接地址和端口。|
|[ModifyDBInstanceNetworkType](intl.zh-CN/API参考/网络管理/ModifyDBInstanceNetworkType.md#)|切换RDS实例网络类型。|
|[SwitchDBInstanceNetType](intl.zh-CN/API参考/网络管理/SwitchDBInstanceNetType.md#)|切换内外网地址。|

## 日志管理 { .section}

|API|描述|
|---|--|
|[DescribeSlowLogs](intl.zh-CN/API参考/日志管理/DescribeSlowLogs.md#)|查看慢日志统计情况。|
|[DescribeSlowLogRecords](intl.zh-CN/API参考/日志管理/DescribeSlowLogRecords.md#)|查看实例的慢日志明细。|
|[DescribeErrorLogs](intl.zh-CN/API参考/日志管理/DescribeErrorLogs.md#)|查看错误日志。|
|[DescribeBinlogFiles](intl.zh-CN/API参考/日志管理/DescribeBinlogFiles.md#)|查看Binlog日志。|
|[DescribeSQLCollectorPolicy](intl.zh-CN/API参考/日志管理/DescribeSQLCollectorPolicy.md#)|查看实例的SQL采集功能是否打开。|
|[ModifySQLCollectorPolicy](intl.zh-CN/API参考/日志管理/ModifySQLCollectorPolicy.md#)|开启或关闭实例的SQL审计功能。|
|[DescribeSQLLogRecords](intl.zh-CN/API参考/日志管理/DescribeSQLLogRecords.md#)|查询实例的SQL审计日志。|
|[DescribeSQLLogFiles](intl.zh-CN/API参考/日志管理/DescribeSQLLogFiles.md#)|查询SQL审计文件列表。|

## 备份恢复 { .section}

|API|描述|
|---|--|
|[CreateBackup](intl.zh-CN/API参考/备份恢复/CreateBackup.md#)|创建备份集。|
|[CloneDBInstance](intl.zh-CN/API参考/备份恢复/CloneDBInstance.md#)|将历史数据恢复至一个新实例（称为克隆实例）。|
|[DescribeBackups](intl.zh-CN/API参考/备份恢复/DescribeBackups.md#)|查看备份集列表。|
|[DescribeBackupTasks](intl.zh-CN/API参考/备份恢复/DescribeBackupTasks.md#)|查询实例的备份任务列表。|
|[CreateTempDBInstance](intl.zh-CN/API参考/备份恢复/CreateTempDBInstance.md#)|创建临时实例。|
|[DescribeBackupPolicy](intl.zh-CN/API参考/备份恢复/DescribeBackupPolicy.md#)|查看实例备份设置。|
|[ModifyBackupPolicy](intl.zh-CN/API参考/备份恢复/ModifyBackupPolicy.md#)|修改备份设置。|
|[RestoreDBInstance](intl.zh-CN/API参考/备份恢复/RestoreDBInstance.md#)|恢复备份集到原实例（覆盖性恢复）。|
|[DeleteBackup](intl.zh-CN/API参考/备份恢复/DeleteBackup.md#)|删除数据备份文件。|
|[RecoveryDBInstance](intl.zh-CN/API参考/备份恢复/RecoveryDBInstance.md#)|恢复数据库。|
|[DescribeLogBackupFiles](intl.zh-CN/API参考/备份恢复/DescribeLogBackupFiles.md#)|查询实例的日志备份文件。|
|[DescribeBackupDatabase](intl.zh-CN/API参考/备份恢复/DescribeBackupDatabase.md#)|查询备份集下的数据库列表。|

## SQL Server备份文件上云 { .section}

|API|描述|
|---|--|
|[CreateMigrateTask](intl.zh-CN/API参考/SQL Server备份文件上云/CreateMigrateTask.md#)|将OSS上的备份文件还原到RDS实例。|
|[CreateOnlineDatabaseTask](intl.zh-CN/API参考/SQL Server备份文件上云/CreateOnlineDatabaseTask.md#)|打开数据库。|
|[DescribeMigrateTasks](intl.zh-CN/API参考/SQL Server备份文件上云/DescribeMigrateTasks.md#)|查询备份数据上云任务列表。|
|[DescribeOssDownloads](intl.zh-CN/API参考/SQL Server备份文件上云/DescribeOssDownloads.md#)|查看备份数据上云任务的文件详情。|

## 监控管理 { .section}

|API|描述|
|---|--|
|[DescribeResourceUsage](intl.zh-CN/API参考/监控管理/DescribeResourceUsage.md#)|查看实例的空间利用信息。|
|[DescribeDBInstancePerformance](intl.zh-CN/API参考/监控管理/DescribeDBInstancePerformance.md#)|查看实例性能数据。|
|[DescribeDBInstanceMonitor](intl.zh-CN/API参考/监控管理/DescribeDBInstanceMonitor.md#)|查询监控频率。|
|[ModifyDBInstanceMonitor](intl.zh-CN/API参考/监控管理/ModifyDBInstanceMonitor.md#)|修改监控频率。|

## 参数管理 { .section}

|API|描述|
|---|--|
|[DescribeParameterTemplates](intl.zh-CN/API参考/参数管理/DescribeParameterTemplates.md#)|查看数据库参数模板。|
|[DescribeParameters](intl.zh-CN/API参考/参数管理/DescribeParameters.md#)|查询实例当前的参数配置。|
|[ModifyParameter](intl.zh-CN/API参考/参数管理/ModifyParameter.md#)|修改实例参数。|

## 数据迁移 { .section}

|API|描述|
|---|--|
|[CreateUploadPathForSQLServer](intl.zh-CN/API参考/数据迁移/CreateUploadPathForSQLServer.md#)|创建文件服务器的账号、密码以及上传文件的路径信息。|
|[DescribeFilesForSQLServer](intl.zh-CN/API参考/数据迁移/DescribeFilesForSQLServer.md#)|查看文件服务器的文件列表。|
|[DescribeImportsForSQLServer](intl.zh-CN/API参考/数据迁移/DescribeImportsForSQLServer.md#)|查看SQL Server数据库导入列表以及导入任务情况|
|[ImportDatabaseBetweenInstances](intl.zh-CN/API参考/数据迁移/ImportDatabaseBetweenInstances.md#)|从其它RDS实例迁入数据。|
|[CancelImport](intl.zh-CN/API参考/数据迁移/CancelImport.md#)|取消RDS实例迁移任务。|

## 标签管理 { .section}

|API|描述|
|---|--|
|[AddTagsToResource](intl.zh-CN/API参考/标签管理/AddTagsToResource.md#)|为RDS实例绑定标签。|
|[DescribeTags](intl.zh-CN/API参考/标签管理/DescribeTags.md#)|查询RDS实例的标签。|
|[RemoveTagsFromResource](intl.zh-CN/API参考/标签管理/RemoveTagsFromResource.md#)|解绑RDS实例的标签。|

