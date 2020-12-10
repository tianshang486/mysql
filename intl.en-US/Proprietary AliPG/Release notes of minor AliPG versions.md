# Release notes of minor AliPG versions

This topic describes the release notes of minor AliPG versions.

## PostgreSQL 12

|Minor version|Description|
|-------------|-----------|
|20201130|-   New features:
    -   AliPG is upgraded to ensure compatibility with the Community edition of PostgreSQL 12.4.
    -   New permissions are granted to privileged accounts. These permissions are used to create accounts that are authorized to replicate streams.
    -   New permissions are granted to privileged accounts. These permissions are used to create triggers.
    -   The rds\_auditlog\_max\_query\_length parameter is introduced. It allows you to specify the maximum length of SQL logs.
    -   The [pg\_cron](/intl.en-US/Proprietary AliPG/Use the pg_cron plug-in to configure scheduled tasks.md) plug-in is upgraded. It allows you to create and execute cross-instance tasks. It also provides a table named cron.job\_log. You can view task execution records in this table.
    -   The [pg\_freespacemap](https://www.postgresql.org/docs/12/pgfreespacemap.html) plug-in is supported.
    -   Spatio-temporal memory topology indexes are supported by the [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in.
    -   The [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in is upgraded to version 3.2.
-   Bugs fixed:
    -   The bug that causes check errors when you migrate data by using Alibaba Cloud Data Transmission Service \(DTS\) is fixed. These check errors occur if you enable or commit more than one child transaction during the migration.
    -   The CVE-2020-14349 vulnerability is fixed. This vulnerability prevents ApsaraDB RDS from properly cleaning search paths during logical replications.
    -   The CVE-2020-14350 vulnerability is fixed. This vulnerability allows `CREATE EXTENSION` statements to include uncontrollable search path elements.
    -   The CVE-2020-25695 vulnerability is fixed. This vulnerability allows you to create permanent objects and to invoke all SQL functions as a super user. |
|20200830|-   New features:
    -   The [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in is upgraded to version 3.0.
    -   The [sql\_firewall](/intl.en-US/Proprietary AliPG/Use the sql_firewall plug-in.md) plug-in is introduced to prevent an injection of malicious SQL statements.
    -   The [pg\_bigm](/intl.en-US/Proprietary AliPG/Fuzzy query (PG_ bigm).md) plug-in is introduced to implement fuzzy match.
    -   The [TimescaleDB](/intl.en-US/Proprietary AliPG/Query vertical industry-specific data/Use the TimescaleDB plug-in.md) plug-in is introduced to process time series data.
-   Bugs fixed:
    -   The bug that prevents the backend from identifying the `rds_` prefix in parameters is fixed.
    -   The bug that prevents you from properly creating and using the pg\_cron plug-in is fixed.
    -   The bug that prevents you from loading the RDKit plug-in due to the lack of dependencies is fixed. |
|20200421|-   New features:
    -   AliPG is upgraded to ensure compatibility with the Community edition of PostgreSQL 12.2.
    -   The [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in is upgraded to version 2.7.
    -   The [HLL](/intl.en-US/Proprietary AliPG/Use the hll plug-in.md) plug-in of version 2.14 is supported.
    -   The [PL/Proxy](/intl.en-US/Proprietary AliPG/Use the PL/Proxy plug-in for horizontal sharding.md) plug-in of version 2.9.0 is supported.
    -   The tsm\_system\_rows plug-in of version 1.0 is supported.
    -   The tsm\_system\_time plug-in of version 1.0 is supported.
    -   The [smlar](/intl.en-US/Proprietary AliPG/Query vertical industry-specific data/Use the smlar plug-in.md) plug-in of version 1.0 is supported.
    -   The [tds\_fdw](/intl.en-US/Proprietary AliPG/Run cross-database queries/Use the tds_fdw plug-in.md) plug-in of version 1.0 is supported.
-   Bug fixed:

The bug that causes RDS instances to restart due to timed-out logical subscriptions is fixed. |
|20200221|-   New features:
    -   The reservation for a specific number of connections is supported for the rds\_superuser role. If you are authorized with this role, you can connect to an RDS instance to troubleshoot issues even if the number of established connections to the RDS instance reaches the upper limit.
    -   The [wal2json](/intl.en-US/Proprietary AliPG/Use the wal2json plug-in.md) plug-in is supported.
    -   The [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in is upgraded to version 2.6.
-   Bugs fixed:

Some permission-related bugs are fixed. |
|20191230|New features:

-   The [pg\_roaringbitmap](/intl.en-US/Proprietary AliPG/Query vertical industry-specific data/Use the roaringbitmap plug-in.md), RDKit, [mysql\_fdw](/intl.en-US/Proprietary AliPG/Run cross-database queries/Use mysql_fdw to read and write data to a MySQL database.md), and Ganos plug-ins are supported.
-   New permissions are granted to privileged accounts. These permissions are used to publish all tables at a time and create subscriptions. |

## PostgreSQL 11

|Minor version|Description|
|-------------|-----------|
|20201130|-   New features:
    -   AliPG is upgraded to ensure compatibility with the Community edition of PostgreSQL 11.9.
    -   New permissions are granted to privileged accounts. These permissions are used to create accounts that are authorized to replicate streams.
    -   New permissions are granted to privileged accounts. These permissions are used to create triggers.
    -   The rds\_auditlog\_max\_query\_length parameter is introduced. It allows you to specify the maximum length of SQL logs.
    -   The pg\_cron plug-in is upgraded. It allows you to create and execute cross-instance tasks. It also provides a table named cron.job\_log. You can view task execution records in this table.
    -   The [pg\_freespacemap](https://www.postgresql.org/docs/11/pgfreespacemap.html) plug-in is supported.
    -   Spatio-temporal memory topology indexes are supported by the [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in.
    -   The [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in is upgraded to version 3.2.
-   Bugs fixed:
    -   The bug that causes check errors when you migrate data by using Alibaba Cloud DTS is fixed. These check errors occur if you enable or commit more than one child transaction during the migration.
    -   The CVE-2020-14349 vulnerability is fixed. This vulnerability prevents ApsaraDB RDS from properly cleaning search paths during logical replications.
    -   The CVE-2020-14350 vulnerability is fixed. This vulnerability allows `CREATE EXTENSION` statements to include uncontrollable search path elements.
    -   The CVE-2020-25695 vulnerability is fixed. This vulnerability allows you to create permanent objects and to invoke all SQL functions as a super user. |
|20200830|-   New features:
    -   The [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in is upgraded to version 3.0.
    -   The [sql\_firewall](/intl.en-US/Proprietary AliPG/Use the sql_firewall plug-in.md) plug-in is introduced to prevent an injection of malicious SQL statements.
    -   The [pg\_bigm](/intl.en-US/Proprietary AliPG/Fuzzy query (PG_ bigm).md) plug-in is introduced to implement fuzzy match.
    -   The [ZomboDB](/intl.en-US/Proprietary AliPG/Use the ZomboDB plug-in to integrate with Elasticsearch.md) plug-in is introduced to implement text search and analysis.
-   Bugs fixed:
    -   The bug that prevents the backend from identifying the `rds_` prefix in parameters is fixed.
    -   The bug that causes a secondary RDS instance to exit is fixed. This error occurs if the failover slot has the same name as the streaming replication slot.
    -   The bug that prevents you from properly creating and using the pg\_cron plug-in is fixed.
    -   The bug in a global variable of the PASE plug-in is fixed. |
|20200610|New features:

-   The [TimescaleDB](/intl.en-US/Proprietary AliPG/Query vertical industry-specific data/Use the TimescaleDB plug-in.md) plug-in of version 1.7.1 is supported.
-   The pageinspect plug-in is supported for the rds\_superuser role.
-   The rds\_superuser role is authorized to grant the replication permissions to other users. |
|20200511|-   New feature:

The [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in is upgraded to version 2.8.

-   Bug fixed:

The bug that causes the PASE plug-in to slowly run INSERT statements on HNSW indexes is fixed. |
|20200421|New features:

-   The failover slot function is supported. For more information, see [Use the failover slot feature for logical subscriptions](/intl.en-US/Proprietary AliPG/Use the failover slot feature for logical subscriptions.md).
-   The [PL/Proxy](/intl.en-US/Proprietary AliPG/Use the PL/Proxy plug-in for horizontal sharding.md) plug-in of version 2.9.0 is supported.
-   The tsm\_system\_rows plug-in of version 1.0 is supported.
-   The tsm\_system\_time plug-in of version 1.0 is supported.
-   The [smlar](/intl.en-US/Proprietary AliPG/Query vertical industry-specific data/Use the smlar plug-in.md) plug-in of version 1.0 is supported. |
|20200402|-   New features:
    -   The [HLL](/intl.en-US/Proprietary AliPG/Use the hll plug-in.md) plug-in of version 2.14 is supported. It allows ApsaraDB RDS to support the HLL data type, respond to queries in milliseconds, and analyze approximate data at low costs and high speeds. For example, you can query page views \(PVs\) and unique visitors \(UVs\) in real time and determine whether the analyzed approximate data contains specified characteristic tags.
    -   The [oss\_fdw](/intl.en-US/Proprietary AliPG/Run cross-database queries/Read and write external data files by using oss_fdw.md) plug-in of version 1.1 is supported. It allows you to store infrequently requested historical data to Alibaba Cloud Object Storage Service \(OSS\) buckets. This reduces storage costs.
    -   The [tds\_fdw](/intl.en-US/Proprietary AliPG/Run cross-database queries/Use the tds_fdw plug-in.md) plug-in of version 2.0.1 is supported. It allows you to initiate requests on an RDS instance to query data from a Sybase or SQL Server database without the need to perform extract, transform and load \(ETL\) operations. It also allows you to migrate data between an RDS instance and a Sybase or SQL Server database.
-   Upgraded plug-ins:
    -   The [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in is upgraded to version 2.7.
    -   The [wal2json](/intl.en-US/Proprietary AliPG/Use the wal2json plug-in.md) plug-in is upgraded to version 2.2.
-   Performance optimization:

The `shutdown -m fast` command is optimized. |
|20191218|New features:

-   The [PASE](/intl.en-US/Proprietary AliPG/Query vertical industry-specific data/Use the PASE plug-in.md) plug-in is introduced to support indexes that are used to recognize images.
-   New permissions are granted to privileged accounts. These permissions are used to publish all tables at a time and create subscriptions. |

## PostgreSQL 10

|Minor version|Description|
|-------------|-----------|
|20201130|-   New features:
    -   AliPG is upgraded to ensure compatibility with the Community edition of PostgreSQL 10.14.
    -   New permissions are granted to privileged accounts. These permissions are used to create accounts that are authorized to replicate streams.
    -   New permissions are granted to privileged accounts. These permissions are used to create triggers.
    -   The rds\_auditlog\_max\_query\_length parameter is introduced. It allows you to specify the maximum length of SQL logs.
    -   The pg\_cron plug-in is upgraded. It allows you to create and execute cross-instance tasks. It also provides a table named cron.job\_log. You can view task execution records in this table.
    -   The [pg\_freespacemap](https://www.postgresql.org/docs/10/pgfreespacemap.html) plug-in is supported.
    -   Spatio-temporal memory topology indexes are supported by the [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in.
    -   The [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in is upgraded to version 3.2.
-   Bugs fixed:
    -   The bug that causes check errors when you migrate data by using Alibaba Cloud DTS is fixed. These check errors occur if you enable or commit more than one child transaction during the migration.
    -   The CVE-2020-14349 vulnerability is fixed. This vulnerability prevents ApsaraDB RDS from properly cleaning search paths during logical replications.
    -   The CVE-2020-14350 vulnerability is fixed. This vulnerability allows `CREATE EXTENSION` statements to include uncontrollable search path elements.
    -   The CVE-2020-25695 vulnerability is fixed. This vulnerability allows you to create permanent objects and to invoke all SQL functions as a super user. |
|20200830|-   New features:
    -   The [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in is upgraded to version 3.0.
    -   The [sql\_firewall](/intl.en-US/Proprietary AliPG/Use the sql_firewall plug-in.md) plug-in is introduced to prevent an injection of malicious SQL statements.
    -   The [pg\_bigm](/intl.en-US/Proprietary AliPG/Fuzzy query (PG_ bigm).md) plug-in is introduced to implement fuzzy match.
-   Bug fixed:

The bug that prevents you from properly creating and using the pg\_cron plug-in is fixed. |
|20200212|-   New features:
    -   The reservation for a specific number of connections is supported for the rds\_superuser role. If you are authorized with this role, you can connect to an RDS instance to troubleshoot issues even if the number of established connections to the RDS instance reaches the upper limit.
    -   The [Ganos](/intl.en-US/Spatio-temporal Database/Overview.md) plug-in is upgraded to version 2.6.
-   Bug fixed:

The bug that causes a long wait for streaming replication is fixed. |
|20190703|-   New features:
    -   AliPG is upgraded to version 10.9.
    -   The change from synchronous replication to asynchronous replication is supported when the ongoing replication times out.
-   Bugs fixed:
    -   The bug that prevents you from properly creating the pg\_hint\_plan plug-in is fixed.
    -   The bug that causes external RUM indexing to fail is fixed. |

## PostgreSQL 9.4

|Minor version|Description|
|-------------|-----------|
|20201130|Bugs fixed:

-   The CVE-2020-25694 vulnerability is fixed. This vulnerability may cause ApsaraDB RDS to lose security parameters when RDS instances are switched over to other connections. If security parameters are lost, RDS instances may be attacked.
-   The CVE-2020-25695 vulnerability is fixed. This vulnerability allows you to create permanent objects and to invoke all SQL functions as a super user.
-   The CVE-2020-25696 vulnerability is fixed. This vulnerability allows the gset command to overwrite variables that are processed based on specified conditions. |
|20200623|-   New features:
    -   The [wal2json](/intl.en-US/Proprietary AliPG/Use the wal2json plug-in.md) plug-in is upgraded to version 2.2.
    -   The xml2 plug-in of version 1.0 is supported.
-   Bug fixed:

The bug that causes memory exhaustion when the wal2json plug-in runs is fixed. |
|20200210|New feature:

The reservation for a specific number of connections is supported for the rds\_superuser role. If you are authorized with this role, you can connect to an RDS instance to troubleshoot issues even if the number of established connections to the RDS instance reaches the upper limit. |
|20190601|AliPG is upgraded to version 9.4.19. |

