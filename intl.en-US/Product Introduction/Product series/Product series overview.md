# Product series overview {#concept_t5k_fkv_tdb .concept}

RDS instances are divided into three series: Basic Edition, High-availability Edition, and Cluster Edition. Different instance types support different series. For more information, see [Instance type overview](intl.en-US/Product Introduction/Instance types/Instance type overview.md).

## Comparison between different series {#section_s3n_3kv_tdb .section}

|Series|Description|Applicable scenarios|
|------|-----------|--------------------|
|Basic Edition|It provides a single node and separates computing from storage, and is extremely cost-effective. For more information, see [Basic Edition](intl.en-US/Product Introduction/Product series/Basic Edition.md).| -   Personal learning
-   Small websites
-   Development and test environments for small- and medium-sized enterprises

 |
|High-availability Edition|It adopts the high-availability architecture with one master node and one slave node. It is applicable to over 80% of scenarios.| -   Production databases of large-and medium-sized enterprises
-   Databases for the Internet, Internet of things \(IoT\), online retail, logistics, gaming, and other industries

 |
|Cluster Edition|Only RDS for SQL Server 2017 Enterprise provides this series. Based on the AlwaysOn technology, it provides one master node, one slave node, and up to seven read-only nodes that horizontally scale read capabilities. For more information, see [Cluster Edition \(AlwaysOn Edition\)](intl.en-US/Product Introduction/Product series/Cluster Edition (AlwaysOn Edition).md).|Production databases of large- and medium-sized enterprises, such as online retail and automobile companies|

## RDS for MySQL {#section_gjb_nmv_tdb .section}

|Function|Basic Edition|High-availability Edition|
|MySQL 5.7|MySQL 5.5/5.6/5.7|
|--------|-------------|-------------------------|
|---------|-----------------|
|[Monitoring](../../../../../intl.en-US/User Guide/Monitoring and Alarming/Set the monitoring frequency.md) and [alarms](../../../../../intl.en-US/User Guide/Monitoring and Alarming/Set monitoring rules.md)|Supported|Supported|
|[IP whitelist](../../../../../intl.en-US/User Guide/Security/Set the whitelist.md)|Supported|Supported|
|[Backup and recovery](../../../../../intl.en-US/User Guide/Backup/Back up RDS data.md)|Supported|Supported|
|[Parameter settings](../../../../../intl.en-US/User Guide/Instance management/Set instance parameters/Set parameters through the RDS console.md)|Supported|Supported|
|[Log management](../../../../../intl.en-US/User Guide/Log management.md)|Not supported|Supported|
|[Master/Slave switchover](../../../../../intl.en-US/User Guide/Instance management/Switch between master and slave instances.md)|Not supported|Supported|
|[SSL](../../../../../intl.en-US/User Guide/Security/Set SSL encryption.md)|Not supported|Supported|
|[TDE](../../../../../intl.en-US/User Guide/Security/Set TDE.md)|Not supported|Supported|
|[Migrate to another zone](../../../../../intl.en-US/User Guide/Instance management/Migrate instance across zones.md)|Not supported|Supported|
|[Read/Write splitting](../../../../../intl.en-US/User Guide/Read__write splitting/Introduction to read__write splitting.md)|Not supported|Supported|
|[Read-only instance](../../../../../intl.en-US/Quick Start for MySQL/Scale instances/Read-only instance/Introduction to read-only instances.md)|Not supported|Supported \(not free\)|
|[SQL audit](../../../../../intl.en-US/User Guide/Security/SQL audit.md)|Not supported|Supported \(not free\)|

**Note:** 

-   MySQL 5.5 High-availability Edition does not support SSL.
-   MySQL 5.7 High-availability Edition based on local SSDs does not support TDE.
-   MySQL 5.7 High-availability Edition based on cloud SSDs does not support SSL, TDE, performance tuning, read-only instances, read/write splitting, SQL audit, or migrations to another zone.

## RDS for SQL Server {#section_w41_mmr_t2b .section}

Please see [Function differences between SQL Server versions](https://www.alibabacloud.com/help/doc-detail/44534.htm).

## RDS for PostgreSQL/PPAS {#section_lfs_4mr_t2b .section}

|Function|Basic Edition|High-availability Edition|
|PostgreSQL 10| PostgreSQL 9.4 or 10

 |
|--------|-------------|-------------------------|
|-------------|------------------------|
|[Monitoring](../../../../../intl.en-US/User Guide/Monitoring and Alarming/Set the monitoring frequency.md) and [alarms](../../../../../intl.en-US/User Guide/Monitoring and Alarming/Set monitoring rules.md)|Supported|Supported|
|[IP whitelist](../../../../../intl.en-US/User Guide/Security/Set the whitelist.md)|Supported|Supported|
|[Backup and recovery](../../../../../intl.en-US/User Guide/Backup/Back up RDS data.md)|Supported|Supported|
|[Parameter settings](../../../../../intl.en-US/User Guide/Instance management/Set instance parameters/Set parameters through the RDS console.md)|Supported|Supported|
|[Log management](../../../../../intl.en-US/User Guide/Log management.md)|Not supported|Supported|
|[SQL audit](../../../../../intl.en-US/User Guide/Security/SQL audit.md)|Not supported|Supported|
|[Migrate to another zone](../../../../../intl.en-US/User Guide/Instance management/Migrate instance across zones.md)|Not supported|Supported|
|[Master/Slave switchover](../../../../../intl.en-US/User Guide/Instance management/Switch between master and slave instances.md)|Not supported|Supported|

## RDS for MariaDB {#section_spq_lkf_2fb .section}

|Function|High-availability Edition|
|--------|-------------------------|
|[Monitoring](../../../../../intl.en-US/User Guide/Monitoring and Alarming/Set the monitoring frequency.md) and [alarms](../../../../../intl.en-US/User Guide/Monitoring and Alarming/Set monitoring rules.md)|Supported|
|[IP whitelist](../../../../../intl.en-US/User Guide/Security/Set the whitelist.md)|Supported|
|[Backup and recovery](../../../../../intl.en-US/User Guide/Backup/Back up RDS data.md)|Supported|
|[Parameter settings](../../../../../intl.en-US/User Guide/Instance management/Set instance parameters/Set parameters through the RDS console.md)|Supported|
|[Log management](../../../../../intl.en-US/User Guide/Log management.md)|Supported|
|[Master/Slave switchover](../../../../../intl.en-US/User Guide/Instance management/Switch between master and slave instances.md)|Supported|
|[SSL](../../../../../intl.en-US/User Guide/Security/Set SSL encryption.md)|Supported|

