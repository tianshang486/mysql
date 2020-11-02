# Create a read-only ApsaraDB RDS for MySQL instance

This topic describes how to create a read-only RDS instance for your primary ApsaraDB RDS for MySQL instance. Read-only RDS instances allow your database system to process a large number of read requests. This also increases the throughput of your application. Each read-only instance is a replica of the primary instance. Data updates on the primary instance are synchronized to all of the read-only instances.

For more information about how to create a read-only instance in other database engines, see the following topics:

-   [Create a read-only ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Read-only instances/Create a read-only ApsaraDB RDS for SQL Server instance.md)
-   [Create a read-only ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/RDS for PostgreSQL read-only instances/Create a read-only ApsaraDB RDS for PostgreSQL instance.md)
-   [Create an RDS PPAS read-only instance](/intl.en-US/RDS PPAS Database/Quick start/Read-only instances/Create an RDS PPAS read-only instance.md)

For more information about read-only instances, see [Overview of read-only ApsaraDB RDS for MySQL instances](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md).

## Prerequisites

The instance runs one of the following MySQL versions and RDS editions:

-   MySQL 8.0 in the High-availability Edition or Enterprise Edition
-   MySQL 5.7 in the High-availability Edition or Enterprise Edition
-   MySQL 5.6

**Note:** If your instance running MySQL 5.7 in the Enterprise Edition does not support read-only instances, [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

## Precautions

-   You can create read-only RDS instances for the primary RDS instance. However, you cannot convert existing RDS instances to read-only RDS instances.
-   When you create a read-only RDS instance, ApsaraDB RDS replicates data to the read-only instance from a secondary RDS instance. This prevents interruptions to the workloads on the primary RDS instance.
-   A read-only instance does not inherit the parameter settings of the primary instance. ApsaraDB RDS generates default parameter settings for the read-only instance. You can modify the parameter settings in the ApsaraDB RDS console.
-   The maximum number of read-only instances can vary based on the memory capacity.

    |Database engine|Memory capacity|Maximum number of read-only instances|
    |---------------|---------------|-------------------------------------|
    |MySQL|≥ 64 GB|10|
    |< 64 GB|5|

-   A read-only RDS instance supports only the pay-as-you-go billing method. It is charged on an hourly basis based on the instance type at the time of fee deduction. For more information, visit the [ApsaraDB RDS for MySQL pricing page](https://www.alibabacloud.com/product/apsaradb-for-rds?spm=a3c0i.7938564.220486.8.10521d15K8Buqg#pricing).

## Create a read-only RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the Distributed by Instance Role section of the Basic Information page, click **Create Read-only Instance**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1730359951/p9361.png)

5.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Zone**|The zone where the read-only RDS instance resides. Each zone is an independent physical location within a region. Zones in the same region provide the same services. Multi-zone deployment provides zone-level disaster recovery for your workloads.|
    |**Instance Type**|    -   **Entry-level**: belongs to the general-purpose instance family. A general-purpose instance exclusively occupies the allocated memory and I/O resources. However, it shares CPU and storage resources with the other general-purpose instances that are deployed on the same server.
    -   **Enterprise-level**: belongs to the dedicated instance family. A dedicated instance exclusively occupies the allocated CPU, memory, storage, and I/O resources. The top configuration of the dedicated instance family is the dedicated host instance family. A dedicated host instance exclusively occupies all the CPU, memory, storage, and I/O resources of the server where it is deployed.
**Note:** Each instance type supports a specific number of CPU cores, memory capacity, maximum number of connections, and maximum IOPS. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). |
    |**Capacity**|The storage capacity that the RDS instance has available to store data files, system files, binary log files, and transaction files. You can adjust the storage capacity in increments of 5 GB. **Note:** If you select local SSDs, the storage capacity of the RDS instance may vary based on the instance type. If you select standard or enhanced SSDs, this limit does not apply. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). |

6.  Click **Next: Instance Configuration** and configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Network Type**|    -   **Classic Network**: the traditional type of network.
    -   **VPC**: A virtual private cloud \(VPC\) is an isolated network that provides higher security and better performance than the classic network. If you select the VPC network type, you must also specify the **VPC** and the **VSwitch of Primary Node**.
**Note:** The RDS instance must have the same network type as the ECS instance that you want to connect. If the RDS and ECS instances both have the VPC network type, they must also reside in the same VPC. Otherwise, the RDS and ECS instances cannot communicate over an internal network. |

7.  Click **Next: Confirm Order**.

8.  Read and select Terms of Service, click **Pay Now**, and then complete the payment.

    **Note:** If your primary RDS instance supports the database proxy feature, you can select **MySQL Dedicated Proxy Service\(Paid Service\)** in the Confirm Order step when you create the read-only RDS instance. For more information, see [Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md).


## View a read-only RDS instance

To view a read-only RDS instance on the Instances page, perform the following steps:

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the read-only RDS instance and click its ID.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2730359951/p2617.png)


To view a read-only RDS instance on the Basic Information page of its primary instance, perform the following steps:

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the primary RDS instance and click its ID.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2730359951/p32584.png)

4.  On the **Basic Information** page, move the pointer over the number of read-only RDS instances and click the ID of the read-only RDS instance that you want to view.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2730359951/p9379.png)


## View the latency of a read-only RDS instance

When a read-only RDS instance synchronizes data from its primary RDS instance, a specific latency may occur. You can navigate to the Basic Information page of a read-only RDS instance to view the latency of data synchronization to the instance.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2730359951/p2636.png)

## FAQ

-   Can I select subscription billing for read-only RDS instances?

    No, read-only RDS instances support only the pay-as-you-go billing method. This makes it easier for you to change the instance specifications.

-   Why am I unable to select a zone when I create a read-only RDS instance?

    You cannot select a zone because the zone does not have available resources. In this case, select another zone. This does not affect your read-only RDS instance.

-   Can I select a different virtual private cloud \(VPC\) than the primary RDS instance when I create a read-only RDS instance?

    Yes, you can select a different VPC than the primary RDS instance. A VPC is used to isolate external access to an RDS instance, such as access from an ECS instance to an RDS instance. Read-only RDS instances are not subject to this limit.


## Related operations

|Operation|Description|
|---------|-----------|
|[t8102.md\#](/intl.en-US/API Reference/Read-Only Instances/Create read-only instance.md)|Creates a read-only ApsaraDB RDS instance.|

