# Overview of ApsaraDB RDS for SQL Server

This topic provides an overview of ApsaraDB RDS for SQL Server and describes the related terms.

ApsaraDB for RDS is a stable, reliable, and scalable online database service. It is designed based on the Apsara Distributed File System and high-performance SSD storage media of Alibaba Cloud. It supports five database engines: MySQL, SQL Server, PostgreSQL, PPAS \(compatible with Oracle\), and MariaDB. It also provides a complete suite of solutions for various scenarios, such as disaster recovery, backup, restoration, monitoring, and migration. These solutions facilitate database operation and maintenance \(O&M\). For more information about the benefits of ApsaraDB for RDS, see [A new version is available.](/intl.en-US/Product Introduction/Why choose ApsaraDB for RDS/Competitive advantages of ApsaraDB for RDS instances over user-created databases.md).

If you require technical support, log on to [the ApsaraDB for RDS console](https://rds.console.aliyun.com/) and in the top navigation bar choose **Tickets** \> **Submit Ticket**. If your workloads are complex, you can purchase a support plan on [the Alibaba Cloud After-Sales Support page](https://www.alibabacloud.com/support/after-sales). This allows you to seek advice from instant messaging \(IM\) enterprise groups, technical account managers \(TAMs\), and service managers.

For more information about ApsaraDB for RDS, visit [the ApsaraDB RDS for MySQL product page](https://www.alibabacloud.com/product/apsaradb-for-rds).

## Disclaimer

Some features or functions that are described in this document may be unavailable. For more information, see the specific terms and conditions in your commercial contract. This document serves as a user guide that is for reference only. No content in this document can constitute any expressed or implied warranty.

## SQL Server

SQL Server supports the high-availability architecture and provides the capability to restore data to a specific point in time. This allows SQL Server to run on various enterprise applications. In addition, SQL Server is provided with a Microsoft-issued license. This relieves the need to purchase a license. ApsaraDB RDS for SQL Server also provides the following advanced features and functions:

-   ApsaraDB for MyBase dedicated clusters: An ApsaraDB for MyBase dedicated cluster consists of multiple hosts, such as ECS instances of the ecs.i2.xlarge instance type and ECS Bare Metal instances. You can run instances on these hosts. For more information, see [What is ApsaraDB for MyBase?]()
-   Disk encryption: This function encrypts the entire data disks of your RDS instance based on block storage. Your data cannot be accessed even if it is leaked. For more information, see [Configure disk encryption for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Data security/Configure disk encryption for an ApsaraDB RDS for SQL Server instance.md). In addition, this function does not interrupt your workloads, and you do not need to modify your application.
-   Read-only RDS instances: If the primary RDS instance is overwhelmed by a large number of read requests, your workloads may be interrupted. In this case, you can create one or more read-only RDS instances to offload read requests from the primary RDS instance. For more information, see [Create a read-only ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Read-only instances/Create a read-only ApsaraDB RDS for SQL Server instance.md). This scales up the read capability of your database system and increases the throughput of your application.
-   Read/write splitting: After read-only RDS instances are created, you can enable the read-only routing endpoint. Then, you can add the endpoint of the primary RDS instance and the read-only routing endpoint to your application. Your database system distributes write requests to the primary RDS instance and read requests to the read-only routing endpoint. The read-only routing endpoint then distributes the read requests to the read-only RDS instances based on the specified read weights. For more information, see [Read/write splitting overview](/intl.en-US/RDS SQL Server Database/Read/write splitting/Read/write splitting overview.md).

For more information about the features that ApsaraDB RDS for SQL Server supports, see [Features of ApsaraDB RDS for SQL Server](/intl.en-US/RDS SQL Server Database/Features of ApsaraDB RDS for SQL Server.md).

## Basic terms

-   Instance: An RDS instance is a database process that consumes independent physical memory resources. You can specify a specific memory size, disk capacity, and database type for an RDS instance. The performance of an RDS instance varies based on the specified memory size. After an RDS instance is created, you can change its specifications or delete the instance.
-   Database: A database is a logical unit that is created on an RDS instance. One RDS instance can have multiple databases. Each database must have a unique name on the RDS instance where it is created.
-   Region and zone: Each region is a physical data center. Each region contains a number of isolated locations that are known as zones. Each zone has an independent power supply and network. For more information, visit [the Alibaba Cloud's Global Infrastructure page](https://www.alibabacloud.com/global-locations).

## General terms

|Term|Description|
|----|-----------|
|On-premises database|A database that is deployed in an on-premises data center or a database that is not deployed on an ApsaraDB for RDS instance.|
|ApsaraDB RDS for XX \(XX represents one of the following database engines: MySQL, SQL Server, PostgreSQL, PPAS, and MariaDB.\)|ApsaraDB for RDS with a specific database engine. For example, ApsaraDB RDS for MySQL indicates an ApsaraDB for RDS instance that runs MySQL.|

