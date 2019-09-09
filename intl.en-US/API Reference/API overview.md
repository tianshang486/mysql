# API overview {#doc_8073 .concept}

This topic provides an overview of APIs provided by RDS for MySQL.

## Instance management {#section_qoy_tra_wjr .section}

|API|Description|
|---|-----------|
|[DestroyDBInstance](intl.en-US/API Reference/Instance management/DestroyDBInstance.md)|Used to destroy an RDS instance. This API has been deprecated.|
|[ModifyDBInstanceDelayReplicationTime](intl.en-US/API Reference/Instance management/ModifyDBInstanceDelayReplicationTime.md)|Used to change the data replication delay time allowed for a read-only instance. This API has been deprecated.|
|[CreateDBInstance](intl.en-US/API Reference/Instance management/CreateDBInstance.md)|Used to create an RDS instance.|
|[DeleteDBInstance](intl.en-US/API Reference/Instance management/DeleteDBInstance.md)|Used to release an RDS instance.|
|[RestartDBInstance](intl.en-US/API Reference/Instance management/RestartDBInstance.md)|Used to restart an RDS instance.|
|[RenewInstance](intl.en-US/API Reference/Instance management/RenewInstance.md)|Used to manually renew an RDS instance.|
|[DescribeDBInstanceAttribute](intl.en-US/API Reference/Instance management/DescribeDBInstanceAttribute.md)|Used to view details about an RDS instance.|
|[DescribeDBInstances](intl.en-US/API Reference/Instance management/DescribeDBInstances.md)|Used to list all RDS instances or only the RDS instances authorized by RAM.|
|[ModifyDBInstanceSpec](intl.en-US/API Reference/Instance management/ModifyDBInstanceSpec.md)|Used to change the type or storage space of an RDS instance \(including common instances and read-only instances, but excluding disaster recovery instances and temporary instances\).|
|[DescribeRegions](intl.en-US/API Reference/Instance management/DescribeRegions.md)|Used to query the available RDS regions and zones.|
|[DescribeDBInstanceHAConfig](intl.en-US/API Reference/Instance management/DescribeDBInstanceHAConfig.md)|Used to query the high availability mode and data replication mode of an RDS instance.|
|[MigrateToOtherZone](intl.en-US/API Reference/Instance management/MigrateToOtherZone.md)|Used to migrate an RDS instance to a different zone.|
|[PurgeDBInstanceLog](intl.en-US/API Reference/Instance management/PurgeDBInstanceLog.md)|Used to delete or compress the logs of an RDS instance.|
|[UpgradeDBInstanceEngineVersion](intl.en-US/API Reference/Instance management/UpgradeDBInstanceEngineVersion.md)|Used to upgrade the database version of an RDS instance.|
|[ModifyDBInstanceDescription](intl.en-US/API Reference/Instance management/ModifyDBInstanceDescription.md)|Used to modify the description of an RDS instance.|
|[ModifyDBInstanceMaintainTime](intl.en-US/API Reference/Instance management/ModifyDBInstanceMaintainTime.md)|Used to change the maintenance window of an RDS instance.|
|[ModifyDBInstanceHAConfig](intl.en-US/API Reference/Instance management/ModifyDBInstanceHAConfig.md)|Used to change the high availability mode and data replication mode of an RDS instance.|
|[SwitchDBInstanceHA](intl.en-US/API Reference/Instance management/SwitchDBInstanceHA.md)|Used to switch between a master RDS instance and its slave RDS instance.|
|[CreateReadOnlyDBInstance](intl.en-US/API Reference/Instance management/CreateReadOnlyDBInstance.md)|Used to create a read-only RDS instance for a master RDS instance.|

## Database management {#section_d15_biz_jl6 .section}

|API|Description|
|---|-----------|
|[CreateDatabase](intl.en-US/API Reference/Database management/CreateDatabase.md)|Used to create a database under an RDS instance.|
|[DeleteDatabase](intl.en-US/API Reference/Database management/DeleteDatabase.md)|Used to delete a database under an RDS instance.|
|[DescribeDatabases](intl.en-US/API Reference/Database management/DescribeDatabases.md)|Used to view information about the databases under an RDS instance.|
|[ModifyDBDescription](intl.en-US/API Reference/Database management/ModifyDBDescription.md)|Used to modify the description of a database.|
|[CopyDatabase](intl.en-US/API Reference/Database management/CopyDatabase.md)|Used to replicate an RDS for SQL Server 2008 R2 instance. This API has been deprecated.|
|[CopyDatabaseBetweenInstances](intl.en-US/API Reference/Database management/CopyDatabaseBetweenInstances.md)|Used to replicate databases between RDS instances.|

## Database proxy {#section_lkr_lxi_ej7 .section}

