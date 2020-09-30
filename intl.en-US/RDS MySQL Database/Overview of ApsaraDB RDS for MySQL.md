# Overview of ApsaraDB RDS for MySQL

This topic provides an overview of ApsaraDB RDS for MySQL and describes the related terms.

ApsaraDB for RDS is a stable, reliable, and scalable online database service. It is designed based on the Apsara Distributed File System and high-performance SSD storage media of Alibaba Cloud. It supports five database engines: MySQL, SQL Server, PostgreSQL, PPAS \(compatible with Oracle\), and MariaDB. It also provides a complete suite of solutions for various scenarios, such as disaster recovery, backup, restoration, monitoring, and migration. These solutions facilitate database operation and maintenance \(O&M\). For more information about the benefits of ApsaraDB for RDS, see [A new version is available.](/intl.en-US/Product Introduction/Why choose ApsaraDB for RDS/Competitive advantages of ApsaraDB for RDS instances over user-created databases.md).

If you require technical support, log on to [the ApsaraDB for RDS console](https://rds.console.aliyun.com/) and in the top navigation bar choose **Tickets** \> **Submit Ticket**. If your workloads are complex, you can purchase a support plan on [the Alibaba Cloud After-Sales Support page](https://www.alibabacloud.com/support/after-sales). This allows you to seek advice from instant messaging \(IM\) enterprise groups, technical account managers \(TAMs\), and service managers.

For more information about ApsaraDB for RDS, visit [the ApsaraDB RDS for MySQL product page](https://www.alibabacloud.com/product/apsaradb-for-rds).

## Disclaimer

Some features or functions that are described in this document may be unavailable. For more information, see the specific terms and conditions in your commercial contract. This document serves as a user guide that is for reference only. No content in this document can constitute any expressed or implied warranty.

## ApsaraDB RDS for MySQL

ApsaraDB RDS for MySQL is developed based on a branch of the MySQL source code. Its excellent performance has been proven over years of Double 11, during which it needs to handle large volumes of concurrent traffic. ApsaraDB RDS for MySQL provides basic features, such as instance management, account management, database management, backup and restoration, control access, Transparent Data Encryption \(TDE\), and data migration. ApsaraDB RDS for MySQL also provides the following advanced features and functions:

-   ApsaraDB for MyBase dedicated clusters: An ApsaraDB for MyBase dedicated cluster consists of multiple hosts, such as ECS instances of the ecs.i2.xlarge instance type and ECS Bare Metal instances. You can run instances on these hosts. For more information, see [What is ApsaraDB for MyBase?]()
-   Read-only RDS instances: If the primary RDS instance is overwhelmed by a large number of read requests, your workloads may be interrupted. In this case, you can create one or more read-only RDS instances to offload read requests from the primary RDS instance. For more information, see [Overview of ApsaraDB RDS for MySQL read-only instances](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md). This scales up the read capability of your database system and increases the throughput of your application.
-   Read/write splitting: The read/write splitting function provides a read/write splitting endpoint. This endpoint connects to the primary RDS instance and all of the read-only RDS instances to establish an automatic read/write splitting link. For more information, see [Read/write splitting](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Read/write splitting.md). Your application can read and write data into your database system after it connects to this endpoint. ApsaraDB for RDS distributes write requests to the primary RDS instance and read requests to the read-only RDS instances based on the specified read weights. You can create more read-only RDS instances to scale up the read capability of your database system. In addition, you do not need to modify your application.
-   Dedicated proxy: A dedicated proxy uses dedicated computing resources. It provides more advanced functions, such as read/write splitting, short-lived connection optimization, and transaction splitting. For more information, see [Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md).
-   Database Autonomy Service \(DAS\): DAS supports intelligent diagnostics and optimization at the instance level based on various metrics. These metrics include SQL execution performance, CPU utilization, input/output operations per second \(IOPS\) utilization, memory usage, disk usage, number of connections, locks, and hotspot tables. For more information, see [DAS overview](/intl.en-US/RDS MySQL Database/Performance optimization and diagnosis (autonomy service)/DAS overview.md). DAS allows you to identify existing and potential issues that may compromise the health of your database system. In addition, DAS provides details and solutions for the identified issues. This facilitates database maintenance.

ApsaraDB RDS for MySQL supports only two storage engines: InnoDB and [X-Engine](/intl.en-US/AliSQL Kernel/X-Engine/X-Engine overview.md). For more information, see [Features of ApsaraDB RDS for MySQL](/intl.en-US/RDS MySQL Database/Features of ApsaraDB RDS for MySQL.md).

## Basic terms

-   Instance: An RDS instance is a database process that consumes independent physical memory resources. You can specify a specific memory size, disk capacity, and database type for an RDS instance. The performance of an RDS instance varies based on the specified memory size. After an RDS instance is created, you can change its specifications or delete the instance.
-   Database: A database is a logical unit that is created on an RDS instance. One RDS instance can have multiple databases. Each database must have a unique name on the RDS instance where it is created.
-   Region and zone: Each region is a physical data center. Each region contains a number of isolated locations that are known as zones. Each zone has an independent power supply and network. For more information, visit [the Alibaba Cloud's Global Infrastructure page](https://www.alibabacloud.com/global-locations).

## General terms

|Term|Description|
|----|-----------|
|On-premises database|A database that is deployed in an on-premises data center or a database that is not deployed on an ApsaraDB for RDS instance.|
|ApsaraDB RDS for XX \(XX represents one of the following database engines: MySQL, SQL Server, PostgreSQL, PPAS, and MariaDB.\)|ApsaraDB for RDS with a specific database engine. For example, ApsaraDB RDS for MySQL indicates an ApsaraDB for RDS instance that runs MySQL.|

