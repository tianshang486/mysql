# API概览 {#doc_8073 .concept}

云数据库 MySQL 版提供以下相关API接口。

## 使用API {#section_02o_2bw_wgk .section}

|API|描述|
|---|--|
|[请求结构](cn.zh-CN/API参考/使用API/请求结构.md)|请求结构|

## 实例管理 {#section_l1z_kc0_1z4 .section}

|API|描述|
|---|--|
|[DestroyDBInstance](cn.zh-CN/API参考/实例管理/DestroyDBInstance.md)|该接口用于销毁RDS实例，已下线。|
|[ModifyDBInstanceDelayReplicationTime](cn.zh-CN/API参考/实例管理/ModifyDBInstanceDelayReplicationTime.md)|该接口用于修改只读实例延迟时间，已下线。|
|[CreateDBInstance](cn.zh-CN/API参考/实例管理/CreateDBInstance.md)|调用CreateDBInstance接口创建一个RDS实例。|
|[DeleteDBInstance](cn.zh-CN/API参考/实例管理/DeleteDBInstance.md)|调用DeleteDBInstance接口释放RDS实例。|
|[RestartDBInstance](cn.zh-CN/API参考/实例管理/RestartDBInstance.md)|调用RestartDBInstance接口重启RDS实例。|
|[RenewInstance](cn.zh-CN/API参考/实例管理/RenewInstance.md)|调用RenewInstance接口对RDS实例进行手动续费。|
|[DescribeDBInstanceAttribute](cn.zh-CN/API参考/实例管理/DescribeDBInstanceAttribute.md)|调用DescribeDBInstanceAttribute接口查看RDS实例的详细信息。|
|[DescribeDBInstances](cn.zh-CN/API参考/实例管理/DescribeDBInstances.md)|调用DescribeDBInstances接口查看RDS实例列表或被RAM授权的实例列表。|
|[ModifyDBInstanceSpec](cn.zh-CN/API参考/实例管理/ModifyDBInstanceSpec.md)|调用ModifyDBInstanceSpec接口变更RDS实例（包括常规实例和只读实例，不包括灾备实例和临时实例）的规格或存储空间。|
|[DescribeRegions](cn.zh-CN/API参考/实例管理/DescribeRegions.md)|调用DescribeRegions接口查询当前可选的RDS地域和可用区信息。|
|[DescribeDBInstanceHAConfig](cn.zh-CN/API参考/实例管理/DescribeDBInstanceHAConfig.md)|调用DescribeDBInstanceHAConfig接口查询RDS实例高可用模式和数据复制方式。|
|[MigrateToOtherZone](cn.zh-CN/API参考/实例管理/MigrateToOtherZone.md)|调用MigrateToOtherZone接口将RDS实例迁移至其他可用区。|
|[PurgeDBInstanceLog](cn.zh-CN/API参考/实例管理/PurgeDBInstanceLog.md)|调用PurgeDBInstanceLog接口清理或收缩RDS实例日志。|
|[UpgradeDBInstanceEngineVersion](cn.zh-CN/API参考/实例管理/UpgradeDBInstanceEngineVersion.md)|调用UpgradeDBInstanceEngineVersion接口升级实例数据库版本。|
|[ModifyDBInstanceDescription](cn.zh-CN/API参考/实例管理/ModifyDBInstanceDescription.md)|调用ModifyDBInstanceDescription接口修改RDS实例的描述。|
|[ModifyDBInstanceMaintainTime](cn.zh-CN/API参考/实例管理/ModifyDBInstanceMaintainTime.md)|调用ModifyDBInstanceMaintainTime接口修改RDS实例可维护时间段。|
|[ModifyDBInstanceHAConfig](cn.zh-CN/API参考/实例管理/ModifyDBInstanceHAConfig.md)|调用ModifyDBInstanceHAConfig接口修改实例的高可用模式和数据复制方式。|
|[SwitchDBInstanceHA](cn.zh-CN/API参考/实例管理/SwitchDBInstanceHA.md)|调用SwitchDBInstanceHA接口切换RDS实例的主备实例。|
|[CreateReadOnlyDBInstance](cn.zh-CN/API参考/实例管理/CreateReadOnlyDBInstance.md)|调用CreateReadOnlyDBInstance接口为某个实例创建一个只读实例。|
|[ModifyDBInstanceAutoUpgradeMinorVersion](cn.zh-CN/API参考/实例管理/ModifyDBInstanceAutoUpgradeMinorVersion.md)|调用ModifyDBInstanceAutoUpgradeMinorVersion接口修改RDS实例升级小版本的方式。|

