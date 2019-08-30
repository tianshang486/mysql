# API overview {#doc_8073 .concept}

This topic provides an overview of APIs provided by RDS for MySQL.

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
|[RecoveryDBInstance](intl.en-US/API Reference/Backup and recovery/RecoveryDBInstance.md)|Used to restore the databases of an RDS instance.|
|[DescribeBackupTasks](intl.en-US/API Reference/Backup and recovery/DescribeBackupTasks.md)|Used to list the backup tasks of an RDS instance.|
|[DescribeLogBackupFiles](intl.en-US/API Reference/Backup and recovery/DescribeLogBackupFiles.md)|Used to query the log backup files of an RDS instance.|
|[DescribeBackupDatabase](intl.en-US/API Reference/Backup and recovery/DescribeBackupDatabase.md)|Used to list the databases in a backup set for an RDS instance. This API has been deprecated.|

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