|API|Description|
|---|-----------|
|[ModifyDBInstanceConnectionMode](intl.en-US/API Reference/Read__Write splitting/ModifyDBInstanceConnectionMode.md)|Used to enable or disable the database proxy. This API has been deprecated.|
|[AllocateReadWriteSplittingConnection](intl.en-US/API Reference/Read__Write splitting/AllocateReadWriteSplittingConnection.md)|Used to apply for a read/write splitting address.|
|[CalculateDBInstanceWeight](intl.en-US/API Reference/Read__Write splitting/CalculateDBInstanceWeight.md)|Used to query the weight allocated to an RDS instance.|
|[ModifyReadWriteSplittingConnection](intl.en-US/API Reference/Read__Write splitting/ModifyReadWriteSplittingConnection.md)|Used to change the delay threshold for connecting a read/write splitting link and the read weights allocated to a master RDS instance and each of its read-only instances.|
|[ReleaseReadWriteSplittingConnection](intl.en-US/API Reference/Read__Write splitting/ReleaseReadWriteSplittingConnection.md)|Used to release a read/write splitting address.|

## Account management {#section_ssw_qum_cfa .section}

|API|Description|
|---|-----------|
|[CreateAccount](intl.en-US/API Reference/Account management/CreateAccount.md)|Used to create an account for managing databases.|
|[DeleteAccount](intl.en-US/API Reference/Account management/DeleteAccount.md)|Used to delete an account that manages databases.|
|[DescribeAccounts](intl.en-US/API Reference/Account management/DescribeAccounts.md)|Used to view information about the accounts under an RDS instance.|
|[GrantAccountPrivilege](intl.en-US/API Reference/Account management/GrantAccountPrivilege.md)|Used to grant an account the permission to access a database.|
|[RevokeAccountPrivilege](intl.en-US/API Reference/Account management/RevokeAccountPrivilege.md)|Used to revoke the permission for an account to access a database.|
|[ModifyAccountDescription](intl.en-US/API Reference/Account management/ModifyAccountDescription.md)|Used to modify the description of a database account.|
|[ResetAccountPassword](intl.en-US/API Reference/Account management/ResetAccountPassword.md)|Used to reset the password of an account.|
|[ResetAccount](intl.en-US/API Reference/Account management/ResetAccount.md)|Used to reset the permissions of the superuser account under an RDS instance.|

## Security management {#section_t2b_eiz_cnm .section}

