# API overview

The following tables list API operations available for use in ApsaraDB for RDS.

## Top 10 operations

|Operation|Description|
|---------|-----------|
|[CreateDBInstance](/intl.en-US/API Reference/Instance management/Create instance.md)|Creates an RDS instance.|
|[DescribeDBInstances](/intl.en-US/API Reference/Instance management/Query ApsaraDB for RDS instances.md)|Queries one or more RDS instances that meet the specified conditions.|
|[DescribeDBInstanceAttribute](/intl.en-US/API Reference/Instance management/Query instance details.md)|Queries details about one or more RDS instances.|
|[DescribeDBInstancePerformance](/intl.en-US/API Reference/Monitoring management/Query performance metrics.md)|Queries the performance metrics of an RDS instance.|
|[DescribeSlowLogRecords](/intl.en-US/API Reference/Log management/DescribeSlowLogRecords.md)|Queries details about the slow query logs for an RDS instance.|
|[DescribeSlowLogs](/intl.en-US/API Reference/Log management/Query summary of slow query logs.md)|Queries the summary of the slow query logs for an RDS instance.|
|[DescribeBackups](/intl.en-US/API Reference/Backup and recovery/Query backup sets.md)|Queries the backup sets of an RDS instance.|
|[DescribeResourceUsage](/intl.en-US/API Reference/Monitoring management/Query occupied space.md)|Queries the storage usage of an RDS instance.|
|[CreateAccount](/intl.en-US/API Reference/Account management/Create database account.md)|Creates an account that is used to manage databases on an RDS instance.|
|[CreateDatabase](/intl.en-US/API Reference/Database management/Create database.md)|Creates a database on an RDS instance.|

## Billing management

|Operation|Description|
|---------|-----------|
|[DescribeAvailableResource](/intl.en-US/API Reference/Billing/Query available resources.md)|Queries the resources available in a region.|
|[DescribeRenewalPrice](/intl.en-US/API Reference/Billing/Queries renewal fees.md)|Queries the fee that is required to renew the subscription of an RDS instance.|
|[TransformDBInstancePayType](/intl.en-US/API Reference/Billing/Modify billing method.md)|Changes the billing method of an RDS instance.|
|[RenewInstance](/intl.en-US/API Reference/Billing/Manual renewal.md)|Renews the subscription of an RDS instance.|

## Instance management

|Operation|Description|
|---------|-----------|
|[CreateDBInstance](/intl.en-US/API Reference/Instance management/Create instance.md)|Creates an RDS instance.|
|[DeleteDBInstance](/intl.en-US/API Reference/Instance management/Delete instance.md)|Releases an RDS instance.|
|[RestartDBInstance](/intl.en-US/API Reference/Instance management/Restart instance.md)|Restarts an RDS instance.|
|[ModifyDBInstanceSpec](/intl.en-US/API Reference/Instance management/Modify instance.md)|Modifies the specifications or storage capacity of a primary or read-only RDS instance.|
|[DescribeAvailableZones](/intl.en-US/API Reference/Instance management/Query available zones.md)|Queries the resources available in the zone to which an RDS instance belongs.|
|[DescribeDBInstanceAttribute](/intl.en-US/API Reference/Instance management/Query instance details.md)|Queries details about one or more RDS instances.|
|[DescribeDBInstances](/intl.en-US/API Reference/Instance management/Query ApsaraDB for RDS instances.md)|Queries one or more RDS instances that meet the specified conditions.|
|[DescribeRegions](/intl.en-US/API Reference/Instance management/Query available region.md)|Queries the regions and zones available for use in ApsaraDB for RDS.|
|[MigrateToOtherZone](/intl.en-US/API Reference/Instance management/Migration zone.md)|Migrates an RDS instance across zones within the same region.|
|[ModifyDBInstanceDescription](/intl.en-US/API Reference/Instance management/Modify instance description.md)|Modifies the description of an RDS instance.|
|[ModifyDBInstanceMaintainTime](/intl.en-US/API Reference/Instance management/Modify maintain time.md)|Changes the maintenance window of an RDS instance.|

## Engine version upgrade

|Operation|Description|
|---------|-----------|
|[UpgradeDBInstanceEngineVersion](/intl.en-US/API Reference/Version upgrade/Upgrade engine version.md)|Upgrades the database engine version of an RDS instance.|
|[UpgradeDBInstanceKernelVersion](/intl.en-US/API Reference/Version upgrade/Upgrade minor version.md)|Upgrades the minor engine version of an RDS instance.|
|[ModifyDBInstanceAutoUpgradeMinorVersion](/intl.en-US/API Reference/Version upgrade/Modify the upgrade method of minor version.md)|Changes the method that is used to upgrade the minor engine version of an RDS instance|

