# Preface

This white paper provides guidelines for you to optimize the performance of your ApsaraDB RDS instance from various dimensions. These dimensions include instance configuration selection, parameter reconfiguration, and monitoring and alerting.

ApsaraDB RDS for MySQL uses AliSQL. AliSQL is an independent MySQL branch that is developed by Alibaba Cloud. AliSQL provides all features of the MySQL Community edition and a number of advanced features that are similar to the MySQL Enterprise edition. These advanced features include enterprise-grade backup and restoration, thread pool, and parallel query. For more information about AliSQL, see [Features of AliSQL](/intl.en-US/Proprietary AliSQL/Overview of AliSQL features.md).

To improve performance, ApsaraDB RDS for MySQL provides the fast query cache, Binlog in Redo, and statement queue features. You can use these features with [Alibaba Cloud Database Autonomy Service \(DAS\)]() to implement automated perception, recovery, optimization, operations and maintenance \(O&M\), and security protection. For more information about these features, see [A new version is available.](/intl.en-US/Proprietary AliSQL/Performance/Fast query cache.md), [Binlog in Redo](/intl.en-US/Proprietary AliSQL/Performance/Binlog in Redo.md), and [Statement Queue](/intl.en-US/Proprietary AliSQL/Performance/Statement Queue.md).

## Factors that affect database performance

Database performance is affected by the following factors:

-   SQL query speed
-   Networking
-   Disk I/O
-   Hardware specifications
-   Database engine version
-   Parameter settings

## Methods to optimize database performance

-   Instance configuration selection

    Before you start your workloads, we recommend that you check the configuration of your RDS instance. For more information, see the following topics:

    -   [Select AliSQL]()
    -   [Select instance specifications]()

        **Note:** If your workloads change over time, you can change the configuration of your RDS instance. For more information, see [Change the specifications of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md).

-   DAS

    You can use DAS to manage your RDS instance. For more information, see the following topics:

    -   [t1962003.md\#]()
    -   [t1962004.md\#]()
    -   [t1962007.md\#]()
    -   [t1962008.md\#]()
-   Parameter reconfiguration

    Reconfigure the parameters of your RDS instance. You can use the default high-performance parameter template that is provided by Alibaba Cloud to reconfigure the parameters. This template allows ApsaraDB RDS to replicate data in asynchronous mode. Therefore, this template delivers medium security but the fastest speed. For more information about this template, see [High-performance parameter template]().

-   Monitoring and alerting

    ApsaraDB RDS provides a number of metrics that you can use to monitor the performance of your RDS instance. In addition, ApsaraDB RDS allows you to configure alert rules for these metrics. If the value of a metric meets the specified alert conditions, an alert is triggered. ApsaraDB RDS sends the alert to all the contacts in the associated alert group. For more information, see [Monitoring and alerting]().

-   Read/write splitting

    If the primary RDS instance needs to process a large number of read requests but only a small number of write requests, it may become overwhelmed. This may even interrupt your workloads. In this case, you can create one or more read-only RDS instances to offload read requests from the primary RDS instance. This allows you to scale the read capability of your database system. For more information, see [Overview of ApsaraDB RDS for MySQL read-only instances](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md).

    After you create read-only RDS instances, you can enable the read/write splitting feature. In this case, the endpoint that is generated to connect to the dedicated proxies of your database system is used to implement read/write splitting. After you add this endpoint to your application, write requests are routed to the primary RDS instance and read requests are routed to the read-only RDS instances.

    For more information, see [Read/write splitting](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Read/write splitting.md).

-   Caching

    If your RDS instance runs MySQL, use MySQL with Redis. This way, read requests are routed to the Redis cache instead of directly to your RDS instance. If the required data cannot be found in the Redis cache, the read requests are then routed to your RDS instance. This method increases query response speeds and relieves the pressure on your RDS instance.


## Performance testing

-   [ApsaraDB RDS for MySQL performance overview](/intl.en-US/Performance White Paper/RDS for MySQL/ApsaraDB RDS for MySQL performance overview.md)
-   [Test guidelines](/intl.en-US/Performance White Paper/RDS for MySQL/Test guidelines.md)

