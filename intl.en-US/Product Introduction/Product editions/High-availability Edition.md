# High-availability Edition

ApsaraDB for RDS offers four editions: Basic Edition, High-availability Edition, Cluster Edition, and Enterprise Edition. This topic describes the High-availability Edition.

The High-availability Edition is a popular edition that allows for one primary instance and one secondary instance. The primary and secondary instances work in the high-availability architecture. This edition is suitable for more than 80% of the actual business scenarios. These scenarios include the Internet, Internet of Things \(IoT\), online retail, logistics, and gaming.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3637688951/p54376.png)

## Topology

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3637688951/p53963.png)

## Benefits

High availability

In the High-availability Edition, the primary instance synchronizes data to the secondary instance in semi-synchronous mode. If the primary instance becomes faulty, your database system automatically fails over to the secondary instance.

You can deploy the primary and secondary instances in the same zone or in different zones.

**Note:** If the secondary instance becomes faulty, the primary instance backs up data on itself in real time. When a backup is about to be completed, a FLUSH TABLE WITH READ LOCK \(FTWRL\) statement is executed. This triggers a global lock that will be held for up to 5 seconds. You can only read data from the primary instance when the global lock is held.

Comprehensive functionality

The High-availability Edition supports all of the features that are provided by ApsaraDB for RDS. These features include automatic scaling, backup and restoration, performance optimization, read/write splitting, and SQL Explorer. The SQL Explorer feature is used to log all of the executed SQL statements. Therefore, you can trace database access and ensure the security of important data.

## Limits

To ensure optimal performance, you must deploy the primary and secondary instances in the same region.

## Upgrade to High-availability Edition

In the Basic Edition, the primary instance does not have a secondary instance as its hot backup. If the primary instance is going through changes such as faults, specification changes, and version upgrades, it may remain unavailable for a long period of time. If you have high requirements for service availability, we recommend that you select the High-availability Edition.

You can create an RDS instance that is designed to run the High-availability Edition. Alternatively, you can upgrade the edition of a created RDS instance from Basic to High-availability. After the upgrade, the new RDS instance inherits the lifecycle of the original RDS instance. Therefore, you do not need to migrate data or reclaim the original RDS instance.

**Note:**

-   If an RDS instance runs MySQL 5.7, you can upgrade its edition from Basic to High-availability by changing the instance specifications. For more information, see [Change the specifications of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md).
-   If an RDS instance runs SQL Server, you can upgrade its edition from Basic to High-availability in the ApsaraDB for RDS console. For more information, see [Upgrade from Basic Edition to High-availability Edition](/intl.en-US/RDS SQL Server Database/Version upgrade/Upgrade from Basic Edition to High-availability Edition.md).

## Create an RDS instance

For more information about how to create an RDS instance that runs the High-availability Edition, see the following topics:

-   [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)
-   [Create an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)
-   [Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md)
-   [Create an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Quick start/Create an ApsaraDB RDS for PPAS instance.md)
-   [Creates an ApsaraDB RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Quick start/Creates an ApsaraDB RDS for MariaDB instance.md)

## FAQ

-   Can I access a secondary RDS instance?

    No, you cannot access a secondary RDS instance. You can only access a primary RDS instance. A secondary RDS instance serves only as a backup and does not allow external access.

-   Can I downgrade the edition of an RDS instance from High-availability to Basic?

    No, you cannot downgrade the edition of an RDS instance from High-availability to Basic. You can create an RDS instance that runs the Basic Edition, migrate the data of your RDS instance to the new RDS instance, and then release your RDS instance. For more information, see [Migrate data between RDS instances](/intl.en-US/Data Migration/Migrate data between instances under the same Alibaba Cloud account/Migrate data between RDS instances.md).


