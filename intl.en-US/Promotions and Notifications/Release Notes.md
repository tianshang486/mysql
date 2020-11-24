# Release Notes

This topic describes the release notes of ApsaraDB RDS, including features and document updates.

## October 2020

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|SQL Server|Cross-region backup|The cross-region backup feature is supported. This feature replicates backup files from an RDS instance to a region that is different from the region of the RDS instance. These cross-region data backup files can be used to monitor and restore the RDS instance.|2020-10-23|[Back up an ApsaraDB RDS for SQL Server instance across regions](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance across regions.md)|

## September 2020

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|PostgreSQL|Spatio-temporal database engine|Version 3.0 of Ganos is released.|2020-09-09|[Overview](/intl.en-US/Spatio-temporal Database/Overview.md)|
|MySQL|AliSQL|The minor AliSQL version 20200831 is released. In this version, start global transaction identifiers \(GTIDs\) and end GTIDs are introduced to the mysqlbinlog plug-in. The concurrency control \(CCL\) mechanism is optimized to better determine how transactions wait and concurrently run. In addition, various log sequence numbers \(LSNs\) in the redo log file are supported.|2020-09-09|[Release notes of minor AliSQL versions](/intl.en-US/Proprietary AliSQL/Release notes of minor AliSQL versions.md)|
|PostgreSQL|AliPG|The minor AliPG version 20200830 is released. In this version, the Ganos plug-in is upgraded to Version 3.0. In addition, the sql\_firewall and TimescaleD plug-ins are supported.|2020-09-09|[Release notes of minor AliPG versions](/intl.en-US/Proprietary AliPG/Release notes of minor AliPG versions.md)|
|All|Alibaba Cloud Resource Access Management \(RAM\) user authorization|The authorization of permissions on RDS instances to RAM users is supported. This is implemented by using RAM.|2020-09-08|[Authorize a RAM user to manage ApsaraDB for RDS instances](/intl.en-US/Best Practices/Authorize a RAM user to manage ApsaraDB for RDS instances.md)|
|PostgreSQL|HyperLogLog \(HLL\) plug-in|The recommendation of content to a user based on the preferences of the user is supported. This is implemented by using the HLL plug-in.|2020-09-07|[User preference recommendation system](/intl.en-US/RDS PostgreSQL Database/Application Solutions/User preference recommendation system.md)|

## August 2020

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|Dedicated proxy|The dedicated proxy feature is supported. You can create, modify, and delete the proxy endpoints of RDS instances.|2020-08-20|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|
|MySQL|Transparent data encryption \(TDE\)|TDE is supported for RDS instances that run MySQL 8.0 on RDS High-availability Edition with local SSDs.|2020-08-12|[Configure TDE for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md)|

## July 2020

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|Single-digit second backup|The single-digit second backup feature is supported for RDS instances that use enhanced SSDs. You can enable this feature on the Backup Settings tab of the Backup and Restoration page in the ApsaraDB RDS console. If this feature is enabled, a backup task can be completed within seconds. This feature is suitable for urgent backup requirements. For example, you can enable this feature if you must back up your RDS instance before an emergency release.|2020-07-28|[Back up an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md)|
|SQL Server|Account creation|The creation of an account named `Sa` is supported. You can connect applications to RDS instances by using this account.|2020-07-22|[Create an account for an RDS SQL Server instancy](/intl.en-US/RDS SQL Server Database/Account/Create an account for an RDS SQL Server instancy.md)|
|PostgreSQL|New instance type|A total of 17 more instance types that provide 2 to 104 CPU cores are introduced to RDS instances that run the RDS High-availability Edition with standard or enhanced SSDs.|2020-07-20|[Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md)|

## June 2020

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|Online expansion of storage capacity|Online expansion of storage capacity is supported for RDS instances that run MySQL 5.7 or 8.0 with standard or enhanced SSDs. The expansion requires about 5 minutes.|2020-06-19|[Change the specifications of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md)|
|MySQL|Maximum username length|The maximum username length is increased to 32 characters. This applies to RDS instances that run MySQL 5.7 or 8.0.|2020-06-16|[Create an account on an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Account/Create an account on an ApsaraDB RDS for MySQL instance.md)|
|SQL Server|User-created domain|RDS instances can be connected to user-created domains.|2020-06-12|[Connect an ApsaraDB RDS for SQL Server instance to a user-created domain](/intl.en-US/RDS SQL Server Database/Best practices/Connect an ApsaraDB RDS for SQL Server instance to a user-created domain.md)|
|SQL Server|Storage type|The storage types of RDS instances can be changed from standard SSDs to enhanced SSDs across zones.|2020-06-11|[A new version is available.](/intl.en-US/RDS SQL Server Database/Instance/Change the specifications of an ApsaraDB RDS for SQL Server instance.md)|

