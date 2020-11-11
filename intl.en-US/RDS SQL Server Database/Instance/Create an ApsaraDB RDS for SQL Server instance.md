# Create an ApsaraDB RDS for SQL Server instance

This topic describes how to create an ApsaraDB RDS for SQL Server instance in the ApsaraDB RDS console. You can also call an API operation to create an ApsaraDB RDS for SQL Server instance.

## Billing

For more information, see [Pricing, billable items, and billing methods](/intl.en-US/Purchase Guide/Pricing, billable items, and billing methods.md).

## Prerequisites

You have an Alibaba Cloud account. For more information, see [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/doc-detail/50482.html).

## Procedure

1.  Log on to the [ApsaraDB RDS console](https://rds-buy.aliyun.com/nextBuy/?#/create/rds/mysql).

    **Note:** In the upper-right corner of the page, you can click **Back to Old Version** to switch back to the original ApsaraDB RDS console.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5150359951/p60573.png)

2.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Billing Method**|    -   **Subscription**: A subscription-billed instance is an instance that you can subscribe to for a specified period of time and pay for up front. Subscription billing is more cost-effective than pay-as-you-go billing. Therefore, we recommend that you select subscription billing with a longer commitment. You can receive larger discounts for longer subscription periods.
    -   **Pay-As-You-Go**: A pay-as-you-go-billed instance is charged per hour based on your actual resource usage. We recommend that you select pay-as-you-go billing for short-term use. If you no longer need your pay-as-you-go-billed instance, you can release it to reduce costs.
**Note:** A maximum of 30 pay-as-you-go-billed instances are allowed per Alibaba Cloud account. If you want to increase this quota, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm#/ticket/createIndex). |
    |**Region**|The region to which the RDS instance belongs.     -   After you confirm your purchase order, you cannot change the selected region.
    -   We recommend that you select a region that is in close proximity to the geographic location where your users reside. This increases the access speeds of your users.
    -   The RDS instance must reside in the same region as the ECS instance that you want to connect. If the RDS and ECS instances reside in different regions, they cannot communicate over an internal network and therefore cannot deliver optimal performance. |
    |**Database Engine**|The database engine and version that the RDS instance runs. Select **Microsoft SQL Server**. The supported SQL Server versions are 2008 R2, 2012, 2016, 2017, and 2019. **Note:** The available database engines and versions vary based on the selected region. |
    |**Edition**|    -   **Basic**: The database system consists of only one RDS instance. Computing is separated from storage to increase cost-effectiveness.
    -   **High-availability**: The database system consists of one primary RDS instance and one secondary RDS instance. These RDS instances work in the high availability architecture.
    -   **AlwaysOn**: The database system consists of one primary RDS instance, one secondary RDS instance, and up to seven read-only RDS instances. You can create read-only RDS instances to scale up the read capability of the database system.
**Note:** The available RDS editions vary based on the selected region and database engine version. For more information, see [Overview of ApsaraDB RDS editions](/intl.en-US/Product Introduction/Product editions/Overview of ApsaraDB for RDS editions.md). |
    |**Storage Type**|    -   **Local SSD**: A local SSD resides on the same server as the database engine. You can store data on local SSDs to reduce I/O latency.
    -   **Enhanced SSD**: An enhanced SSD is an ultra-high performance disk that is developed by Alibaba Cloud based on the next-generation distributed block storage architecture. It integrates 25 Gigabit Ethernet and remote direct memory access \(RDMA\) technologies. This reduces one-way latency and delivers up to 1 million random input/output operations per second \(IOPS\). Supported enhanced SSDs are available in the following three performance levels \(PLs\):
        -   PL1 \(Enhanced SSD\): An enhanced SSD of PL1 is a regular enhanced SSD.
        -   PL2 \(ESSD PL2\): An enhanced SSD of PL2 delivers IOPS and throughput that are twice as high as those delivered by an enhanced SSD of PL1.
        -   PL3 \(ESSD PL3\): An enhanced SSD of PL3 delivers IOPS that is 20 times as high as the IOPS delivered by an enhanced SSD of PL1. It also delivers throughput that is 11 times as high as the throughput delivered by an enhanced SSD of PL1. Enhanced SSDs of PL3 are suitable for workloads that require high I/O performance in processing concurrent requests and stable read/write latency.
    -   **Standard SSD**: A standard SSD is an elastic block storage device that is designed based on the distributed storage architecture. You can store data on standard SSDs to separate computing from storage.