## 历史事件 {#section_q96_bib_mvw .section}

|API|描述|
|---|--|
|[DescribeEvents](cn.zh-CN/API参考/历史事件/DescribeEvents.md)|调用DescribeEvents接口查询RDS事件记录列表。|
|[DescribeActionEventPolicy](cn.zh-CN/API参考/历史事件/DescribeActionEventPolicy.md)|调用DescribeActionEventPolicy接口查看RDS历史事件功能开启情况。|
|[ModifyActionEventPolicy](cn.zh-CN/API参考/历史事件/ModifyActionEventPolicy.md)|调用ModifyActionEventPolicy接口开启或关闭RDS历史事件功能。|

## CloudDBA数据库性能优化 {#section_syp_lke_erq .section}

|API|描述|
|---|--|
|[CreateDiagnosticReport](cn.zh-CN/API参考/CloudDBA数据库性能优化/CreateDiagnosticReport.md)|调用CreateDiagnosticReport接口创建诊断报告。|
|[DescribeDiagnosticReportList](cn.zh-CN/API参考/CloudDBA数据库性能优化/DescribeDiagnosticReportList.md)|调用DescribeDiagnosticReportList接口获取诊断报告列表。|

## 数据库管理 {#section_jpq_y7x_jjq .section}

|API|描述|
|---|--|
|[ModifyCollationTimeZone](cn.zh-CN/API参考/数据库管理/ModifyCollationTimeZone.md)|调用ModifyCollationTimeZone接口修改系统库的字符集排序规则和时区，已下线。|
|[CreateDatabase](cn.zh-CN/API参考/数据库管理/CreateDatabase.md)|调用CreateDatabase接口在某个实例下创建数据库。|
|[DeleteDatabase](cn.zh-CN/API参考/数据库管理/DeleteDatabase.md)|调用DeleteDatabase接口删除实例下的某个数据库。|
|[DescribeDatabases](cn.zh-CN/API参考/数据库管理/DescribeDatabases.md)|调用DescribeDatabases接口查看实例下的数据库信息。|
|[ModifyDBDescription](cn.zh-CN/API参考/数据库管理/ModifyDBDescription.md)|调用ModifyDBDescription接口修改数据库备注。|
|[CopyDatabase](cn.zh-CN/API参考/数据库管理/CopyDatabase.md)|调用CopyDatabase接口复制数据库SQL Server 2008 R2版，已下线。|
|[CopyDatabaseBetweenInstances](cn.zh-CN/API参考/数据库管理/CopyDatabaseBetweenInstances.md)|调用CopyDatabaseBetweenInstances接口在实例间复制数据库。|
|[DescribeCollationTimeZones](cn.zh-CN/API参考/数据库管理/DescribeCollationTimeZones.md)|调用DescribeCollationTimeZones接口查看支持的字符集排序规则和时区。|

## 数据库代理 {#section_lg2_4tn_kij .section}

