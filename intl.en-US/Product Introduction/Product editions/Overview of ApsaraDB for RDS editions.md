# Overview of ApsaraDB for RDS editions

ApsaraDB for RDS offers four editions: Basic Edition, High-availability Edition, Cluster Edition, and Enterprise Edition. This topic describes how to view the edition of an ApsaraDB for RDS instance and provides a comparison between various editions.

For more information about the instance families that are supported by each edition, see [Instance families](/intl.en-US/Product Introduction/Product specifications/Instance families.md).

## View the edition of an RDS instance

Log on to the ApsaraDB for RDS console, find the RDS instance, and navigate to the Basic Information page. Then, you can view the edition of the RDS instance.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8649259951/p54372.png)

## Comparison between various editions

|RDS edition|Description|Application scenario|
|-----------|-----------|--------------------|
|Basic Edition|Your database system consists of only one primary instance, and computing is separated from storage. This edition is cost-effective. For more information, see [Basic Edition](/intl.en-US/Product Introduction/Product editions/Basic Edition.md).

|-   Personal learning
-   Small-sized websites
-   Development and test environments for small- and medium-sized enterprises |
|High-availability Edition|Your database system consists of one primary instance and one secondary instance. These instances work in the high-availability architecture. This edition is suitable for more than 80% of the actual business scenarios.|-   Production databases for large- and medium-sized enterprises
-   Databases in industries such as the Internet, Internet of Things \(IoT\), online retail, logistics, and gaming |
|Cluster Edition|Your database system consists of one primary instance, one secondary instance, and up to seven read-only instances that are used to increase the read capability. This edition is developed based on the AlwaysOn technology. It is supported only for SQL Server. By default, if you select the Cluster Edition, your database system consists of only one primary instance and one secondary instance. You must create read-only instances later based on your business requirements. For more information, see [ApsaraDB for RDS Cluster Edition](/intl.en-US/Product Introduction/Product editions/Cluster Edition.md).

|Production databases for large- and medium-sized enterprises, such as online retailers, automobile companies, and ERP providers|
|Enterprise Edition|Your database system consists of one primary instance and two secondary instances. Data is synchronously replicated from the primary instance to the secondary instances. This allows you to ensure data consistency and finance-grade reliability. For more information, see [ApsaraDB for RDS Enterprise Edition](/intl.en-US/Product Introduction/Product editions/Enterprise Edition.md).

|-   Important databases in the finance, securities, and insurance industries that require high data security
-   Important production databases for large-sized enterprises |

## Features supported by various editions

For more information, see [Features](/intl.en-US/Product Introduction/Features.md).

## Create an RDS instance

For more information about how to create an RDS instance, see the following topics:

-   [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)
-   [Create an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)
-   [Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md)
-   [Create an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Quick start/Create an ApsaraDB RDS for PPAS instance.md)
-   [Creates an ApsaraDB RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Quick start/Creates an ApsaraDB RDS for MariaDB instance.md)