For more information, see [Storage types](/intl.en-US/Product Introduction/Storage types.md).

**Note:** If you select the **standard SSD** or **enhanced SSD** storage type, you can enable **Disk Encryption**. This allows you to maximize protection for your data. For more information, see [Configure disk encryption for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Data security/Configure disk encryption for an ApsaraDB RDS for SQL Server instance.md). |
    |**Zone of Primary Node and Zone of Secondary Node**|The zone to which the RDS instance belongs. A zone is an independent physical location within a region. The **Zone of Primary Node** parameter specifies the zone to which the primary RDS instance belongs. The **Zone of Secondary Node** parameter specifies the zone to which the secondary RDS instance belongs.

You can select the **Single-zone Deployment** or **Multi-zone Development** method.

    -   **Single-zone Deployment**: The **Zone of Primary Node** and the **Zone of Secondary Node** are the same.
    -   **Multi-zone Deployment**: The **Zone of Primary Node** and the **Zone of Secondary Node** are different. After you specify the **Zone of Primary Node**, the system automatically allocates the **Zone of Secondary Node**.
The multi-zone deployment method provides zone-level disaster recovery. We recommend that you select the multi-zone deployment method.

**Note:**

    -   After the RDS instance is created, you can view information about the RDS instance and its secondary RDS instance on the **Service Availability** page.
    -   If you select the RDS Basic Edition, the database system consists of only one RDS instance and supports only the single-zone deployment method.
![Select zones](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0650359951/p87361.png) |
    |**Instance Type**|    -   **Entry-level**: belongs to the general-purpose instance family. A general-purpose instance exclusively occupies the allocated memory and I/O resources. However, it shares CPU and storage resources with the other general-purpose RDS instances that are deployed on the same server.
    -   **Enterprise-level**: belongs to the dedicated instance family. A dedicated instance exclusively occupies the allocated CPU, memory, storage, and I/O resources. The top configuration of the dedicated instance family is the dedicated host instance family. A dedicated host instance exclusively occupies all the CPU, memory, storage, and I/O resources of the server where it is deployed.
**Note:** Each instance type supports a specific number of CPU cores, memory capacity, maximum number of connections, and maximum IOPS. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). |
    |**Capacity**|The storage capacity that the RDS instance has available to store data files, system files, binary log files, and transaction files. The storage capacity increases in increments of 5 GB. **Note:** The dedicated instance family supports exclusive allocations of resources. Therefore, the storage capacity of each instance type with local SSDs in this family is fixed. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). |

3.  Click **Next: Instance Configuration**.

4.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Network Type**|    -   **Classic Network**: the traditional type of network.
    -   **VPC**: A virtual private cloud \(VPC\) is an isolated network that provides higher security and better performance than the classic network. If you select the VPC network type, you must also specify the **VPC** and the **VSwitch of Primary Node**.
**Note:** The RDS instance must have the same network type as the ECS instance that you want to connect. If the RDS and ECS instances both have the VPC network type, they must also reside in the same VPC. Otherwise, the RDS and ECS instances cannot communicate over an internal network. |
    |**Resource Group**|

5.  Click **Next: Confirm Order**.