|API|描述|
|---|--|
|[ModifyDBInstanceConnectionMode](cn.zh-CN/API参考/数据库代理/ModifyDBInstanceConnectionMode.md)|调用ModifyDBInstanceConnectionMode接口开启或关闭数据库代理，已下线。|
|[ModifyDBInstanceProxyConfiguration](cn.zh-CN/API参考/数据库代理/ModifyDBInstanceProxyConfiguration.md)|调用ModifyDBInstanceProxyConfiguration接口设置数据库代理，已下线。|
|[DescribeDBInstanceProxyConfiguration](cn.zh-CN/API参考/数据库代理/DescribeDBInstanceProxyConfiguration.md)|调用DescribeDBInstanceProxyConfiguration接口查看数据库代理设置，已下线。|
|[AllocateReadWriteSplittingConnection](cn.zh-CN/API参考/数据库代理/AllocateReadWriteSplittingConnection.md)|调用AllocateReadWriteSplittingConnection接口申请读写分离地址。|
|[CalculateDBInstanceWeight](cn.zh-CN/API参考/数据库代理/CalculateDBInstanceWeight.md)|调用CalculateDBInstanceWeight接口查询系统权重分配值。|
|[ModifyReadWriteSplittingConnection](cn.zh-CN/API参考/数据库代理/ModifyReadWriteSplittingConnection.md)|调用ModifyReadWriteSplittingConnection接口修改读写分离链路的延迟阈值和各个实例的读权重。|
|[ReleaseReadWriteSplittingConnection](cn.zh-CN/API参考/数据库代理/ReleaseReadWriteSplittingConnection.md)|调用ReleaseReadWriteSplittingConnection接口释放读写分离地址。|

## 账号管理 {#section_f1s_nif_bxy .section}

|API|描述|
|---|--|
|[CreateAccount](cn.zh-CN/API参考/账号管理/CreateAccount.md)|调用CreateAccount接口创建管理数据库的账号。|
|[DeleteAccount](cn.zh-CN/API参考/账号管理/DeleteAccount.md)|调用DeleteAccount接口删除数据库账号。|
|[DescribeAccounts](cn.zh-CN/API参考/账号管理/DescribeAccounts.md)|调用DescribeAccounts接口查看实例的帐号信息。|
|[GrantAccountPrivilege](cn.zh-CN/API参考/账号管理/GrantAccountPrivilege.md)|调用GrantAccountPrivilege接口授权账号访问数据库。|
|[RevokeAccountPrivilege](cn.zh-CN/API参考/账号管理/RevokeAccountPrivilege.md)|调用RevokeAccountPrivilege接口撤销账号对数据库的访问权限。|
|[ModifyAccountDescription](cn.zh-CN/API参考/账号管理/ModifyAccountDescription.md)|调用ModifyAccountDescription接口修改数据库账号的描述。|
|[ResetAccountPassword](cn.zh-CN/API参考/账号管理/ResetAccountPassword.md)|调用ResetAccountPassword接口重置账号密码。|
|[ResetAccount](cn.zh-CN/API参考/账号管理/ResetAccount.md)|调用ResetAccount接口重置高权限账号的权限。|

## 安全管理 {#section_akw_ycs_cwa .section}

|API|描述|
|---|--|
|[DescribeDBInstanceIPArrayList](cn.zh-CN/API参考/安全管理/DescribeDBInstanceIPArrayList.md)|调用DescribeDBInstanceIPArrayList接口查看RDS实例IP白名单。|
|[DescribeDBInstanceSSL](cn.zh-CN/API参考/安全管理/DescribeDBInstanceSSL.md)|调用DescribeDBInstanceSSL接口查询实例SSL设置。|
|[DescribeDBInstanceTDE](cn.zh-CN/API参考/安全管理/DescribeDBInstanceTDE.md)|调用DescribeDBInstanceTDE接口查询实例数据加密状态。|
|[ModifyDBInstanceSSL](cn.zh-CN/API参考/安全管理/ModifyDBInstanceSSL.md)|调用ModifyDBInstanceSSL接口修改实例SSL链路。|
|[ModifyDBInstanceTDE](cn.zh-CN/API参考/安全管理/ModifyDBInstanceTDE.md)|调用ModifyDBInstanceTDE接口修改实例数据加密状态。|
|[ModifySecurityIps](cn.zh-CN/API参考/安全管理/ModifySecurityIps.md)|调用ModifySecurityIps接口修改白名单。|
|[MigrateSecurityIPMode](cn.zh-CN/API参考/安全管理/MigrateSecurityIPMode.md)|调用MigrateSecurityIPMode接口把白名单从通用模式切换为高安全模式。|
|[DescribeDBInstanceIpHostname](cn.zh-CN/API参考/安全管理/DescribeDBInstanceIpHostname.md)|调用DescribeDBInstanceIpHostname接口查询RDS实例的底层ECS实例的hostname。|
|[DescribeDTCSecurityIpHostsForSQLServer](cn.zh-CN/API参考/安全管理/DescribeDTCSecurityIpHostsForSQLServer.md)|调用DescribeDTCSecurityIpHostsForSQLServer接口查询RDS实例的分布式事务白名单信息。|
|[ModifyDTCSecurityIpHostsForSQLServer](cn.zh-CN/API参考/安全管理/ModifyDTCSecurityIpHostsForSQLServer.md)|调用ModifyDTCSecurityIpHostsForSQLServer接口设置分布式事务白名单。|