## Endpoint management

|Operation|Description|
|---------|-----------|
|[AllocateInstancePublicConnection](/intl.en-US/API Reference/Database Connection/Allocate public connection.md)|Allocates a public endpoint to an RDS instance.|
|[DescribeDBInstanceNetInfo](/intl.en-US/API Reference/Database Connection/Query endpoints.md)|Queries the endpoints of an RDS instance.|
|[ModifyDBInstanceConnectionString](/intl.en-US/API Reference/Database Connection/Modify connection address.md)|Modifies an endpoint and the associated port of an RDS instance.|
|[ModifyDBInstanceNetworkExpireTime](/intl.en-US/API Reference/Database Connection/Modify the expiration time of a connection address.md)|Modifies the expiration time of an endpoint for an RDS instance.|
|[SwitchDBInstanceNetType](/intl.en-US/API Reference/Database Connection/Switch between internal and public endpoints.md)|Switches an RDS instance between its internal and public endpoints.|
|[ReleaseInstancePublicConnection](/intl.en-US/API Reference/Database Connection/Release public endpoint.md)|Releases the public endpoint of an RDS instance.|

## Primary/secondary high availability and data replication

|Operation|Description|
|---------|-----------|
|[ModifyDBInstanceHAConfig](/intl.en-US/API Reference/Primary/Secondary High Availability and Data Replication/Modify high availability mode.md)|Changes the high availability and data replication modes of an RDS instance.|
|[DescribeDBInstanceHAConfig](/intl.en-US/API Reference/Primary/Secondary High Availability and Data Replication/Query high availability mode.md)|Queries the high availability and data replication modes of an RDS instance.|
|[SwitchDBInstanceHA](/intl.en-US/API Reference/Primary/Secondary High Availability and Data Replication/Switch over services between primary RDS instance and its secondary instance.md)|Switches services over between a primary RDS instance and its secondary instance.|
|[ModifyHASwitchConfig](/intl.en-US/API Reference/Primary/Secondary High Availability and Data Replication/Enable or disable automatic primary/secondary switchover.md)|Enables or disables the automatic primary/secondary switchover function for an RDS instance.|
|[DescribeHASwitchConfig](/intl.en-US/API Reference/Primary/Secondary High Availability and Data Replication/Query settings of automatic primary/secondary switchover.md)|Queries the settings of the automatic primary/secondary switchover function for an RDS instance.|

## Event history management

|Operation|Description|
|---------|-----------|
|[DescribeEvents](/intl.en-US/API Reference/Event History/Query events.md)|Queries the events of an RDS instance.|
|[DescribeActionEventPolicy](/intl.en-US/API Reference/Event History/Query status of event history.md)|Queries the status of the event history feature for an RDS instance.|
|[ModifyActionEventPolicy](/intl.en-US/API Reference/Event History/Enable or disable event history.md)|Enables or disables the event history feature for an RDS instance.|

## Account management

|Operation|Description|
|---------|-----------|
|[CreateAccount](/intl.en-US/API Reference/Account management/Create database account.md)|Creates an account that is used to manage databases on an RDS instance.|
|[DeleteAccount](/intl.en-US/API Reference/Account management/Delete database account.md)|Deletes an account from an RDS instance.|
|[ResetAccountPassword](/intl.en-US/API Reference/Account management/Reset password of account.md)|Resets the password of an account on an RDS instance.|
|[LockAccount](/intl.en-US/API Reference/Account management/Lock account.md)|Locks an account of an RDS instance.|
|[UnlockAccount](/intl.en-US/API Reference/Account management/Unlock account.md)|Unlocks an account of an RDS instance.|
|[DescribeAccounts](/intl.en-US/API Reference/Account management/Query accounts.md)|Queries the accounts that are created on an RDS instance.|
|[ModifyAccountDescription](/intl.en-US/API Reference/Account management/Modify descriptions of account.md)|Modifies the description of an account on an RDS instance.|
|[GrantAccountPrivilege](/intl.en-US/API Reference/Account management/Account permission/Grant permissions to account.md)|Grants the permissions on a database of an RDS instance to an account.|
|[RevokeAccountPrivilege](/intl.en-US/API Reference/Account management/Account permission/Revoke permissions from account.md)|Revokes the permissions on a database of an RDS instance from an account.|
|[ResetAccount](/intl.en-US/API Reference/Account management/Account permission/Reset permissions of privileged account.md)|Resets the permissions of the privileged account on an RDS instance.|

