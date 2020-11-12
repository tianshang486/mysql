# Purchase guide

This topic describes how to select the configuration for an ApsaraDB RDS instance based on your business requirements when you create the instance.

## Purchase consultation

If you want to consult more about the selection of RDS instance configuration, scan the following Quick Response \(QR\) code by using your DingTalk. After you join the chat group, you can obtain professional advice from experts.

![QR code for purchase consultation](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4765415061/p171216.png)

## Introduction to RDS editions, storage types, instance families, and storage engines

Before you create an RDS instance, you must select the most cost-effective, stable configuration based on factors such as performance, prices, and workload. The RDS edition, storage type, and instance family that you select affect one another. For more information, see [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md).

**Note:** If the RDS instance runs MySQL 8.0, you must also select a default storage engine.

-   RDS editions

    ApsaraDB RDS offers four editions: Basic Edition, High-availability Edition, Cluster Edition, and Enterprise Edition. The following figure and table provide more details.

    |RDS edition|Description|Application scenario|
    |-----------|-----------|--------------------|
    |Basic Edition|Your database system consists of only one primary instance, and computing is separated from storage. This edition is cost-effective. For more information, see [Basic Edition](/intl.en-US/Product Introduction/Product editions/Basic Edition.md).

|    -   Personal learning
    -   Small-sized websites
    -   Development and test environments for small- and medium-sized enterprises |
    |High-availability Edition|Your database system consists of one primary instance and one secondary instance. These instances work in the high-availability architecture. This edition is suitable for more than 80% of the actual business scenarios.|    -   Production databases for large- and medium-sized enterprises
    -   Databases in industries such as the Internet, Internet of Things \(IoT\), online retail, logistics, and gaming |
    |Cluster Edition|Your database system consists of one primary instance, one secondary instance, and up to seven read-only instances that are used to increase the read capability. This edition is developed based on the AlwaysOn technology. It is supported only for SQL Server. By default, if you select the Cluster Edition, your database system consists of only one primary instance and one secondary instance. You must create read-only instances later based on your business requirements. For more information, see [ApsaraDB for RDS Cluster Edition](/intl.en-US/Product Introduction/Product editions/Cluster Edition.md).

|Production databases for large- and medium-sized enterprises, such as online retailers, automobile companies, and ERP providers|
    |Enterprise Edition|Your database system consists of one primary instance and two secondary instances. Data is synchronously replicated from the primary instance to the secondary instances. This allows you to ensure data consistency and finance-grade reliability. For more information, see [ApsaraDB for RDS Enterprise Edition](/intl.en-US/Product Introduction/Product editions/Enterprise Edition.md).

|    -   Important databases in the finance, securities, and insurance industries that require high data security
    -   Important production databases for large-sized enterprises |

-   Storage types

    ApsaraDB RDS provides three storage types: local SSD, enhanced SSD, and standard SSD. All of these storage types meet the reliability, persistence, and read/write performance requirements that are specified in Alibaba Cloud service level agreement \(SLA\). The following list describes these storage types:

    -   Local SSD

        This is a recommended storage type. A local SSD resides on the same server as the database engine. You can store data on local SSDs to reduce I/O latency.

    -   Standard SSD

        A standard SSD is an elastic block storage device that is designed based on a distributed storage architecture. You can store data on standard SSDs to separate computing from storage.

    -   Enhanced SSD

        This is also a recommended storage type. This new SSD product is designed by Alibaba Cloud based on the next-generation distributed block storage architecture. It integrates 25 Gigabit Ethernet and remote direct memory access \(RDMA\) technologies to provide super high performance at low latency. An enhanced SSD can process up to 1 million random read/write requests per second. Supported enhanced SSDs come in the following three performance levels \(PLs\):

        -   PL1: An enhanced SSD of PL1 is a regular enhanced SSD.
        -   PL2: An enhanced SSD of PL2 delivers input/output operations per second \(IOPS\) and throughput that are twice as high as those delivered by an enhanced SSD of PL1.
        -   PL3: An enhanced SSD of PL3 delivers IOPS that is 20 times as high as the IOPS delivered by an enhanced SSD of PL1. It also delivers throughput that is 11 times as high as the throughput delivered by an enhanced SSD of PL1. Enhanced SSDs of PL3 are ideal for workloads that require high I/O performance in processing concurrent requests and stable read/write latency.
        For more information about PLs, see [Block Storage performance](https://www.alibabacloud.com/help/zh/doc-detail/25382.htm).

-   Instance families

    ApsaraDB RDS offers a wide range of instance families based on the number of CPU cores, memory capacity, number of connections, and input/output operations per second \(IOPS\). Each instance family includes multiple instance types. The following figure and table provide more details.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8244029951/p1370.png)

    |Instance family|Description|Scenario|
    |---------------|-----------|--------|
    |Shared instance family \(Not supported\)

|    -   A shared instance exclusively occupies the memory resources allocated to it, but shares CPU and storage resources with the other shared instances that are deployed on the same server.
    -   CPU resources are highly reused among shared instances that are deployed on the same server. This maximizes cost effectiveness.
    -   Shared instances may compete for resources.
|    -   Business that requires low costs.
    -   Business that requires high availability but is not demanding for stability. |
    |General-purpose instance family|    -   A general-purpose instance exclusively occupies the memory resources allocated to it, but shares CPU and storage resources with the other general-purpose instances that are deployed on the same server.
    -   CPU resources are moderately reused among general-purpose instances that are deployed on the same server. This increases cost effectiveness.
    -   The storage capacity of a general-purpose instance is independent of the number of CPU cores and memory capacity. You can flexibly configure the storage capacity based on your business requirements.