## 网络管理 {#section_cdk_ros_ryb .section}

|API|描述|
|---|--|
|[AllocateInstancePublicConnection](cn.zh-CN/API参考/网络管理/AllocateInstancePublicConnection.md)|调用AllocateInstancePublicConnection接口申请实例的外网地址。|
|[DescribeDBInstanceNetInfo](cn.zh-CN/API参考/网络管理/DescribeDBInstanceNetInfo.md)|调用DescribeDBInstanceNetInfo接口查看实例的所有连接地址信息。|
|[ModifyDBInstanceNetworkExpireTime](cn.zh-CN/API参考/网络管理/ModifyDBInstanceNetworkExpireTime.md)|调用ModifyDBInstanceNetworkExpireTime接口修改连接地址过期时间。|
|[ModifyDBInstanceConnectionString](cn.zh-CN/API参考/网络管理/ModifyDBInstanceConnectionString.md)|调用ModifyDBInstanceConnectionString接口修改实例的连接地址和端口。|
|[ModifyDBInstanceNetworkType](cn.zh-CN/API参考/网络管理/ModifyDBInstanceNetworkType.md)|调用ModifyDBInstanceNetworkType接口切换RDS实例网络类型。|
|[ReleaseInstancePublicConnection](cn.zh-CN/API参考/网络管理/ReleaseInstancePublicConnection.md)|调用ReleaseInstancePublicConnection接口释放实例的外网连接地址。|
|[SwitchDBInstanceNetType](cn.zh-CN/API参考/网络管理/SwitchDBInstanceNetType.md)|调用SwitchDBInstanceNetType接口切换内外网地址。|

## 日志管理 {#section_jsv_epf_qbf .section}

|API|描述|
|---|--|
|[DescribeSlowLogs](cn.zh-CN/API参考/日志管理/DescribeSlowLogs.md)|调用DescribeSlowLogs查看慢日志统计情况。|
|[DescribeSlowLogRecords](cn.zh-CN/API参考/日志管理/DescribeSlowLogRecords.md)|调用DescribeSlowLogRecords接口查看实例的慢日志明细。|
|[DescribeErrorLogs](cn.zh-CN/API参考/日志管理/DescribeErrorLogs.md)|调用DescribeErrorLogs接口查看实例某段时间内的错误日志。|
|[DescribeBinlogFiles](cn.zh-CN/API参考/日志管理/DescribeBinlogFiles.md)|调用DescribeBinlogFiles接口查看Binlog日志。|
|[ModifySQLCollectorPolicy](cn.zh-CN/API参考/日志管理/ModifySQLCollectorPolicy.md)|调用ModifySQLCollectorPolicy接口开启或关闭实例的SQL审计功能。|
|[DescribeSQLLogRecords](cn.zh-CN/API参考/日志管理/DescribeSQLLogRecords.md)|调用DescribeSQLLogRecords接口查询实例的SQL审计日志。|
|[DescribeSQLLogFiles](cn.zh-CN/API参考/日志管理/DescribeSQLLogFiles.md)|调用DescribeSQLLogFiles接口查询SQL审计文件列表。|

## 备份恢复 {#section_88t_vnj_qza .section}