## Database management

|Operation|Description|
|---------|-----------|
|[CreateDatabase](/intl.en-US/API Reference/Database management/Create database.md)|Creates a database on an RDS instance.|
|[DeleteDatabase](/intl.en-US/API Reference/Database management/Delete database.md)|Deletes a database from an RDS instance.|
|[ModifyDBDescription](/intl.en-US/API Reference/Database management/Modify database descriptions.md)|Modifies the description of a database on an RDS instance.|
|[CopyDatabaseBetweenInstances](/intl.en-US/API Reference/Database management/Copy database.md)|Replicates databases across RDS instances.|
|[DescribeDatabases](/intl.en-US/API Reference/Database management/Query databases.md)|Queries details about the databases that are created on an RDS instance.|
|[DescribeCollationTimeZones](/intl.en-US/API Reference/Database management/Query collations and time zones.md)|Queries the character set collations and time zones available for use in ApsaraDB for RDS.|

## Read-only instance management

|Operation|Description|
|---------|-----------|
|[CreateReadOnlyDBInstance](/intl.en-US/API Reference/Read-Only Instances/Create read-only instance.md)|Creates a read-only instance for a primary RDS instance.|
|[DescribeReadDBInstanceDelay](/intl.en-US/API Reference/Read-Only Instances/Query latency between primary RDS instance and its read-only instance.md)|Queries the latency of data replication to a read-only RDS instance.|
|[ModifyReadonlyInstanceDelayReplicationTime](/intl.en-US/API Reference/Read-Only Instances/Modify replication latency of read-only RDS instance.md)|Modifies the latency of data replication to a read-only RDS instance.|

## Read/write splitting

|Operation|Description|
|---------|-----------|
|[AllocateReadWriteSplittingConnection](/intl.en-US/API Reference/Read/Write Splitting/Apply for read/write splitting endpoint.md)|Allocates a read/write splitting endpoint to an RDS instance.|
|[ReleaseReadWriteSplittingConnection](/intl.en-US/API Reference/Read/Write Splitting/Release read/write splitting endpoint.md)|Releases the read/write splitting endpoint of an RDS instance.|
|[CalculateDBInstanceWeight](/intl.en-US/API Reference/Read/Write Splitting/Query read weights of instance.md)|Queries the read weights of a primary RDS instance and its read-only instances.|
|[ModifyReadWriteSplittingConnection](/intl.en-US/API Reference/Read/Write Splitting/Modify read weights and latency threshold.md)|Modifies the latency threshold of the read/write splitting link and the read weights of a primary RDS instance and its read-only instances.|

## Database proxy management

|Operation|Description|
|---------|-----------|
|[ModifyDBProxy](/intl.en-US/API Reference/Database proxy/Enable or disable dedicated proxy.md)|Enables or disables the dedicated proxy feature for an RDS instance.|
|[ModifyDBProxyInstance](/intl.en-US/API Reference/Database proxy/Modify settings of dedicated proxy.md)|Modifies the settings of the dedicated proxy feature for an RDS instance.|
|[ModifyDBProxyEndpoint](/intl.en-US/API Reference/Database proxy/Modify endpoint of dedicated proxy.md)|Modifies the endpoint that is used to connect to the dedicated proxies of an RDS instance.|
|[DescribeDBProxy](/intl.en-US/API Reference/Database proxy/Query settings of dedicated proxy.md)|Queries details about the dedicated proxies of an RDS instance.|
|[DescribeDBProxyEndpoint](/intl.en-US/API Reference/Database proxy/Query endpoint of dedicated proxy.md)|Queries the endpoint that is used to connect to the dedicated proxies of an RDS instance.|
|[DescribeDBProxyPerformance](/intl.en-US/API Reference/Database proxy/Query performance metrics of dedicated proxy.md)|Queries the performance metrics of the dedicated proxies of an RDS instance.|
|[CreateDBProxyEndpointAddress](/intl.en-US/API Reference/Database proxy/Create proxy endpoint.md)|Creates an endpoint that is used to connect to the dedicated proxies of an RDS instance.|
|[ModifyDBProxyEndpointAddress](/intl.en-US/API Reference/Database proxy/Modify proxy endpoint.md)|Modifies the endpoint that is used to connect to the dedicated proxies of an RDS instance.|
|[DeleteDBProxyEndpointAddress](/intl.en-US/API Reference/Database proxy/Delete proxy endpoint.md)|Deletes the endpoint that is used to connect to the dedicated proxies of an RDS instance.|
|[DescribeDBInstanceProxyConfiguration](/intl.en-US/API Reference/Database proxy/Query settings of database proxy (shared proxy).md)|Queries the settings of the shared proxy feature for an RDS instance.|