## May 2020

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|Minor engine version update|The selection of a policy that is used to update the minor engine version is supported. This applies when you create an RDS instance.|2020-05-15|[Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)|
|MySQL|Database- and table-level restoration|The efficiency of database- and table-level restoration is increased by four times.|2020-05-12|[Restore individual databases and tables of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md)|
|SQL Server|Storage type|The storage types of RDS instances can be changed from standard SSDs to enhanced SSDs.|2020-05-07|[A new version is available.](/intl.en-US/RDS SQL Server Database/Instance/Change the specifications of an ApsaraDB RDS for SQL Server instance.md)|

## April 2020

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|Data restoration across regions|The restoration of data from a cross-region backup file to an existing RDS instance is supported.|2020-04-24|[Restore the data of an ApsaraDB RDS for MySQL instance across regions](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance across regions.md)|
|MySQL|Memory management|Custom memory management is supported.|2020-04-22|[Memory management of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Memory management of an ApsaraDB RDS for MySQL instance.md)|
|All|Billing method|The billing method can be changed from subscription to pay-as-you-go.|2020-04-21|[Switch the billing method from subscription to pay-as-you-go](/intl.en-US/RDS MySQL Database/Instance Change/Switch the billing method from subscription to pay-as-you-go.md)|
|MySQL|Dedicated proxy|Custom proxy endpoints are supported in the dedicated proxy feature.|2020-04-15|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|
|PostgreSQL|Plug-in|The HLL, smlar, and tds\_fdw plug-ins are supported.|2020-04-21|[Plug-ins supported](/intl.en-US/Proprietary AliPG/Plug-ins supported.md)|
|MySQL|Data restoration|Auto-renewal is supported for new RDS instances to which you restore data.|2020-04-14|[Restore the data of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance.md)|
|SQL Server|New version|SQL Server 2008 R2 is supported for RDS instances that use standard or enhanced SSDs.|2020-04-10|[Create an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)|
|MySQL|Secure Sockets Layer \(SSL\) encryption|SSL encryption is supported for RDS instances that run MySQL 5.7 or 8.0 on RDS Enterprise Edition.|2020-04-09|[Configure SSL encryption on an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure SSL encryption on an ApsaraDB RDS for MySQL instance.md)|
|PostgreSQL|Foreign table|Both foreign SQL Server and Sybase tables are supported.|2020-04-03|N/A|
|MySQL|Database- and table-level restoration|The restoration of databases and tables is supported for RDS instances that run MySQL 8.0.|2020-04-01|[Restore individual databases and tables of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md)|

## March 2020

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|Dedicated proxy|The upgrade from shared proxy to dedicated proxy is supported.|2020-03-20|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|
|MySQL|Dedicated cluster|Dedicated clusters \(formerly known as host groups\) are supported for RDS instances that run MySQL 5.6.|2020-03-18|[Dedicated cluster](/intl.en-US/.md)|
|MySQL|Dedicated proxy|The dedicated proxy feature is supported for RDS instances that run MySQL 5.6 on RDS High-availability Edition with local SSDs.|2020-03-13|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|
|PostgreSQL|Multi-zone deployment|Multi-zone deployment is supported for RDS instances that run the RDS High-availability Edition with standard or enhanced SSDs.|2020-03-08|[Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md)|
|MySQL|Alert rule|Alert rules are optimized to support one-minute alert intervals and more metrics.|2020-03-02|[Configure an alert rule for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for MySQL instance.md)|