|API|描述|
|---|--|
|[CreateBackup](cn.zh-CN/API参考/备份恢复/CreateBackup.md)|调用CreateBackup接口为实例创建一个备份集。|
|[CloneDBInstance](cn.zh-CN/API参考/备份恢复/CloneDBInstance.md)|调用CloneDBInstance接口将历史数据恢复至一个新实例（称为克隆实例）。|
|[DescribeBackups](cn.zh-CN/API参考/备份恢复/DescribeBackups.md)|调用DescribeBackups接口查看备份集列表。|
|[CreateTempDBInstance](cn.zh-CN/API参考/备份恢复/CreateTempDBInstance.md)|调用CreateTempDBInstance接口创建临时实例。|
|[DescribeBackupPolicy](cn.zh-CN/API参考/备份恢复/DescribeBackupPolicy.md)|调用DescribeBackupPolicy接口查看实例备份设置。|
|[ModifyBackupPolicy](cn.zh-CN/API参考/备份恢复/ModifyBackupPolicy.md)|调用ModifyBackupPolicy接口修改备份设置。|
|[RestoreDBInstance](cn.zh-CN/API参考/备份恢复/RestoreDBInstance.md)|调用RestoreDBInstance接口恢复备份集到原实例（覆盖性恢复），已下线。|
|[DeleteBackup](cn.zh-CN/API参考/备份恢复/DeleteBackup.md)|调用DeleteBackup接口删除数据备份文件。|
|[RecoveryDBInstance](cn.zh-CN/API参考/备份恢复/RecoveryDBInstance.md)|调用RecoveryDBInstance接口恢复数据库。|
|[DescribeBackupTasks](cn.zh-CN/API参考/备份恢复/DescribeBackupTasks.md)|调用DescribeBackupTasks接口查询实例的备份任务列表。|
|[DescribeLogBackupFiles](cn.zh-CN/API参考/备份恢复/DescribeLogBackupFiles.md)|调用DescribeLogBackupFiles接口查询实例的日志备份文件。|
|[DescribeBackupDatabase](cn.zh-CN/API参考/备份恢复/DescribeBackupDatabase.md)|调用DescribeBackupDatabase接口查询备份集下的数据库列表，已下线。|

## 跨地域备份恢复 {#section_k4h_jyb_uwk .section}

|API|描述|
|---|--|
|[CheckCreateDdrDBInstance](cn.zh-CN/API参考/跨地域备份恢复/CheckCreateDdrDBInstance.md)|调用CheckCreateDdrDBInstance接口预检查某RDS实例是否可以用跨地域备份集进行跨地域恢复。|
|[CreateDdrInstance](cn.zh-CN/API参考/跨地域备份恢复/CreateDdrInstance.md)|调用CreateDdrInstance接口跨地域恢复数据到新实例。|
|[ModifyInstanceCrossBackupPolicy](cn.zh-CN/API参考/跨地域备份恢复/ModifyInstanceCrossBackupPolicy.md)|调用ModifyInstanceCrossBackupPolicy接口修改RDS跨地域备份设置。|
|[DescribeInstanceCrossBackupPolicy](cn.zh-CN/API参考/跨地域备份恢复/DescribeInstanceCrossBackupPolicy.md)|调用DescribeInstanceCrossBackupPolicy接口查询跨地域备份设置。|
|[DescribeCrossRegionBackups](cn.zh-CN/API参考/跨地域备份恢复/DescribeCrossRegionBackups.md)|调用DescribeCrossRegionBackups接口查看某RDS实例跨地域数据备份文件列表。|
|[DescribeCrossRegionLogBackupFiles](cn.zh-CN/API参考/跨地域备份恢复/DescribeCrossRegionLogBackupFiles.md)|调用DescribeCrossRegionLogBackupFiles接口查看跨地域日志备份文件列表。|
|[DescribeAvailableCrossRegion](cn.zh-CN/API参考/跨地域备份恢复/DescribeAvailableCrossRegion.md)|调用DescribeAvailableCrossRegion接口查询所选地域当前可以进行跨地域备份的目的地域。|
|[DescribeAvailableRecoveryTime](cn.zh-CN/API参考/跨地域备份恢复/DescribeAvailableRecoveryTime.md)|调用DescribeAvailableRecoveryTime接口查询某跨地域备份文件可恢复哪个时间段的数据。|
|[DescribeCrossRegionBackupDBInstance](cn.zh-CN/API参考/跨地域备份恢复/DescribeCrossRegionBackupDBInstance.md)|调用DescribeCrossRegionBackupDBInstance接口查询所选地域的哪些实例开启了跨地域备份，以及这些实例的跨地域备份设置。|