## Security and encryption

|Operation|Description|
|---------|-----------|
|[DescribeSecurityGroupConfiguration](/intl.en-US/API Reference/Security management/Query security groups.md)|Queries details about the Elastic Compute Service \(ECS\) security groups that are associated with an RDS instance.|
|[ModifySecurityGroupConfiguration](/intl.en-US/API Reference/Security management/Modify security groups.md)|Modifies the ECS security groups that are associated with an RDS instance.|
|[DescribeDBInstanceIPArrayList](/intl.en-US/API Reference/Security management/Query IP address whitelists.md)|Queries the IP address whitelists of an RDS instance.|
|[ModifySecurityIps](/intl.en-US/API Reference/Security management/Modify IP address whitelists.md)|Modifies an IP address whitelist of an RDS instance.|
|[DescribeDBInstanceSSL](/intl.en-US/API Reference/Security management/Query settings of SSL.md)|Queries the settings of the Secure Sockets Layer \(SSL\) encryption function for an RDS instance.|
|[ModifyDBInstanceSSL](/intl.en-US/API Reference/Security management/Modify settings of SSL encryption.md)|Modifies the SSL link of an RDS instance|
|[DescribeDBInstanceTDE](/intl.en-US/API Reference/Security management/Query settings of TDE.md)|Queries the status of the Transparent Data Encryption \(TDE\) function for an RDS instance.|
|[ModifyDBInstanceTDE](/intl.en-US/API Reference/Security management/Enable TDE.md)|Enables the TDE function for an RDS instance.|
|[MigrateSecurityIPMode](/intl.en-US/API Reference/Security management/Switch network isolation mode from standard whitelist to enhanced whitelist.md)|Switches the network isolation mode of an RDS instance from standard whitelist to enhanced whitelist.|
|[DescribeDBInstanceIpHostname](/intl.en-US/API Reference/Security management/Query hostname of ECS instance connected to RDS instance.md)|Queries the hostname of the ECS instance that houses an RDS instance.|
|[DescribeDTCSecurityIpHostsForSQLServer](/intl.en-US/API Reference/Security management/Query distributed transaction whitelists.md)|Queries the distributed transaction whitelists of an RDS instance.|
|[ModifyDTCSecurityIpHostsForSQLServer](/intl.en-US/API Reference/Security management/Modify distributed transaction whitelists.md)|Configures a distributed transaction whitelist for an RDS instance.|

## Network management

|Operation|Description|
|---------|-----------|
|[ModifyDBInstanceNetworkType](/intl.en-US/API Reference/Network management/Switch network type.md)|Changes the network type of an RDS instance.|

## Log management

|Operation|Description|
|---------|-----------|
|[ModifySQLCollectorPolicy](/intl.en-US/API Reference/Log management/Enable or disable SQL Explorer (SQL audit).md)|Enables or disables the SQL Explorer \(SQL Audit\) feature for an RDS instance.|
|[DescribeSQLCollectorPolicy](/intl.en-US/API Reference/Log management/Query status of SQL Explorer (SQL audit).md)|Queries the status of the SQL Explorer \(SQL Audit\) feature for an RDS instance.|
|[DescribeSQLLogRecords](/intl.en-US/API Reference/Log management/Query SQL Explorer (SQL audit) logs.md)|Queries the SQL logs of an RDS instance.|
|[DescribeSQLLogFiles](/intl.en-US/API Reference/Log management/Query SQL Explorer (SQL audit) files.md)|Queries the SQL log files of an RDS instance.|
|[ModifySQLCollectorRetention](/intl.en-US/API Reference/Log management/Modify retention period of SQL Explorer logs.md)|Modifies the SQL log storage duration of an RDS instance.|
|[DescribeSQLCollectorRetention](/intl.en-US/API Reference/Log management/Query the log retention period allowed for the SQL explorer feature.md)|Queries the SQL log storage duration of an RDS instance.|
|[DescribeSlowLogs](/intl.en-US/API Reference/Log management/Query summary of slow query logs.md)|Queries the summary of the slow query logs for an RDS instance.|
|[DescribeSlowLogRecords](/intl.en-US/API Reference/Log management/DescribeSlowLogRecords.md)|Queries details about the slow query logs for an RDS instance.|
|[DescribeErrorLogs](/intl.en-US/API Reference/Log management/Query error logs.md)|Queries the error logs of an RDS instance over a specified time range.|
|[PurgeDBInstanceLog](/intl.en-US/API Reference/Log management/Clear logs.md)|Deletes or shrinks the SQL logs of an RDS instance.|

