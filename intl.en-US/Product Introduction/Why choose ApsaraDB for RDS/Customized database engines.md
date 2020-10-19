# Customized database engines

Alibaba Cloud customizes database engines based on the community editions of native MySQL and PostgreSQL to provide more advanced features.

## AliSQL

AliSQL is an independent MySQL branch that is developed by Alibaba Cloud. AliSQL provides all of the features that are available in the MySQL Community edition. AliSQL also provides some similar features that you can find in the MySQL Enterprise edition. These similar features include enterprise-grade backup and restoration, thread pool, and parallel query. In addition, AliSQL provides Oracle-compatible features, such as Sequence engine. ApsaraDB RDS for MySQL with AliSQL provides all the basic features of MySQL and a wide range of advanced features such as enterprise-grade security, backup and restoration, monitoring, performance optimization, and read-only instance.

AliSQL provides a number of innovative features that are designed to improve functionality, performance, stability, and security, including:

-   [Thread Pool](/intl.en-US/Proprietary AliSQL/Feature/Thread Pool.md)

    This feature uses the Listener-Worker model to improve the connection performance of AliSQL. It optimizes the concurrency control for different types of operations based on their priorities. This allows ApsaraDB for RDS to ensure high performance when it processes a large number of concurrent requests.

-   [Statement outline](/intl.en-US/Proprietary AliSQL/Feature/Statement outline.md)

    This feature uses optimizer and index hints to ensure the stability of ApsaraDB for RDS when SQL query plans change due to data update, index addition or deletion, or parameter adjustment.

-   [A new version is available.](/intl.en-US/Proprietary AliSQL/Performance/Fast query cache.md)

    The fast query cache is developed by Alibaba Cloud based on the native MySQL query cache. The fast query cache uses a new design and implementation mechanism to increase the query performance of ApsaraDB for RDS. The fast query cache also optimizes concurrency control, memory management, and caching.

-   [Binlog in Redo](/intl.en-US/Proprietary AliSQL/Performance/Binlog in Redo.md)

    This feature synchronously writes binary logs to the redo log file when a transaction is committed. This reduces operations on disks and improves database performance.

-   [Faster DDL](/intl.en-US/Proprietary AliSQL/Stability/Faster DDL.md)

    This feature is developed by the ApsaraDB for RDS team. It fixes defects in the cache maintenance logic that is used to manage data definition language \(DDL\) operations. It also provides the optimized buffer pool management mechanism to reduce competition for locks that are triggered by DDL operations. This feature ensures the DDL operation performance of ApsaraDB for RDS when it processes a regular number of requests.


For more information, see [Features of AliSQL](/intl.en-US/Proprietary AliSQL/Features of AliSQL.md).

## AliPG

Alibaba Cloud offers two PostgreSQL-compatible database services that run AliPG: ApsaraDB for RDS and ApsaraDB for MyBase. AliPG is a unified database engine that is developed by Alibaba Cloud. Since its commercial rollout in 2015, AliPG has been running stably for years to process a large number of workloads within Alibaba Group and on the cloud. AliPG supports the following major PostgreSQL versions: 9.4, 10, 11, and 12.

AliPG has the following benefits over the PostgreSQL Community edition:

-   Faster
    -   Image recognition and vector similarity-based search run tens of thousands of times faster on AliPG than on the PostgreSQL Community edition. For more information, see [Image recognition, face recognition, similarity-based retrieval, and similarity-based audience spotting](/intl.en-US/RDS PostgreSQL Database/Application Solutions/Image recognition, face recognition, similarity-based retrieval, and similarity-based audience spotting.md).
    -   Real-time marketing and user profiling run thousands of times faster on AliPG than on the PostgreSQL Community edition. For more information, see [Real-time precision marketing \(user selection\)](/intl.en-US/RDS PostgreSQL Database/Application Solutions/Real-time precision marketing (user selection).md).
    -   The GIS-based Mod operator processes mobile objects 50 times faster than the Mod operator that runs based on the open-source PostGIS. For more information, see [Overview](/intl.en-US/Spatio-temporal Database/Overview.md).
-   More stable

    AliPG uses the Platform as a Service \(PaaS\) architecture. This architecture allows you to transform traditional software from license-based service to subscription-based service. You can manage a large amount of metadata, optimize connections, and better isolate resources. You can also use tens of thousands of schemas per RDS instance.

-   More secure
    -   AliPG is certified based on leading national and international security standards, which empowers enterprises to increase institutional security scores in the financing and listing phases.
    -   AliPG provides the following security enhancements:
        -   Encrypts sensitive data that contains passwords. This sensitive data includes the dynamic views, shared memory, dblink plug-in, historical commands, and audit logs.
        -   Fixes bugs in the functions that you call in the PostgreSQL Community edition.
        -   Supports fully encrypted databases. For more information, see [Create a fully encrypted database on an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Data security/Create a fully encrypted database on an ApsaraDB RDS for PostgreSQL instance.md).
        -   Supports the semi-synchronous mode. This mode allows you to configure the following protection levels for your RDS instance: maximum protection, highest high availability, and optimal performance. For more information, see [Set the protection level of an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Instance/Set the protection level of an ApsaraDB RDS for PostgreSQL instance.md).
        -   Supports the failover slot function. This function prevents primary/secondary switchovers from affecting the reliability of logical replication. For more information, see [Failover slot](/intl.en-US/Proprietary AliPG/Failover slot.md).
-   More flexible and controllable \(For more information, see [What is ApsaraDB for MyBase?]()\)
    -   AliPG grants you the permissions to manage the operating systems on hosts in dedicated ApsaraDB for MyBase clusters. This allows you to manage your dedicated ApsaraDB for MyBase clusters based on your business requirements.
    -   AliPG allows you to customize overcommit ratios in the development, test, and staging environments. For example, you can configure 128 CPU cores for a host that provides only 64 CPU cores. This allows you to exclusively occupy resources in the production system to reduce the overall costs.

For more information about the features of AliPG, see [Functional modules of AliPG](/intl.en-US/Proprietary AliPG/Functional modules of AliPG.md).

