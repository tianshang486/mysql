# What is ApsaraDB for RDS {#concept_pc2_lv5_tdb .concept}

ApsaraDB for RDS \(Relational Database Service\) is a stable, reliable, and scalable online database service. Based on a distributed file system designed by Alibaba Cloud and incorporated with high-performance SSDs, RDS supports MySQL, SQL Server, PostgreSQL, Postgre Plus Advanced Server \(PPAS\), and MariaDB engines. It provides a complete solution that includes backup, recovery, monitoring, migration, and more, and allows you to focus more on services rather than database O&M.

## Learning Path {#section_nnr_y4j_b2b .section}

Use [RDS Learning Path](https://www.alibabacloud.com/getting-started/learningpath/rds) to learn about concepts and operations of RDS.

## Related concepts {#section_gbt_pd1_42b .section}

To better familiarize yourself with RDS, the following describes common terms used in RDS:

-   Instance: Avirtualized database server. You can create one or more databases in an RDS instance.
-   Region: A physical data center. Generally, we recommend that your RDS and ECS instances are located in the same region so that ECS can access RDS at fasternetwork speeds.
-   Zone: A physical area that has an independent power supply and networks. A region consists of one or more zones.
-   Database engine: Database engines supported by RDS are MySQL, SQL Server, PostgreSQL, PPAS \(Postgre Plus Advanced Server, highly compatible with Oracle\) and MariaDB. For more information, see [Database engines](../../../../intl.en-US/User Guide/Quick start.md).
-   Network type: Alibaba Cloud supports two network types: classic network and virtual private cloud \(VPC\).
-   Product series: ApsaraDB for RDS includes Basic Edition, High-Availability Edition, and Cluster \(AlwaysOn\) Edition. For more information, see [Product series overview](intl.en-US/Product Introduction/Product series/Product series overview.md).
-   Instance type family: ApsaraDB for RDS supports common instance, dedicated instance, or dedicated-host instance types. For more information, see [Instance type overview](intl.en-US/Product Introduction/Instance types/Instance type overview.md).
-   Storage type: ApsaraDB for RDS supports local SSDs or cloud SSDs. For more information, see [Storage types](intl.en-US/Product Introduction/Storage types.md).

## Related services {#section_r45_z21_42b .section}

-   [ECS](../../../../intl.en-US/Product Introduction/What is ECS?.md): Elastic Compute Service \(ECS\) is a cloud-based server. An ECS instance can access an RDS instance at the fastest speed if the ECS instance accesses the RDS instance through the intranet. Using both ECS and RDS is a typical service model.
-   [Redis](../../../../intl.en-US/Product Introduction/What is ApsaraDB for Redis.md): Redis is a persistent in-memory database service. If the service volume is large, using ECS, RDS, and Redis can handle more read requests and reduce the response time.
-   [MongoDB](https://www.alibabacloud.com/help/doc-detail/26558.htm): MongoDB is a stable, reliable, and scalable database service that is compatible with the MongoDB protocol. If your business involves different types of data structure, you can store structured data in RDS and unstructured data in MongoDB.
-   [MaxCompute](../../../../intl.en-US/Product Introduction/What is MaxCompute?.md): MaxCompute \(previously known as ODPS\) is a general-purpose, fully managed, multi-tenant data processing platform for large-scale data warehousing. MaxCompute supports various data importing solutions and distributed computing models, allowing you to effectively query massive datasets, reduce production costs, and ensure data security. You can use the Data Integration service to import RDS data to MaxCompute for large-scale data processing.
-   [DTS](https://www.alibabacloud.com/help/doc-detail/26592.html): You can use Data Transmission Service \(DTS\) to migrate on-premises database to RDS or implement remote disaster recovery of RDS.
-   [OSS](../../../../intl.en-US/Product Introduction/What is OSS?.md): Object Storage Service \(OSS\) is an encrypted, secure, cost-effective, and easy-to-use object storage service that enables you to store, back up, and archive large amounts of data in the cloud.

## How to use RDS {#section_rgz_gg1_42b .section}

You can create RDS instances, configure the network, create databases, create accounts, and more by using the web console, CLI, SDK, or API, depending on your actual scenario.

-   [Web console](https://rdsnext.console.aliyun.com): RDS provides a graphical web console where you can perform operations easily.
-   CLI: All operations available on the web console can be performed through the CLI.
-   [SDK](../../../../intl.en-US/SDK Reference/SDK reference.md#): All operations available on the web console can be performed through the SDK.
-   [API](../../../../intl.en-US/API Reference/API overview.md#): All operations available on the web console can be performed through APIs.

After you create an RDS instance, you can access it through any common client, such as MySQL-Front, SSMS \(SQL Server Management Studio\), or pgAdmin.

## RDS pricing {#section_kzx_jg1_42b .section}

See [Billing items and billing methods](../../../../intl.en-US/Purchase Guide/Billing items and billing methods.md).