## Backup

|Operation|Description|
|---------|-----------|
|[CreateBackup](/intl.en-US/API Reference/Backup and recovery/Create backup set.md)|Creates a backup for an RDS instance.|
|[DescribeBackups](/intl.en-US/API Reference/Backup and recovery/Query backup sets.md)|Queries the backup sets of an RDS instance.|
|[DescribeBackupPolicy](/intl.en-US/API Reference/Backup and recovery/Query backup settings.md)|Queries the backup settings of an RDS instance.|
|[ModifyBackupPolicy](/intl.en-US/API Reference/Backup and recovery/Modify backup settings.md)|Modifies the backup settings of an RDS instance.|
|[DeleteBackup](/intl.en-US/API Reference/Backup and recovery/Delete backup sets.md)|Deletes one or more data backup files from an RDS instance.|
|[DescribeBackupTasks](/intl.en-US/API Reference/Backup and recovery/Query backup tasks.md)|Queries the backup tasks of an RDS instance.|
|[DescribeBinlogFiles](/intl.en-US/API Reference/Backup and recovery/Query binary logs.md)|Queries the log backup files of an RDS instance.|

## Restoration

|Operation|Description|
|---------|-----------|
|[RecoveryDBInstance](/intl.en-US/API Reference/Restoration/Restore databases.md)|Restores one or more databases of an RDS instance.|
|[CloneDBInstance](/intl.en-US/API Reference/Restoration/Clone instance.md)|Restores the data of an RDS instance to a new RDS instance, which is called a cloned instance.|
|[CreateTempDBInstance](/intl.en-US/API Reference/Restoration/Create temporary instance.md)|Creates a temporary RDS instance.|
|[DescribeLocalAvailableRecoveryTime](/intl.en-US/API Reference/Restoration/Query the time range for restoration.md)|Queries the restorable time of an RDS instance.|
|[RestoreTable](/intl.en-US/API Reference/Restoration/Restore databases or tables.md)|Restores one or more databases or tables of an RDS instance to the same RDS instance.|

## Cross-region backup and restoration

|Operation|Description|
|---------|-----------|
|[CheckCreateDdrDBInstance](/intl.en-US/API Reference/Cross-region backup and restoration/Check whether RDS instance can be restored by using backup sets across regions.md)|Checks whether to allow an RDS instance to be restored by using a cross-region backup set.|
|[CreateDdrInstance](/intl.en-US/API Reference/Cross-region backup and restoration/Create disaster recovery instance.md)|Restores the data of an RDS instance to a new RDS instance across regions.|
|[ModifyInstanceCrossBackupPolicy](/intl.en-US/API Reference/Cross-region backup and restoration/Modify settings of cross-region backup.md)|Modifies the cross-region backup settings of an RDS instance.|
|[DescribeInstanceCrossBackupPolicy](/intl.en-US/API Reference/Cross-region backup and restoration/Query settings of cross-region backup.md)|Queries the cross-region backup settings of an RDS instance.|
|[DescribeCrossRegionBackups](/intl.en-US/API Reference/Cross-region backup and restoration/Query cross-region data backup files.md)|Queries the cross-region data backup files of an RDS instance.|
|[DescribeCrossRegionLogBackupFiles](/intl.en-US/API Reference/Cross-region backup and restoration/Query cross-region log backup files.md)|Queries the cross-region log backup files of an RDS instance.|
|[DescribeAvailableCrossRegion](/intl.en-US/API Reference/Cross-region backup and restoration/Query available regions for cross-region backup.md)|Queries the destination regions that allow cross-region backup files from a region.|
|[DescribeAvailableRecoveryTime](/intl.en-US/API Reference/Cross-region backup and restoration/Query time range for cross-region backup.md)|Queries the restorable time that is allowed by a cross-region backup file.|
|[DescribeCrossRegionBackupDBInstance](/intl.en-US/API Reference/Cross-region backup and restoration/Query details about instances with cross-region backup enabled.md)|Queries the RDS instances for which the cross-region backup feature is enabled in a region and the cross-region backup settings of these instances.|

