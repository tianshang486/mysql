# Create a read-only ApsaraDB RDS for PostgreSQL instance

This topic describes how to create a read-only RDS instance for your primary ApsaraDB RDS for PostgreSQL instance. Read-only RDS instances allow your database system to process more read requests. Read-only RDS instances also increase the throughput of your application. Each read-only RDS instance is a replica of the primary RDS instance. Data updates on the primary RDS instance are automatically synchronized to all of the read-only RDS instances.

For more information about read-only RDS instances, see [Overview of read-only ApsaraDB RDS for PostgreSQL instances](/intl.en-US/RDS PostgreSQL Database/Quick start/RDS for PostgreSQL read-only instances/Overview of read-only ApsaraDB RDS for PostgreSQL instances.md).

## Prerequisites

-   The primary RDS instance runs PostgreSQL 10, 11, or 12.
-   If the primary RDS instance uses local SSDs, it must be a dedicated RDS instance that provides at least 8 CPU cores and 32 GB of memory. If the primary RDS instance uses standard or enhanced SSDs, no specific requirements are imposed for the instance specifications.

**Note:** If the primary RDS instance runs PostgreSQL 10 with standard or enhanced SSDs, you cannot create read-only RDS instances.

## Precautions

-   You can create read-only RDS instances for the primary RDS instance. However, you cannot convert existing RDS instances into read-only RDS instances.
-   When you create a read-only RDS instance, your database system replicates data to the read-only instance from the secondary RDS instance. This avoids interruptions to your workloads on the primary RDS instance.
-   A read-only RDS instance does not inherit the parameter settings of the primary RDS instance. Your database system generates default parameter settings for the read-only RDS instance. You can modify these default parameter settings in the ApsaraDB RDS console.
-   If the primary RDS instance uses local SSDs, the specifications and storage capacity of a read-only RDS instance cannot be lower than those of the primary RDS instance.
-   If the primary RDS instance uses local SSDs, you can create a maximum of five read-only RDS instances. If the primary RDS instance uses standard or enhanced SSDs, you can create a maximum of 32 read-only RDS instances.
-   If the primary RDS instance uses local SSDs, its read-only RDS instances run in the high-availability architecture. If the primary RDS instance uses standard or enhanced SSDs, its read-only RDS instances run in the single-node architecture.

    **Note:** In the single-node architecture, a read-only RDS instance does not have a secondary RDS instance as its backup. For availability purposes, we recommend that you purchase more than one read-only RDS instance. This way, you can implement failovers by using the libpq or Java Database Connectivity \(JDBC\) API. For more information, see [Configure automatic failover and read/write splitting](/intl.en-US/RDS PostgreSQL Database/Best Practices/Configure automatic failover and read/write splitting.md).

-   Read-only RDS instances are charged at an hourly fee based on the pay-as-you-go billing method.

## Create a read-only RDS instance

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, select the region where the primary RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the primary RDS instance and click its ID.
4.  In the Distributed by Instance Role section of the Basic Information page, click **Create Read-only Instance**.

    ![Create Read-only Instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6840359951/p39780.png)

5.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Zone**|The zone where the read-only RDS instance resides. Each zone is an independent physical location within a region. Zones in the same region provide the same services. Multi-zone deployment provides zone-level disaster recovery for your business.|
    |**Instance Type**|    -   **Entry-level**: belongs to the general-purpose instance family. A general-purpose instance exclusively occupies the allocated memory and I/O resources. However, it shares CPU and storage resources with the other general-purpose instances that are deployed on the same server.
    -   **Enterprise-level**: belongs to the dedicated instance family. A dedicated instance exclusively occupies the allocated CPU, memory, storage, and I/O resources. The top configuration of the dedicated instance family is the dedicated host instance family. A dedicated host instance exclusively occupies all the CPU, memory, storage, and I/O resources of the server where it is deployed.
**Note:** Each instance type supports a specific number of CPU cores, memory capacity, maximum number of connections, and maximum IOPS. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). |
    |**Capacity**|

6.  Click **Next: Instance Configuration** and configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Network Type**|    -   **Classic Network**: the traditional type of network.
    -   **VPC**: A virtual private cloud \(VPC\) is an isolated network that provides higher security and better performance than the classic network. If you select the VPC network type, you must also specify the **VPC** and the **VSwitch of Primary Node**.
**Note:** The RDS instance must have the same network type as the ECS instance that you want to connect. If the RDS and ECS instances both have the VPC network type, they must also reside in the same VPC. Otherwise, the RDS and ECS instances cannot communicate over an internal network. |

7.  Click **Next: Confirm Order**.
8.  Read and select Terms of Service, click **Pay Now**, and then complete the payment.

A few minutes are required to create the read-only RDS instance.

## View a read-only RDS instance

To view a read-only RDS instance on the Instances page, perform the following steps:

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the read-only RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the read-only RDS instance and click its ID.

    ![Find the read-only RDS instance that you want to view](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7840359951/p39783.png)


To view a read-only RDS instance on the Basic Information page of the primary RDS instance, perform the following steps:

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the primary RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the primary RDS instance and click its ID.
4.  On the **Basic Information** page, move the pointer over the number of read-only RDS instances and click the ID of the read-only instance that you want to view.

    ![Go to the read-only RDS instance from the primary RDS instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7840359951/p39784.png)


## View the latency of data replication to a read-only RDS instance

When a read-only RDS instance synchronizes data from the primary RDS instance, a latency may occur. You can view the latency on the Basic Information page of the read-only RDS instance.

![Latency of data replication to a read-only RDS instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7840359951/p39785.png)

## Related operations

|Operation|Description|
|---------|-----------|
|[Create read-only instance](/intl.en-US/API Reference/Read-Only Instances/Create read-only instance.md)|Creates a read-only ApsaraDB RDS instance.|