6.  Confirm the settings in the **Parameters** section, specify the **Purchase Plan** and the **Duration**, read and select Terms of Service, and click **Pay Now**. You only need to specify the Duration when you create a subscription-billed RDS instance.

    **Note:** When you create a subscription-billed RDS instance, we recommend that you select **Auto-Renew Enabled**. This allows you to avoid the need to manually renew the subscription. This also allows you to avoid interruptions to your workloads due to overdue payments.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5150359951/p52773.png)


In the top navigation bar, select the required region. Then, you can view the RDS instance that you created.

![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

## What to do next

After the RDS instance is created, you must configure IP address whitelists or security groups and create accounts on the RDS instance. If you want to connect to the RDS instance over the Internet, you must also apply for a public endpoint. After you connect to the RDS instance, you can migrate data to the RDS instance. For more information, see the following topics:

-   [Configure a whitelist for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Configure a whitelist for an ApsaraDB RDS for SQL Server instance.md)
-   [Create accounts and databases for an ApsaraDB for RDS instance running SQL Server 2008 R2](/intl.en-US/RDS SQL Server Database/Quick start/Creating accounts and databases/Create accounts and databases for an ApsaraDB for RDS instance running SQL Server
         2008 R2.md)
-   [Create accounts and databases for an ApsaraDB for RDS instance running SQL Server 2012, 2016, 2017 SE, or 2019](/intl.en-US/RDS SQL Server Database/Quick start/Creating accounts and databases/Create accounts and databases for an ApsaraDB for RDS instance running SQL Server
         2012, 2016, 2017 SE, or 2019.md)
-   [Create accounts and databases for an ApsaraDB for RDS instance running SQL Server 2017 EE](/intl.en-US/RDS SQL Server Database/Quick start/Creating accounts and databases/Create accounts and databases for an ApsaraDB for RDS instance running SQL Server
         2017 EE.md)
-   [Apply for or release a public endpoint on an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Database connection/Apply for or release a public endpoint on an ApsaraDB RDS for SQL Server instance.md)
-   [Connect to an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Connect to an ApsaraDB RDS for SQL Server instance.md)

## FAQ

-   After I create an RDS instance, why does the ApsaraDB for RDS console not respond and why am I unable to find the RDS instance that I created?

    This issue may occur due to the following two reasons:

    -   The RDS instance that you created does not reside in the selected region.

        In the top navigation bar, select the region where the RDS instance resides. Then, you can find the RDS instance that you created.

        ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

    -   The selected zone cannot provide sufficient resources.

        Resources in zones are dynamically allocated. After you submit your purchase order, the selected zone may be unable to provide sufficient resources. As a result, the RDS instance cannot be created. In this case, we recommend that you select another zone and try again. If the RDS instance cannot be created, you can go to [the Orders page](https://billing.console.aliyun.com/?#/order/list/) in the Billing Management console to view the refunded fees.

-   How do I authorize a RAM user to manage my RDS instance?

    For more information, see [Use RAM to manage ApsaraDB for RDS permissions](https://www.alibabacloud.com/help/zh/doc-detail/58932.htm).

-   If my RDS instance resides in a VPC, how many private IP addresses does it occupy?

    The number of private IP addresses that your RDS instance occupies can vary based on the selected database engine and RDS edition.

    -   MySQL 5.5, 5.6, 5.7, and 8.0 on RDS High-availability Edition \(with local SSDs\): 1
    -   MySQL 5.6, 5.7, and 8.0 on RDS Enterprise Edition \(with local SSDs\): 1
    -   MySQL 5.7 on RDS Basic Edition \(with standard SSDs\): 1
    -   MySQL 8.0 on RDS Basic Edition \(with standard SSDs\): 2
    -   MySQL 5.7 and 8.0 on RDS High-availability Edition \(with standard or enhanced SSDs\): 3
    -   MySQL 5.7 and 8.0 on RDS Enterprise Edition \(with standard or enhanced SSDs\): 1

## Related operations

|Operation|Description|
|---------|-----------|
|[Create instance](/intl.en-US/API Reference/Instance management/Create instance.md)|Creates an ApsaraDB for RDS instance.|