## Migration of backup files to the cloud \(SQL Server\)

|Operation|Description|
|---------|-----------|
|[CreateMigrateTask](/intl.en-US/API Reference/Migrate SQL Server to the cloud/Create migration task.md)|Restores backup files from Object Storage Service \(OSS\) buckets to an RDS instance.|
|[DescribeMigrateTasks](/intl.en-US/API Reference/Migrate SQL Server to the cloud/Query migration tasks.md)|Queries the backup data migration tasks of an RDS instance.|
|[DescribeOssDownloads](/intl.en-US/API Reference/Migrate SQL Server to the cloud/Query backup data files of migration task.md)|Queries the backup files that are involved in a backup data migration task of an RDS instance.|
|[CreateOnlineDatabaseTask](/intl.en-US/API Reference/Migrate SQL Server to the cloud/Open database.md)|Opens the databases that are involved in a backup data migration task of an RDS instance.|

## Monitoring

|Operation|Description|
|---------|-----------|
|[DescribeResourceUsage](/intl.en-US/API Reference/Monitoring management/Query occupied space.md)|Queries the storage usage of an RDS instance.|
|[DescribeDBInstancePerformance](/intl.en-US/API Reference/Monitoring management/Query performance metrics.md)|Queries the performance metrics of an RDS instance.|
|[DescribeDBInstanceMonitor](/intl.en-US/API Reference/Monitoring management/Query monitoring frequency.md)|Queries the monitoring frequency of an RDS instance.|
|[ModifyDBInstanceMonitor](/intl.en-US/API Reference/Monitoring management/Modify monitoring frequency.md)|Modifies the monitoring frequency of an RDS instance.|

## Parameter management

|Operation|Description|
|---------|-----------|
|[DescribeParameters](/intl.en-US/API Reference/Parameter management/Query parameter configurations.md)|Queries the parameter settings of an RDS instance.|
|[ModifyParameter](/intl.en-US/API Reference/Parameter management/Modify instance parameters.md)|Reconfigures the parameters of an RDS instance.|
|[DescribeModifyParameterLog](/intl.en-US/API Reference/Parameter management/Query parameter configuration logs.md)|Queries the parameter reconfiguration logs of an RDS instance.|
|[DescribeParameterTemplates](/intl.en-US/API Reference/Parameter management/Query parameter template.md)|Queries the parameter templates available to an RDS instance.|
|[CreateParameterGroup](/intl.en-US/API Reference/Parameter management/Create parameter template.md)|Creates a parameter template.|
|[ModifyParameterGroup](/intl.en-US/API Reference/Parameter management/Modify parameter template.md)|Modifies a parameter template.|
|[CloneParameterGroup](/intl.en-US/API Reference/Parameter management/Copy parameter template.md)|Replicates a parameter template to the current region or to another specified region.|
|[DescribeParameterGroups](/intl.en-US/API Reference/Parameter management/Query parameter templates.md)|Queries the parameter templates available to a region.|
|[DescribeParameterGroup](/intl.en-US/API Reference/Parameter management/Query information of parameter template.md)|Queries details about a parameter template.|
|[DeleteParameterGroup](/intl.en-US/API Reference/Parameter management/Delete parameter template.md)|Deletes a parameter template.|

## Data migration

|Operation|Description|
|---------|-----------|
|[ImportDatabaseBetweenInstances](/intl.en-US/API Reference/Data migration/Migrate data from other RDS instances.md)|Migrates data between RDS instances.|
|[CancelImport](/intl.en-US/API Reference/Data migration/Cancel migration task.md)|Cancels a migration task of an RDS instance.|

## Tag management

|Operation|Description|
|---------|-----------|
|[TagResources](/intl.en-US/API Reference/Tag management/Create tag.md)|Creates and binds tags to one or more RDS instances.|
|[UntagResources](/intl.en-US/API Reference/Tag management/Unbind tag.md)|Unbinds tags from an RDS instance.|
|[ListTagResources](/intl.en-US/API Reference/Tag management/Query tags.md)|Queries the tags that are bound to one or more RDS instances.|