## February 2020

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|Enterprise Edition|The RDS Enterprise Edition is supported for RDS instances that run MySQL 5.7 or 8.0 in all regions.|2020-02-28|[Enterprise Edition](/intl.en-US/Product Introduction/Product editions/Enterprise Edition.md)|
|MySQL|Instance analysis|Instance analysis is supported for RDS instances that run the RDS High-availability or Enterprise Edition.|2020-02-28|[Overview of ApsaraDB RDS for MySQL analytic instances]()|
|SQL Server|New version|SQL Server 2019 SE Beta is supported.|2020-02-28|[Create an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)|
|MySQL|Zone of the primary instance|Single-zone deployment and multi-zone deployment are supported. You can specify a zone for the primary RDS instance, and the system then assigns a zone for the secondary RDS instance.|2020-02-27|[Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)|
|MySQL|Long term backup|The long term backup feature is supported. This feature allows you to retain backup files for a long term.|2020-02-26|[Back up an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md)|
|SQL Server|Disk encryption|The encryption of standard and enhanced SSDs based on Bring Your Own Keys \(BYOKs\) is supported when multi-zone deployment is adopted.|2020-02-26|[Configure disk encryption for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Data security/Configure disk encryption for an ApsaraDB RDS for SQL Server instance.md)|
|SQL Server|Database management|Database management is supported for RDS instances that run SQL Server 2017 EE.|2020-02-25|[Create a database on an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Database/Create a database on an ApsaraDB RDS for SQL Server instance.md)|
|PostgreSQL|Reserved connection|The reservation for a specific number of connections is supported for superuser accounts. You can log on to an RDS instance and troubleshoot issues by using these accounts even if the number of established connections to the RDS instance reaches the upper limit.|2020-02-22|[Release notes of minor AliPG versions](/intl.en-US/Proprietary AliPG/Release notes of minor AliPG versions.md)|
|PostgreSQL|PLV8|PLV8 2.3.13 is provided for PostgreSQL 12 to compile stored procedures and functions.|2020-02-22|N/A|
|MySQL|Storage type|Two new storage types are provided on the ApsaraDB RDS buy page: ESSD PL2 and ESSD PL3.|2020-02-21|[Storage types](/intl.en-US/Product Introduction/Storage types.md)|
|PostgreSQL|SQL translation|The translation of SQL statements from the Oracle syntax to the PostgreSQL syntax is supported.|2020-02-14|[SQL translation](/intl.en-US/RDS PostgreSQL Database/SQL translation.md)|
|PostgreSQL|wal2json plug-in|The wal2json plug-in is provided for PostgreSQL 12 to support logical subscriptions.|2020-02-14|[Use the wal2json plug-in](/intl.en-US/Proprietary AliPG/Use the wal2json plug-in.md)|
|MySQL|Edition change|The RDS edition can be changed from Enterprise to High-availability. This applies to RDS instances that run MySQL 5.6.|2020-02-13|[Change the specifications of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md)|
|MySQL|Number of ECS security groups|The number of ECS security groups allowed per instance is increased from 1 to 10.|2020-02-04|[Control access to an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.md)|

