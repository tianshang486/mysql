# Basic Edition

ApsaraDB for RDS offers four editions: Basic Edition, High-availability Edition, Cluster Edition, and Enterprise Edition. This topic describes the Basic Edition.

In the Basic Edition, your database system consists of only one primary instance, and computing is separated from storage. This edition is cost-effective.

**Note:** In the Basic Edition, the primary instance does not have a secondary instance as its hot backup. If the primary instance breaks down unexpectedly, is executing specification changes, or is upgrading its version, your database service may be unavailable for a long period of time. If you have high requirements for service availability, we recommend that you select the High-availability, Cluster, or Enterprise Edition. Alternatively, you can upgrade the edition of your RDS instance from Basic to High-availability. For more information, see [Upgrade to High-availability Edition](#section_5sr_8hd_e8j).

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8649259951/p54372.png)

The following figure shows a comparison between the Basic Edition and the High-availability Edition.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3637688951/p1359.png)

## Benefits

Performance

The primary instance does not need to replicate data to a secondary instance. Therefore, no extra performance overheads are incurred. This makes the Basic Edition perform better than the High-availability Edition and the Enterprise Edition when the same instance configuration is used.

Reliability

-   Computing is separated from storage. This prevents data losses in the event of failures on compute nodes.

    **Note:** If you set the **Backup Frequency** parameter to **Every 30 Minutes**, you can restore data to a point in time within the last 30 minutes in the event of SSD damages or other unexpected failures. This applies only when you are using SQL Server with the Basic Edition. For more information, see [Back up an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance.md).

    ![Compute-storage separation](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3637688951/p46129.png)

-   The ultra-large Apsara distributed storage system of Alibaba Cloud is used to store multiple data copies that help ensure reliability.

Cost-effectiveness

Only one primary instance is deployed. This reduces your overall costs by 50% compared with the High-availability Edition.

## Features

The Basic Edition supports basic features, such as IP address whitelist, monitoring and alerting, and backup and restoration. The Basic Edition does not support the following features:

-   [Primary/secondary switchover]()
-   [Cross-zone migration]()
-   [Log management]()
-   [Read-only instance](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md)

For more information about the features that are supported by the Basic Edition, see [Overview of ApsaraDB for RDS editions](/intl.en-US/Product Introduction/Product editions/Overview of ApsaraDB for RDS editions.md).

## Scenarios

-   Small-sized websites and applications

    The Basic Edition is cost-effective and relieves the need for database operation and maintenance \(O&M\). You can focus only on your business development.

-   Personal learning

    If you are new to databases, you can use the Basic Edition for testing and learning.

-   Research and development \(R&D\)

    The Basic Edition allows you to create and release RDS instances anytime and anywhere. This significantly improves R&D efficiency.


## Create an RDS instance

For more information about how to create an RDS instance that runs the Basic Edition, see the following topics:

-   [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)
-   [Create an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md#)
-   [Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md#)

## Get started with the Basic Edition

The Basic Edition is supported for MySQL, SQL Server, and PostgreSQL. For more information about how to create and connect to an RDS instance that runs the Basic Edition, see the following topics:

-   [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)
-   [Create an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)
-   [Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md)

## Upgrade to High-availability Edition

-   If your RDS instance runs MySQL 5.7, you can upgrade its edition from Basic to High-availability by changing the instance specifications. For more information, see [Change the specifications of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md).
-   If your RDS instance runs SQL Server, you can upgrade its edition from Basic to High-availability in the ApsaraDB for RDS console. For more information, see [Upgrade from Basic Edition to High-availability Edition](/intl.en-US/RDS SQL Server Database/Version upgrade/Upgrade from Basic Edition to High-availability Edition.md).

## FAQ

-   Why does it take a long time to upgrade the Basic Edition or change the specifications of my RDS instance?

    In the Basic Edition, your database system consists of only one primary instance. When you upgrade the Basic Edition or change the specifications, your database system checks whether the physical server that hosts the primary instance provides sufficient resources. If the physical server does not provide sufficient resources, your database system replicates data to another suitable physical server and switches your database service to that physical server. This process takes a long time. In extreme circumstances, your database service may be unavailable for more than 30 minutes. We recommend that you select the High-availability Edition, Enterprise Edition, or Cluster Edition. These editions use the high-availability architecture, which allows you to replicate data from a secondary instance without causing interruptions to your database service. For more information, see [High-availability Edition](/intl.en-US/Product Introduction/Product editions/High-availability Edition.md), [Enterprise Edition](/intl.en-US/Product Introduction/Product editions/Enterprise Edition.md), and [Cluster Edition](/intl.en-US/Product Introduction/Product editions/Cluster Edition.md).

-   Why does the Basic Edition provide only a small number of features? And which features are supported by the Basic Edition?

    The Basic Edition provides only one primary instance. Therefore, features that are supported by the High-availability Edition, Cluster Edition, and Enterprise Edition are unavailable in the Basic Edition. The Basic Edition is suitable only in a small number of business scenarios. For more information about the features that are supported by the Basic Edition, see the following topics:

    -   [Features of ApsaraDB RDS for MySQL](/intl.en-US/RDS MySQL Database/Features of ApsaraDB RDS for MySQL.md)
    -   [Features of ApsaraDB RDS for SQL Server](/intl.en-US/RDS SQL Server Database/Features of ApsaraDB RDS for SQL Server.md)
    -   [Features of ApsaraDB RDS for PostgreSQL](/intl.en-US/RDS PostgreSQL Database/Features of ApsaraDB RDS for PostgreSQL.md)
    **Note:** The Basic Edition is not supported for PPAS or MariaDB.


