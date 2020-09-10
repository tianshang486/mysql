# Release Notes of Minor AliPG Versions

This topic describes the release notes of minor AliPG versions.

## PostgreSQL 12

20200421

-   New features:
    -   The engine is upgraded to be compatible with PostgreSQL 12.2 of the community edition.
    -   The version of the ganos plug-in is upgraded to 2.7.
    -   The HLL plug-in of version 2.14 is supported.
    -   The PL/Proxy plug-in of version 2.9.0 is supported.
    -   The tsm\_system\_rows plug-in of version 1.0 is supported.
    -   The tsm\_system\_time plug-in of version 1.0 is supported.
    -   The smlar plug-in of version 1.0 is supported.
    -   The tds\_fdw plug-in of version 1.0 is supported.
-   Bug fixed:

    The bug that causes instances to restart due to logical subscription timeout is fixed.


20200221

-   New features:
    -   A specified number of connections can be reserved for users with the rds\_superuser role. This allows you to connect to the instance and troubleshoot issues even if the number of established connections reaches the upper limit.
    -   The [wal2json](/intl.en-US/AliPG Kernel/Plug-ins/Use the wal2json plug-in.md) plug-in is supported.
    -   The version of the ganos plug-in is upgraded to 2.6.
-   Bug fixed:

    Some permission issues are fixed.


20191230

New features:

-   The [pg\_roaringbitmap](/intl.en-US/AliPG Kernel/Plug-ins/Query vertical industry-specific data/Use the roaringbitmap plug-in.md), rdkit, [mysql\_fdw](/intl.en-US/AliPG Kernel/Plug-ins/Run cross-database queries/Use mysql_fdw to read and write data to a MySQL database.md), and ganos plug-ins are supported.
-   Permissions to publish all tables at a time and create subscriptions are granted to privileged accounts.

## PostgreSQL 11

20200610

New features:

-   The [timescaledb](/intl.en-US/AliPG Kernel/Plug-ins/Query vertical industry-specific data/Use the TimescaleDB plug-in.md) plug-in of version 1.7.1 is supported.
-   The pageinspect plug-in is available for users with the rds\_superuser role.
-   Users with the rds\_superuser role are allowed to grant other users replication permissions.

20200511

-   New feature:

    The version of the ganos plug-in is upgraded to 2.8.

-   Bug fixed:

    The bug that INSERT operations are slow on HNSW indexes is fixed for the PASE plug-in.


20200421

New features:

-   The failover slot function is supported. For more information, see [Failover slot](/intl.en-US/RDS PostgreSQL Database/Best Practices/Failover slot.md).
-   The PL/Proxy plug-in of version 2.9.0 is supported.
-   The tsm\_system\_rows plug-in of version 1.0 is supported.
-   The tsm\_system\_time plug-in of version 1.0 is supported.
-   The smlar plug-in of version 1.0 is supported.

20200402

-   New features:
    -   The HLL plug-in of version 2.14 is supported. It supports the HLL data type and responds to queries in milliseconds. It is suitable for approximation data analysis, such as real-time PV, UV, and feature label queries. This reduces costs and improves efficiency.
    -   The oss\_fdw plug-in of version 1.1 is supported. It can be used to expand database storage to OSS. You can store historical data that is not frequently queried in OSS buckets. This reduces storage costs and meets requirements for infrequent queries.
    -   The tds\_fdw plug-in of version 2.0.1 is supported. You can query data in Sybase or SQL Server databases from PostgreSQL databases without extract, transform and load \(ETL\). This allows you to query and migrate data across different types of databases.
-   Plug-in upgrade:
    -   The version of the ganos plug-in is upgraded to 2.7.
    -   The version of the wal2json plug-in is upgraded to 2.2.
-   Performance optimization:

    The `shutdown -m fast` command is optimized.


20191218

New features:

-   The [PASE](/intl.en-US/AliPG Kernel/Plug-ins/Query vertical industry-specific data/Use the PASE plug-in.md) plug-in is supported to provide indexes for image recognition.
-   Permissions to publish all tables at a time and create subscriptions are granted to privileged accounts.

## PostgreSQL 10

20200212

-   New features:
    -   A specified number of connections can be reserved for users with the rds\_superuser role. This allows you to connect to the instance and troubleshoot issues even if the number of established connections reaches the upper limit.
    -   The version of the ganos plug-in is upgraded to 2.6.
-   Bug fixed:

    The bug that causes long waits in streaming replication is fixed.


20190703

-   New features:
    -   The engine version is upgraded to 10.9.
    -   The change from synchronous replication to asynchronous replication when replication tasks time out is supported.
-   Bugs fixed:
    -   The bug that causes errors when pg\_hint\_plan is created is fixed.
    -   The bug that causes failures in external RUM indexing is fixed.

## PostgreSQL 9.4

20200623

-   New features:
    -   The version of the wal2json plug-in is upgraded to 2.2.
    -   The xml2 plug-in of version 1.0 is supported.
-   Bug fixed:

    The bug that the wal2json plug-in causes memory exhaustion is fixed.


20200210

A specified number of connections can be reserved for users with the rds\_superuser role. This allows you to connect to the instance and troubleshoot issues even if the number of established connections reaches the upper limit.

20190601

The engine version is upgraded to 9.4.19.