|Business that is not demanding on performance and stability.|
    |Dedicated instance family|A dedicated instance exclusively occupies the CPU and memory resources allocated to it. Its performance remains stable and is not affected by other instances that are deployed on the same server. The top configuration of this instance family is dedicated host. A dedicated host instance occupies all resources on the server where it is deployed.

|Business that uses databases as the core system, such as finance, e-commerce, government affairs, and large- and medium-sized Internet services.|

-   Storage engines

    If the RDS instance runs MySQL 8.0, you can select one of the following two storage engines:

    -   InnoDB: the default storage engine that is provided by open source MySQL. The InnoDB storage engine used for ApsaraDB RDS has been reinforced by Alibaba Cloud.
    -   X-Engine: the storage engine that is developed by Alibaba Cloud. X-Engine is compatible with InnoDB. X-Engine performs better than InnoDB in terms of disk space usage and cost-effectiveness. Therefore, X-Engine is more suitable for scenarios such as data archiving than InnoDB. For more information, see [X-Engine overview](/intl.en-US/Proprietary AliSQL/X-Engine/X-Engine overview.md).

## Select configuration for an RDS instance

Perform the following steps to select configuration for an RDS instance:

1.  Select an RDS edition.

    If the RDS instance is used for medium- and large-sized enterprises or for industries such as Internet, Internet of Things \(IoT\), online retail, logistics, and gaming, we recommend that you select the High-availability Edition. This edition adopts the high-availability architecture that consists of one primary instance and one secondary instance.

    If the RDS instance is used for crucial databases in large-sized enterprises or for financial, securities, and insurance industries that require high data security, we recommend that you select the Enterprise Edition \(MySQL\) or the Cluster Edition \(SQL Server\).

    ![Select an RDS edition](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2537688951/p102669.png)

2.  Select a storage type.

    We recommend that you select a local SSD or an enhanced SSD of a suitable performance level \(PL\) based on the IOPS and throughput requirements of your business. For more information about the differences between local SSDs and standard or enhanced SSDs, see [Features](/intl.en-US/Product Introduction/Features.md).

    The maximum IOPS of a standard or enhanced SSD varies based on the instance type and the storage capacity. The following table lists the formulas that are used to calculate the maximum IOPS of a standard or enhanced SSD.

    |Storage type|ESSD|Standard SSD|
|Performance level|PL3|PL2|PL1|-|
    |------------|----|------------|
    |-----------------|---|---|---|--|
    |Maximum IOPS

\(The storage capacity is measured in GB.\)

|min\{1800 + 50 × Storage capacity, 1000000\}|min\{1800 + 50 × Storage capacity, 100000\}|min\{1800 + 50 × Storage capacity, 50000\}|min\{1800 + 30 × Storage capacity, 25000\}|

    ![Select a storage type](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2537688951/p102670.png)

3.  Select an instance type.

    The specifications of an RDS instance type include the number of CPU cores, memory capacity, maximum number of connections, and maximum IOPS. When you create an RDS instance, you must select an instance level: entry level or enterprise level. Then, you can select an instance type based on your business requirements. The entry level provides the shared and general-purpose instance families, and the enterprise level provides the dedicated instance family.

    ![Select an instance type](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3537688951/p102671.png)

    **Note:** If you select the standard or enhanced SSD storage type, the IOPS becomes **N/A** in the ApsaraDB RDS console. This is because ApsaraDB RDS must calculate the IOPS based on the selected storage type. For more information, see [Select a storage type](#li_px0_mvq_wd1) in this section.

4.  Select a storage engine.

    If the RDS instance runs MySQL, we recommend that you select X-Engine as the storage engine. X-Engine costs about 50% less than InnoDB but delivers comparable performance. For more information, see [Usage notes](/intl.en-US/Proprietary AliSQL/X-Engine/Usage notes.md).


## Check and modify the configuration of an RDS instance

After you select configuration for an RDS instance, we recommend that you continue to monitor the performance of the RDS instance for a specific period of time. This allows you to check whether the configuration of the RDS instance is suitable.

For example, if you find that the memory usage is high, we recommend that you log on to the RDS instance to troubleshoot the issue. If no exceptions occur, you can modify the configuration of the RDS instance. If exceptions occur, you can modify the allocation of memory capacity on the RDS instance. For more information, see the following topics:

-   [View the resource and engine metrics of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for MySQL instance.md)
-   [Configure an alert rule for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for MySQL instance.md)
-   [Change the specifications of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md)

## Create an RDS instance

For more information about how to create an RDS instance, see the following topics:

-   [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)
-   [Create an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)
-   [Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md)
-   [Create an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Quick start/Create an ApsaraDB RDS for PPAS instance.md)
-   [Creates an ApsaraDB RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Quick start/Creates an ApsaraDB RDS for MariaDB instance.md)

## References

-   [Price calculator](https://www.aliyun.com/pricing-calculator?spm=5176.8064714.321464.pricing_version_2.64a85fb0ctJ33N#/add/3884821/rds/rds)
-   [Test results of ApsaraDB RDS for MySQL 8.0](/intl.en-US/Performance White Paper/RDS for MySQL/Test results of ApsaraDB RDS for MySQL 8.0.md)
-   [Test results of ApsaraDB RDS for MySQL 5.7](/intl.en-US/Performance White Paper/RDS for MySQL/Test results of ApsaraDB RDS for MySQL 5.7.md)
-   [Test results of ApsaraDB RDS for MySQL 5.6](/intl.en-US/Performance White Paper/RDS for MySQL/Test results of ApsaraDB RDS for MySQL 5.6.md)
-   [Test result](/intl.en-US/Performance White Paper/RDS for PostgreSQL/Test result.md)