## SQL Server备份文件上云 {#section_vxb_rg8_79h .section}

|API|描述|
|---|--|
|[CreateMigrateTask](cn.zh-CN/API参考/SQL Server备份文件上云/CreateMigrateTask.md)|调用CreateMigrateTask接口将OSS上的备份文件还原到RDS实例，实现数据上云。|
|[DescribeMigrateTasks](cn.zh-CN/API参考/SQL Server备份文件上云/DescribeMigrateTasks.md)|调用DescribeMigrateTasks接口查询备份数据上云任务列表。|
|[DescribeOssDownloads](cn.zh-CN/API参考/SQL Server备份文件上云/DescribeOssDownloads.md)|调用DescribeOssDownloads接口查看备份数据上云任务的文件详情。|
|[CreateOnlineDatabaseTask](cn.zh-CN/API参考/SQL Server备份文件上云/CreateOnlineDatabaseTask.md)|在备份数据上云时调用CreateOnlineDatabaseTask接口打开数据库。|

## 监控管理 {#section_lrn_a1g_jft .section}

|API|描述|
|---|--|
|[DescribeResourceUsage](cn.zh-CN/API参考/监控管理/DescribeResourceUsage.md)|调用DescribeResourceUsage接口查看实例的空间利用信息。|
|[DescribeDBInstancePerformance](cn.zh-CN/API参考/监控管理/DescribeDBInstancePerformance.md)|调用DescribeDBInstancePerformance接口查看实例性能数据。|
|[DescribeDBInstanceMonitor](cn.zh-CN/API参考/监控管理/DescribeDBInstanceMonitor.md)|调用DescribeDBInstanceMonitor接口查询监控频率。|
|[ModifyDBInstanceMonitor](cn.zh-CN/API参考/监控管理/ModifyDBInstanceMonitor.md)|调用ModifyDBInstanceMonitor修改监控频率。|

## 参数管理 {#section_t2i_x5q_en4 .section}

|API|描述|
|---|--|
|[DescribeParameterTemplates](cn.zh-CN/API参考/参数管理/DescribeParameterTemplates.md)|调用DescribeParameterTemplates接口查看数据库参数模板。|
|[DescribeParameters](cn.zh-CN/API参考/参数管理/DescribeParameters.md)|调用DescribeParameters接口查询实例当前的参数配置。|
|[ModifyParameter](cn.zh-CN/API参考/参数管理/ModifyParameter.md)|调用ModifyParameter接口修改实例参数。|

## 数据迁移 {#section_nqh_jp4_iv0 .section}

|API|描述|
|---|--|
|[ImportDatabaseBetweenInstances](cn.zh-CN/API参考/数据迁移/ImportDatabaseBetweenInstances.md)|调用ImportDatabaseBetweenInstances接口从其它RDS实例迁入数据。|
|[CancelImport](cn.zh-CN/API参考/数据迁移/CancelImport.md)|调用CancelImport接口用于取消RDS实例迁移任务。|

## 标签管理 {#section_iu4_c1g_npu .section}

|API|描述|
|---|--|
|[AddTagsToResource](cn.zh-CN/API参考/标签管理/AddTagsToResource.md)|调用AddTagsToResource接口为实例绑定标签。|
|[DescribeTags](cn.zh-CN/API参考/标签管理/DescribeTags.md)|调用DescribeTags接口查询RDS实例的标签。|
|[RemoveTagsFromResource](cn.zh-CN/API参考/标签管理/RemoveTagsFromResource.md)|调用RemoveTagsFromResource接口解绑标签。|