|API|Description|
|---|-----------|
|[DescribeDBInstanceIPArrayList](intl.en-US/API Reference/Security management/DescribeDBInstanceIPArrayList.md)|Used to view the IP address whitelist of an RDS instance.|
|[DescribeDBInstanceSSL](intl.en-US/API Reference/Security management/DescribeDBInstanceSSL.md)|Used to query the SSL setting of an RDS instance.|
|[DescribeDBInstanceTDE](intl.en-US/API Reference/Security management/DescribeDBInstanceTDE.md)|Used to query the data encryption status of an RDS instance.|
|[ModifyDBInstanceSSL](intl.en-US/API Reference/Security management/ModifyDBInstanceSSL.md)|Used to change the SSL link of an RDS instance.|
|[ModifyDBInstanceTDE](intl.en-US/API Reference/Security management/ModifyDBInstanceTDE.md)|Used to change the data encryption status of an RDS instance.|
|[ModifySecurityIps](intl.en-US/API Reference/Security management/ModifySecurityIps.md)|Used to modify the IP address whitelist of an RDS instance.|
|[MigrateSecurityIPMode](intl.en-US/API Reference/Security management/MigrateSecurityIPMode.md)|Used to change the standard mode to the enhanced security mode for a whitelist.|
|[DescribeDBInstanceIpHostname](intl.en-US/API Reference/Security management/DescribeDBInstanceIpHostname.md#)|Used to query the host name of the ECS instance connected to an RDS instance.|
|[DescribeDTCSecurityIpHostsForSQLServer](intl.en-US/API Reference/Security management/DescribeDTCSecurityIpHostsForSQLServer.md#)|Used to query the distributed transaction whitelist of an RDS instance.|
|[ModifyDTCSecurityIpHostsForSQLServer](intl.en-US/API Reference/Security management/ModifyDTCSecurityIpHostsForSQLServer.md#)|Used to configure a distributed transaction whitelist for an RDS instance.|

## Network management {#section_piv_av6_vf1 .section}

|API|Description|
|---|-----------|
|[AllocateInstancePublicConnection](intl.en-US/API Reference/Network management/AllocateInstancePublicConnection.md)|Used to apply for a public IP address for an RDS instance.|
|[DescribeDBInstanceNetInfo](intl.en-US/API Reference/Network management/DescribeDBInstanceNetInfo.md)|Used to view all the connection addresses of an RDS instance.|
|[ModifyDBInstanceNetworkExpireTime](intl.en-US/API Reference/Network management/ModifyDBInstanceNetworkExpireTime.md)|Used to change the expiration time of a connection address.|
|[ModifyDBInstanceConnectionString](intl.en-US/API Reference/Network management/ModifyDBInstanceConnectionString.md)|Used to change the connection addresses and ports of an RDS instance.|
|[ModifyDBInstanceNetworkType](intl.en-US/API Reference/Network management/ModifyDBInstanceNetworkType.md)|Used to change the network type of an RDS instance.|
|[ReleaseInstancePublicConnection](intl.en-US/API Reference/Network management/ReleaseInstancePublicConnection.md)|Used to release the public IP address of an RDS instance.|
|[SwitchDBInstanceNetType](intl.en-US/API Reference/Network management/SwitchDBInstanceNetType.md)|Used to switch between public and private IP addresses.|

## Log management {#section_oyl_qdq_aoh .section}

|API|Description|
|---|-----------|
|[DescribeSlowLogs](intl.en-US/API Reference/Log management/DescribeSlowLogs.md)|Used to view statistics of slow logs for an RDS instance.|
|[DescribeSlowLogRecords](intl.en-US/API Reference/Log management/DescribeSlowLogRecords.md)|Used to view details about the slow logs of an RDS instance.|
|[DescribeErrorLogs](intl.en-US/API Reference/Log management/DescribeErrorLogs.md)|Used to view the error logs generated within a specified time period for an RDS instance.|
|[DescribeBinlogFiles](intl.en-US/API Reference/Log management/DescribeBinlogFiles.md)|Used to view the binary logs of an RDS instance.|
|[ModifySQLCollectorPolicy](intl.en-US/API Reference/Log management/ModifySQLCollectorPolicy.md)|Used to enable or disable SQL audit for an RDS instance.|
|[DescribeSQLLogRecords](intl.en-US/API Reference/Log management/DescribeSQLLogRecords.md)|Used to query the SQL audit logs of an RDS instance.|
|[DescribeSQLLogFiles](intl.en-US/API Reference/Log management/DescribeSQLLogFiles.md)|Used to list the SQL audit files of an RDS instance.|

## Backup and restoration {#section_xtg_i1d_n4a .section}

|API|Description|
|---|-----------|
|[CreateBackup](intl.en-US/API Reference/Backup and recovery/CreateBackup.md)|Used to create a backup set for an RDS instance.|
|[CloneDBInstance](intl.en-US/API Reference/Backup and recovery/CloneDBInstance.md)|Used to restore the historical data of an RDS instance to a new RDS instance.|
|[DescribeBackups](intl.en-US/API Reference/Backup and recovery/DescribeBackups.md)|Used to list the backup sets of an RDS instance.|
|[CreateTempDBInstance](intl.en-US/API Reference/Backup and recovery/CreateTempDBInstance.md)|Used to create a temporary RDS instance.|
|[DescribeBackupPolicy](intl.en-US/API Reference/Backup and recovery/DescribeBackupPolicy.md)|Used to view the backup settings of an RDS instance.|
|[ModifyBackupPolicy](intl.en-US/API Reference/Backup and recovery/ModifyBackupPolicy.md)|Used to modify the backup settings of an RDS instance.|
|[RestoreDBInstance](intl.en-US/API Reference/Backup and recovery/RestoreDBInstance.md)|Used to restore an RDS instance by using a backup set. The existing data in the RDS instance is overwritten by the backup set. This API has been deprecated.|
|[DeleteBackup](intl.en-US/API Reference/Backup and recovery/DeleteBackup.md)|Used to delete the data backup files of an RDS instance.|
|[DescribeBackupTasks](intl.en-US/API Reference/Backup and recovery/DescribeBackupTasks.md)|Used to list the backup tasks of an RDS instance.|
|[DescribeLogBackupFiles](intl.en-US/API Reference/Backup and recovery/DescribeLogBackupFiles.md)|Used to query the log backup files of an RDS instance.|

## Cross-region backup and restoration {#section_xru_ha9_sp1 .section}

|API|Description|
|---|-----------|
|[CheckCreateDdrDBInstance](intl.en-US/API Reference/Cross-region backup and restoration/CheckCreateDdrDBInstance.md#)|Used to check whether the data of an RDS instance can be restored to a new RDS instance in a different region by using a cross-region backup set.|
|[CreateDdrInstance](intl.en-US/API Reference/Cross-region backup and restoration/CreateDdrInstance.md#)|Used to restore the data of an RDS instance to a new RDS instance in a different region.|
|[ModifyInstanceCrossBackupPolicy](intl.en-US/API Reference/Cross-region backup and restoration/ModifyInstanceCrossBackupPolicy.md#)|Used to modify the cross-region backup settings of an RDS instance.|
|[DescribeInstanceCrossBackupPolicy](intl.en-US/API Reference/Cross-region backup and restoration/DescribeInstanceCrossBackupPolicy.md#)|Used to query the cross-region backup settings of an RDS instance.|
|[DescribeCrossRegionBackups](intl.en-US/API Reference/Cross-region backup and restoration/DescribeCrossRegionBackups.md#)|Used to list the cross-region data backup files of an RDS instance.|
|[DescribeCrossRegionLogBackupFiles](intl.en-US/API Reference/Cross-region backup and restoration/DescribeCrossRegionLogBackupFiles.md#)|Used to list the cross-region log backup files of an RDS instance.|
|[DescribeAvailableCrossRegion](intl.en-US/API Reference/Cross-region backup and restoration/DescribeAvailableCrossRegion.md#)|Used to query the available destination regions for an RDS instance.|
|[DescribeAvailableRecoveryTime](intl.en-US/API Reference/Cross-region backup and restoration/DescribeAvailableRecoveryTime.md#)|Used to query the time range within which the data of a cross-region backup file can be restored.|
|[DescribeCrossRegionBackupDBInstance](intl.en-US/API Reference/Cross-region backup and restoration/DescribeCrossRegionBackupDBInstance.md#)|Used to query which RDS instances have cross-region backup enabled in a specified region, and the cross-region backup settings of these instances.|

## Migration of backup files to the cloud for an RDS for SQL Server instance {#section_bfg_eqc_q78 .section}

|API|Description|
|---|-----------|
|[CreateMigrateTask](intl.en-US/API Reference/Migrate SQL Server to the cloud/CreateMigrateTask.md)|Used to restore the data of a backup file in an OSS bucket to an RDS instance in the cloud.|
|[DescribeMigrateTasks](intl.en-US/API Reference/Migrate SQL Server to the cloud/DescribeMigrateTasks.md)|Used to list data migration tasks.|
|[DescribeOssDownloads](intl.en-US/API Reference/Migrate SQL Server to the cloud/DescribeOssDownloads.md)|Used to view details about the backup files used for data migration tasks.|
|[CreateOnlineDatabaseTask](intl.en-US/API Reference/Migrate SQL Server to the cloud/CreateOnlineDatabaseTask.md)|Used to open a database.|

## Monitoring management {#section_t7b_s9v_kjo .section}

|API|Description|
|---|-----------|
|[DescribeResourceUsage](intl.en-US/API Reference/Monitoring management/DescribeResourceUsage.md)|Used to view the space usage of an RDS instance.|
|[DescribeDBInstancePerformance](intl.en-US/API Reference/Monitoring management/DescribeDBInstancePerformance.md)|Used to view the performance data of an RDS instance.|
|[DescribeDBInstanceMonitor](intl.en-US/API Reference/Monitoring management/DescribeDBInstanceMonitor.md)|Used to query the monitoring frequency of an RDS instance.|
|[ModifyDBInstanceMonitor](intl.en-US/API Reference/Monitoring management/ModifyDBInstanceMonitor.md)|Used to change the monitoring frequency of an RDS instance.|

## Parameter management {#section_eg1_amq_joa .section}

|API|Description|
|---|-----------|
|[DescribeParameterTemplates](intl.en-US/API Reference/Parameter management/DescribeParameterTemplates.md)|Used to view a database parameter template.|
|[DescribeParameters](intl.en-US/API Reference/Parameter management/DescribeParameters.md)|Used to query the parameter settings of an RDS instance.|
|[ModifyParameter](intl.en-US/API Reference/Parameter management/ModifyParameter.md)|Used to reconfigure the parameters of an RDS instance.|

## Data migration {#section_ris_j0d_g48 .section}

|API|Description|
|---|-----------|
|[ImportDatabaseBetweenInstances](intl.en-US/API Reference/Data migration/ImportDatabaseBetweenInstances.md)|Used to migrate data to an RDS instance from another RDS instance.|
|[CancelImport](intl.en-US/API Reference/Data migration/CancelImport.md)|Used to cancel an RDS instance migration task.|

## Tag management {#section_lsh_bnf_lae .section}

|API|Description|
|---|-----------|
|[AddTagsToResource](intl.en-US/API Reference/Tag management/AddTagsToResource.md)|Used to bind tags to an RDS instance.|
|[DescribeTags](intl.en-US/API Reference/Tag management/DescribeTags.md)|Used to query the tags bound to an RDS instance.|
|[RemoveTagsFromResource](intl.en-US/API Reference/Tag management/RemoveTagsFromResource.md)|Used to unbind tags from an RDS instance.|

