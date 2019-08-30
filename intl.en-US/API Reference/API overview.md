# API overview {#doc_8073 .concept}

This topic provides an overview of APIs provided by RDS for MySQL.

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

