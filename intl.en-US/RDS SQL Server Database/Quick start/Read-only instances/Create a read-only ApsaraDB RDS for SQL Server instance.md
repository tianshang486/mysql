# Create a read-only ApsaraDB RDS for SQL Server instance

This topic describes how to create a read-only instance for your primary ApsaraDB RDS for SQL server instance. This allows your database system to process a large number of read requests and increases the throughput of your application. Each read-only instance is a replica of the primary instance. The primary instance replicates updates to its data to all of the read-only instances created in it.

For more information about read-only instances, see [Overview of read-only ApsaraDB RDS for SQL Server instances](/intl.en-US/RDS SQL Server Database/Quick start/Read-only instances/Overview of read-only ApsaraDB RDS for SQL Server instances.md).

## Prerequisites

Your primary instance runs SQL Server 2017 on RDS Cluster Edition.

## Precautions

-   You can only create read-only instances for your primary instance. You cannot switch existing instances to read-only instances.
-   While you create a read-only instance, the system replicates data from a secondary instance. Therefore, the operation of your primary instance is not interrupted.
-   You can create up to seven read-only instances.
-   A read-only instance is billed on an hourly basis. The actual fee varies based on the instance type at the time of fee deduction. For more information, see the "Billing" section in [Introduction to SQL Server read-only instances](/intl.en-US/RDS SQL Server Database/Quick start/Read-only instances/Overview of read-only ApsaraDB RDS for SQL Server instances.md).

## Create a read-only instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, select the region where your primary instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your primary instance and click its ID.
4.  In the Distributed by Instance Role section of the Basic Information page, click **Create Read-only Instance**.

    ![添加只读实例](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4761760061/p168763.png)

5.  Configure the following parameters and click **Next:Instance Configuration**.

    |Parameter|Description|
    |---------|-----------|
    |**Storage Type**|    -   **Standard SSD**: A standard SSD is an elastic block storage device that is designed based on the distributed storage architecture. If you use standard SSDs, computing is separated from storage.
    -   **Enhanced SSD \(Recommended\)**: An enhanced SSD is an ultra-high performance disk that is designed by Alibaba Cloud based on next-generation distributed block storage architecture. It integrates 25 Gigabit Ethernet and remote direct memory access \(RDMA\) technologies to reduce latency and deliver up to 1 million random input/output operations per second \(IOPS\). Enhanced SSDs are available in three performance levels \(PLs\):
        -   Enhanced SSD: This is an enhanced SSD of PL1.
        -   Enhanced SSD PL2: An enhanced SSD of PL2 delivers an IOPS and throughput that are twice as high as those delivered by an enhanced SSD of PL1.
        -   Enhanced SSD PL3: An enhanced SSD of PL3 delivers an IOPS that is 20 times as high as the IOPS delivered by an enhanced SSD of PL1. It also delivers throughput that is 11 times as high as the throughput delivered by an enhanced SSD of PL1. Enhanced SSDs of PL3 are ideal for businesses that require high I/O performance in processing concurrent requests and stable read/write latency.
For more information about storage types, see [Storage types](/intl.en-US/Product Introduction/Storage types.md). |
    |**Zone**|Zones are independent physical areas located within a region.|
    |**Instance Type**|    -   **Entry-level**: belongs to the general-purpose instance family. A general-purpose instance exclusively occupies the memory and I/O resources allocated to it, but shares CPU and storage resources with the other general-purpose instances that are deployed on the same server.
    -   **Enterprise-level**: belongs to the dedicated instance family. A dedicated instance exclusively occupies the CPU, memory, storage, and I/O resources allocated to it. The top configuration of the dedicated instance family is the dedicated host. A dedicated host instance occupies all of the CPU, memory, storage, and I/O resources on the server where it resides.
**Note:** Each instance type supports a specific number of CPU cores, memory capacity, maximum number of connections, and maximum IOPS. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). |
    |**Capacity**|The storage capacity that the read-only instance has available to store data files, system files, binary log files, and transaction files. The storage capacity increases in increments of 5 GB. **Note:** The dedicated instance family supports exclusive allocations of resources. Therefore, the storage capacity of each instance type with local SSDs in this family is fixed. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). |

    **Note:** To ensure sufficient I/O throughput for data synchronization, we recommend that read-only instances be allocated at least as much memory as their primary instance.

6.  Configure the following parameters and click **Next:Confirm Order**.

    |Parameter|Description|
    |---------|-----------|
    |**Network Type**|    -   **Classic Network**: a traditional type of network.
    -   **VPC**: A Virtual Private Cloud \(VPC\) is an isolated network with higher security and better performance than the classic network. If you select the VPC network type, you must also specify the **VPC** and the **VSwitch of Primary Node** parameters.
**Note:** The read-only instance must have the same network type as the ECS instance to which you want to connect. If both the read-only and ECS instances have the VPC network type, make sure that they reside in the same VPC. Otherwise, they cannot communicate over an internal network. |
    |**Resource Group**|The resource group to which the read-only instance belongs.|

7.  Click **Next:Confirm Order**, confirm the settings in the **Parameters** section, set **Purchase Plan**, read and select Terms of Service, and click **Pay Now**.

The read-only instance is created in a few minutes.

## View a read-only instance

-   To view a read-only instance on the Instances page, follow these steps:
    1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
    2.  Select the region where the read-only instance resides.

        ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

    3.  Find the read-only instance and click its ID.

        ![Read-only instance](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8949259951/p39852.png)

-   To view a read-only instance on the Basic Information page of its primary instance, follow these steps:
    1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
    2.  Select the region where the primary instance resides.

        ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

    3.  Find the primary instance and click its ID.

        ![Primary instance](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8949259951/p39853.png)

    4.  On the **Basic Information** page, move the pointer over the number of read-only instances and click the ID of the read-only instance that you want to view.

        ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2730359951/p9379.png)


## View a read-only instance on the Cluster management page

Prerequisites

[Read/write splitting]() is enabled on the Cluster management page of the primary instance to which the read-only instance is attached.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9949259951/p32588.png)

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the primary instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the primary instance and click its ID.
4.  In the left-side navigation pane, click **Cluster management**.
5.  Find the read-only instance and click its ID.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8949259951/p32587.png)


## View the latency of a read-only instance

A primary instance replicates data to its read-only instances at a certain latency. You can navigate to the Basic Information page of a read-only instance to view the latency of data replication to it.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2730359951/p2636.png)

## Related operations

|Operation|Description|
|---------|-----------|
|[Create read-only instance](/intl.en-US/API Reference/Read-Only Instances/Create read-only instance.md)|Creates a read-only ApsaraDB for RDS instance.|