## January 2020

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|X-Engine|The X-Engine storage engine that is developed by Alibaba Cloud is provided. X-Engine can compress a large volume of data at a significantly high compression ratio in online transaction processing \(OLTP\) scenarios.|2020-01-15|[X-Engine overview](/intl.en-US/Proprietary AliSQL/X-Engine/X-Engine overview.md)|
|MySQL|Host monitoring|The monitoring of hosts in dedicated clusters is supported. You can view host monitoring information and configure alert rules.|2020-01-15|[View a host in an RDS ApsaraDB for MyBase]()|
|MySQL|System parameter template|Two system parameter templates are provided: one for high availability and the other for high performance.|2020-01-14|[Use a parameter template to manage parameters](/intl.en-US/RDS MySQL Database/Instance parameters/Use a parameter template to manage parameters.md)|
|PostgreSQL|pg\_cron plug-in|The pg\_cron plug-in is released for PostgreSQL 11 to configure scheduled tasks.|2020-01-14|[t1857649.md\#](/intl.en-US/Proprietary AliPG/Use the pg_cron plug-in.md)|
|PostgreSQL|PLV8|PLV8 2.3.13 is provided for PostgreSQL 11 to compile stored procedures and functions.|2020-01-14|N/A|
|PostgreSQL|log\_fdw plug-in|The log\_fdw plug-in is provided for PostgreSQL 11 to query logs in real time.|2020-01-14|[Use the log\_fdw plug-in](/intl.en-US/Proprietary AliPG/Run cross-database queries/Use the log_fdw plug-in.md)|
|PostgreSQL|wal2json plug-in|The wal2json plug-in is provided for PostgreSQL 12 to support logical subscriptions.|2020-01-14|[Use the wal2json plug-in](/intl.en-US/Proprietary AliPG/Use the wal2json plug-in.md)|
|MySQL|Performance insight|The performance insight feature is supported for two RDS editions: High-availability and Enterprise.|2020-01-09|[Performance insight](/intl.en-US/RDS MySQL Database/Performance optimization and diagnosis (autonomy service)/Performance insight.md)|
|MySQL|TDE|TDE with BYOKs is supported for RDS instances that run MySQL 5.7 on RDS High-availability Edition with local SSDs.|2020-01-07|[Configure TDE for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md)|
|PostgreSQL|Enhanced SSD PL|Two new protection levels \(PLs\) of enhanced SSDs are provided on the ApsaraDB RDS buy page: ESSD PL2 and ESSD PL3. This applies to RDS instances that run PostgreSQL 10 on RDS High-availability Edition.|2020-01-07|[Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md)|

## December 2019

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|PostgreSQL|pg\_roaringbitmap plug-in|The pg\_roaringbitmap plug-in is provided for PostgreSQL 12 to spot user profiles in real time.|2019-12-31|[Use the roaringbitmap plug-in](/intl.en-US/Proprietary AliPG/Query vertical industry-specific data/Use the roaringbitmap plug-in.md)|
|PostgreSQL|Monitoring and alerting|Monitoring and alerting are supported for RDS instances that use standard or enhanced SSDs.|2019-12-31|[Set the monitoring frequency of an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Monitoring and alerts/Set the monitoring frequency of an ApsaraDB RDS for PostgreSQL instance.md)|
|MySQL|Dedicated proxy|The dedicated proxy feature is supported for RDS instances that run MySQL 5.7 or 8.0 on RDS Enterprise Edition.|2019-12-25|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|
|MySQL|Enterprise Edition|The RDS Enterprise Edition is supported for RDS instances that run MySQL 8.0.|2019-12-24|[Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)|
|MySQL|Storage for dedicated clusters|X-Dragon servers are supported for dedicated clusters. You can create RDS instances that use enhanced SSDs on these servers.|2019-12-19|[Create hosts in an ApsaraDB for MyBase dedicated cluster]()|
|PostgreSQL|New version|The RDS Basic Edition is supported for RDS instances that run PostgreSQL 12.|2019-12-17|[Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md)|
|PostgreSQL|SSL|SSL encryption can be enabled and disabled in the ApsaraDB RDS console. This applies to RDS instances that use standard or enhanced SSDs.|2019-12-17|[Configure data encryption for an RDS PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Data security/Configure data encryption for an RDS PostgreSQL instance.md)|
|PostgreSQL|VSwitch change|Changes to VSwitches are supported. This applies to RDS instances that use standard or enhanced SSDs.|2019-12-17|[Switch to a new VSwitch for an RDS PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Network, VPC, and VSwitch/Switch to a new VSwitch for an RDS PostgreSQL instance.md)|
|PostgreSQL|Service account authorization|The authorization of a temporary service account is supported in the ApsaraDB RDS console. This service account is used by Alibaba Cloud technical support to troubleshoot instance issues.|2019-12-17|[t1849622.md\#](/intl.en-US/RDS PostgreSQL Database/Account/Authorize the service account of an RDS PostgreSQL instance.md)|
|MySQL|Dedicated proxy|The dedicated proxy feature is supported for RDS instances that run MySQL 5.7 or 8.0 on RDS High-availability Edition with standard or enhanced SSDs.|2019-12-17|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|

## November 2019

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|New instance type|General-purpose instance types are supported for RDS instances that run MySQL 5.7 on RDS Enterprise Edition.|2019-11-24|[Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md)|
|MySQL|SQL Explorer|The SQL Explorer feature is supported for RDS instances that run MySQL 5.7 on RDS Enterprise Edition.|2019-11-21|[SQL Explorer](/intl.en-US/RDS MySQL Database/Audit/SQL Explorer.md)|
|MySQL|Read-only instance|Read-only instances are supported for RDS instances that run MySQL 5.7 on RDS Enterprise Edition.|2019-11-19|[Create a read-only ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Read-only instances/Create a read-only ApsaraDB RDS for MySQL instance.md)|
|MySQL|New instance type|New instance types that provide 12, 24, 52, and 104 CPU cores are introduced to RDS instances that run the RDS High-availability Edition with standard or enhanced SSDs.|2019-11-15|[Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md)|
|PostgreSQL|Data reads and writes on foreign MySQL tables|The mysql\_fdw plug-in is provided for RDS instances that run PostgreSQL 10 with standard or enhanced SSDs. This allows you to directly read and write data to ApsaraDB RDS for MySQL instances or user-created MySQL databases.|2019-11-13|[Use mysql\_fdw to read and write data to a MySQL database](/intl.en-US/Proprietary AliPG/Run cross-database queries/Use mysql_fdw to read and write data to a MySQL database.md)|
|MySQL|New instance type|A new instance type that provides one CPU core and 1 GB of memory is introduced to RDS instances that run MySQL 8.0 on RDS Basic Edition.|2019-11-12|[Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md)|

## October 2019

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|Dedicated proxy|The dedicated proxy feature is provided for RDS instances that run MySQL 5.7 on RDS High-availability Edition with local SSDs. This feature provides the read/write splitting and short-lived connection optimization capabilities.|2019-10-28|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|
|PostgreSQL|Removal of binding relationships between storage capacity sizes and instance types|The binding relationships between storage capacity sizes and instance types are removed. You can purchase any amount of storage capacity for the selected instance type. This reduces the costs of storage- and compute-intensive workloads.|2019-10-24|[Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md)|
|PostgreSQL|Data reads and writes on foreign PostgreSQL tables|The dblink and postgres\_fdw plug-ins are provided for RDS instances that run PostgreSQL 11 with standard or enhanced SSDs. These plug-ins allow you to manage tables across instances.|2019-10-24|[Use the dblink and postgre\_fdw plug-ins for cross-database operations](/intl.en-US/Proprietary AliPG/Use the dblink and postgre_fdw plug-ins for cross-database operations.md)|
|PostgreSQL|Up to 32-TB storage capacity|The maximum storage capacity is increased. The limit is 6 TB for RDS instances that run the RDS Basic Edition and for those that run the RDS High-availability Edition with local or standard SSDs. The limit is 32 TB for RDS instances that run the RDS High-availability Edition with enhanced SSDs.|2019-10-24|[Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md)|
|PostgreSQL|PostgreSQL 11|PostgreSQL 11 is supported.|2019-10-24|[Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md)|
|SQL Server|SQL Server 2017 SE|SQL Server 2017 SE is supported. ApsaraDB RDS has now covered all of the SQL Server versions within the range of 2012 to 2017 in various editions.|2019-10-18|[Functions supported by different versions and editions of SQL Server](/intl.en-US/RDS SQL Server Database/Quick start/Functions supported by different versions and editions of SQL Server.md)|
|SQL Server|ESSD PL2 and ESSD PL3|Enhanced SSDs of PL2 and PL3 are released in all regions in mainland China. An enhanced SSD of PL 3 delivers 20 times more input/output operations per second \(IOPS\) and 11 times more throughput than an enhanced SSD of PL1. You can use enhanced SSDs of PL2 or PL3 to handle a large number of concurrent I/O requests at stable read/write latencies.|2019-10-17|[Storage types](/intl.en-US/Product Introduction/Storage types.md)|
|MySQL|Dedicated proxy|The dedicated proxy feature is provided for RDS instances that run MySQL 8.0 on RDS High-availability Edition with local SSDs. This feature provides the read/write splitting and short-lived connection optimization capabilities.|2019-10-15|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|
|MySQL|Price adjustment|The prices of RDS instances with standard or enhanced SSDs are reduced by up to 50%.|2019-10-15|[Pricing, billable items, and billing methods](/intl.en-US/Purchase Guide/Pricing, billable items, and billing methods.md)|
|SQL Server|Multi-zone deployment|Multi-zone deployment is supported for RDS instances that span zones A and C in the China \(Zhangjiakou\) region.|2019-10-10|[Create an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)|

## September 2019

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|Dedicated Instance|The storage capacity range is adjusted for RDS instances that use local SSDs. The adjustment applies to the dedicated instance family.|2019-09-18|[Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md)|
|MySQL|Upgrade from Basic Edition to High-availability Edition|The upgrade from the RDS Basic Edition to the RDS High-availability Edition is supported.|2019-09-15|[Change the specifications of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md)|
|MySQL|New instance type|A new instance type that provides 90 CPU cores and 720 GB of memory is introduced. The new instance type applies to the dedicated host instance family.|2019-09-15|[Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md)|
|All|New buy page|A new ApsaraDB RDS buy page is released.|2019-09-12|[Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)|
|MySQL|VPC change|Changes to virtual private clouds \(VPCs\) are supported.|2019-09-12|[Switch to a new VPC and VSwitch for an RDS MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Switch to a new VPC and VSwitch for an RDS MySQL instance.md)|
|PostgreSQL|Disk encryption|SSL encryption and disk encryption are supported. These encryption features can work together to better protect your data.|2019-09-04|[Configure data encryption for an RDS PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Data security/Configure data encryption for an RDS PostgreSQL instance.md)|

## August 2019

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|Parameter template|Parameter templates are provided. You can manage a number of instance parameters at a time by using a parameter template.|2019-08-27|[Use a parameter template to manage parameters](/intl.en-US/RDS MySQL Database/Instance parameters/Use a parameter template to manage parameters.md)|
|MySQL|Disabling SSL encryption|The disabling of SSL encryption is supported.|2019-08-23|[Configure SSL encryption on an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure SSL encryption on an ApsaraDB RDS for MySQL instance.md)|
|MySQL|Temporary disabling of automatic failover|The temporary disabling of automatic failover for up to one week is supported.|2019-08-22|[Perform a manual or automatic switchover of services between a primary ApsaraDB RDS for MySQL instance and its secondary instance](/intl.en-US/RDS MySQL Database/Instance Change/Perform a manual or automatic switchover of services between a primary ApsaraDB RDS for MySQL instance and its secondary instance.md)|
|MySQL|Database- and table-level backup and restoration|Backup and restoration at the database and table levels are supported for RDS instances that run MySQL 5.6 or 5.7.|2019-08-20|[Restore individual databases and tables of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md)|
|MySQL|Instance rebuilding from the recycle bin|The rebuilding of subscription RDS instances from the recycle bin is supported. This applies when the RDS instances are locked due to overdue payments.|2019-08-16|[Manage ApsaraDB RDS for MySQL instances in the recycle bin](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Manage ApsaraDB RDS for MySQL instances in the recycle bin.md)|
|MySQL|Cross-region backup|The cross-region backup feature is supported. You can back up an RDS instance and store the backup data to a region where that instance does not reside.|2019-08-13|[Back up an ApsaraDB RDS for MySQL instance across regions](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance across regions.md)|
|MySQL|SQL Explorer|The time range to query logs in the SQL Explorer feature is refined to 24 hours or less.|2019-08-08|[SQL Explorer](/intl.en-US/RDS MySQL Database/Audit/SQL Explorer.md)|
|MySQL|SQL Explorer|The SQL Explorer feature is supported for RDS instances that run MySQL 5.7 on RDS High-availability Edition with standard or enhanced SSDs. This feature logs all of the SQL statements that are executed.|2019-08-01|[SQL Explorer](/intl.en-US/RDS MySQL Database/Audit/SQL Explorer.md)|

## July 2019

|Database engine|Feature|Description|Release date|Documentation|
|---------------|-------|-----------|------------|-------------|
|MySQL|TDE|TDE with BYOKs is supported for RDS instances that run MySQL 5.6.|2019-07-30|[Configure TDE for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md)|
|MySQL|VPC endpoint change|Changes to endpoints are supported for RDS instances that reside in VPCs.|2019-07-29|[Configure endpoints]()|
|MySQL|Up to 16-TB storage capacity|The maximum storage capacity is increased. The limit is up to 16 TB for RDS instances that run MySQL 5.7 or 8.0 on RDS High-availability Edition with enhanced SSDs.|2019-07-29|[Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md)|
|SQL Server|SQL Server 2016 EE Basic|SQL Server 2016 EE Basic is supported for RDS instances in the dedicated instance family.|2019-07-25|[Create an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)|
|All|Five-year subscription|Five-year subscription is supported for RDS instances that run MySQL, SQL Server, PPAS, PostgreSQL, or MariaDB.|2019-07-20|[Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)|
|SQL Server|Upgrade from Basic Edition to High-availability Edition|The upgrade from the RDS Basic Edition to the RDS High-availability Edition is supported. You can perform the upgrade on the Basic Information page of the ApsaraDB RDS console.|2019-07-17|[Upgrade from Basic Edition to High-availability Edition](/intl.en-US/RDS SQL Server Database/Version upgrade/Upgrade from Basic Edition to High-availability Edition.md)|

