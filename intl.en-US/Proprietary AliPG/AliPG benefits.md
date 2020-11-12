# AliPG benefits

This topic describes the background information and benefits of AliPG.

## Background information

PostgreSQL is an advanced open source enterprise-grade database service. PostgreSQL was listed in the DB-Engines Ranking in 2017 and 2018. In 2019, PostgreSQL even won the O'Reilly Open Source Convention award \(OSCON\).

Alibaba Cloud offers two PostgreSQL-compatible database services that run AliPG: ApsaraDB RDS for PostgreSQL and ApsaraDB MyBase for PostgreSQL. AliPG is a unified database engine that is developed by Alibaba Cloud. Since its commercial rollout in 2015, AliPG has been running stably for years to process a large number of workloads within Alibaba Group and on the cloud. AliPG supports the following major PostgreSQL versions: 9.4, 10, 11, and 12.

## Alibaba Cloud database services that run AliPG

-   ApsaraDB RDS for PostgreSQL
-   ApsaraDB MyBase for PostgreSQL

## Supported PostgreSQL versions

-   12
-   11
-   10
-   9.4

## Benefits

AliPG is developed based on insights into the industry requirements. AliPG aims to help customers expand business boundaries.

AliPG has the following benefits over the PostgreSQL Community edition:

-   Faster
    -   Image recognition and vector similarity-based search run tens of thousands of times faster on AliPG than on the PostgreSQL Community edition. For more information, see [Image recognition, face recognition, similarity-based retrieval, and similarity-based audience spotting](/intl.en-US/RDS PostgreSQL Database/Application Solutions/Image recognition, face recognition, similarity-based retrieval, and similarity-based audience spotting.md).
    -   Real-time marketing and user profiling run thousands of times faster on AliPG than on the PostgreSQL Community edition. For more information, see [Real-time precision marketing \(user selection\)](/intl.en-US/RDS PostgreSQL Database/Application Solutions/Real-time precision marketing (user selection).md).
    -   The GIS-based Mod operator processes mobile objects 50 times faster than the Mod operator that runs based on the open source PostGIS. For more information, see [Overview](/intl.en-US/Spatio-temporal Database/Overview.md).
-   More stable

    AliPG uses the Platform as a Service \(PaaS\) architecture. This architecture allows you to transform traditional software from license-based service to subscription-based service. You can manage a large amount of metadata, optimize connections, and better isolate resources. You can also use tens of thousands of schemas per RDS instance.

-   More secure
    -   AliPG is certified based on leading national and international security standards, which empowers enterprises to increase institutional security scores in the financing and listing phases.
    -   AliPG provides the following security enhancements:
        -   Encrypts sensitive data that contains passwords. The sensitive data includes dynamic views, shared memory, the dblink plug-in, historical commands, and audit logs.
        -   Fixes bugs in the functions that you call in the PostgreSQL Community edition.
        -   Supports fully encrypted databases. For more information, see [Create a fully encrypted database on an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Data security/Create a fully encrypted database on an ApsaraDB RDS for PostgreSQL instance.md).
        -   Supports the semi-synchronous mode. This mode allows you to configure the following protection levels for your RDS instance: maximum protection, maximum availability, and maximum performance. For more information, see [Set the protection level of an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Instance/Set the protection level of an ApsaraDB RDS for PostgreSQL instance.md).
        -   Supports the failover slot function. This function prevents primary/secondary switchovers from affecting the reliability of logical replication. For more information, see [Failover slot](/intl.en-US/Proprietary AliPG/Failover slot.md).
-   More flexible and controllable \(For more information, see [What is ApsaraDB for MyBase?]()\)
    -   AliPG grants you the permissions to manage the operating systems on hosts in dedicated ApsaraDB MyBase for PostgreSQL clusters. This allows you to manage your dedicated ApsaraDB MyBase for PostgreSQL clusters based on your business requirements.
    -   AliPG allows you to customize overcommit ratios in the development, test, and staging environments. For example, you can configure 128 CPU cores for a host that provides only 64 CPU cores. This allows you to exclusively occupy resources in the production system to reduce the overall costs.

