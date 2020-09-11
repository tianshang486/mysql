# Restore the data of an ApsaraDB RDS for MySQL instance

This topic describes how to restore the data of an ApsaraDB RDS for MySQL instance.

The original RDS instance whose data you want to restore must meet the following requirements:

-   The original RDS instance is in the Running state and is not locked.
-   The original RDS instance does not have an ongoing migration task.
-   If you want to restore data to a point in time, the log backup function is enabled for the original RDS instance.
-   If you want to restore data from a backup, the original RDS instance has at least one backup.

For more information about how to restore data in other database engines, see the following topics:

-   [Restore the data of an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Restoration/Restore the data of an ApsaraDB RDS for SQL Server instance.md)
-   [Restore the data of an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Restoration/Restore data of an ApsaraDB RDS for PostgreSQL instance.md)
-   [Restore the data of an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Restoration/Restore the data of an ApsaraDB RDS for PPAS instance.md)
-   [Restore data of an RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Restoration/Restore data of an RDS for MariaDB instance.md)

## Background information

You can use one of the following methods to restore the data of the original RDS instance:

-   Method 1: Restore the data of the original RDS instance to a new RDS instance, verify the data on the new RDS instance, and then migrate the data from the new RDS instance back to the original RDS instance. This function was previously known as instance cloning. This topic describes this restoration method.
-   Method 2: Restore the data of individual databases or tables to the original RDS instance or to a new RDS instance. For more information, see [Restore individual databases and tables of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md).
-   Method 3: Restore the data of the original RDS instance to a new or existing RDS instance that resides in a different region. For more information, see [Restore an ApsaraDB RDS for MySQL instance across regions](/intl.en-US/RDS MySQL Database/Restoration/Restore an ApsaraDB RDS for MySQL instance across regions.md).

**Note:** For more information about how to restore the data of the original RDS instance to a user-created database, see [Use a physical backup file to restore an ApsaraDB RDS for MySQL instance to a user-created MySQL database](/intl.en-US/RDS MySQL Database/Restoration/Use a physical backup file to restore an ApsaraDB RDS for MySQL instance to a user-created MySQL database.md) or [Restore data from logical backup files of an ApsaraDB RDS for MySQL instance to a user-created database](/intl.en-US/RDS MySQL Database/Restoration/Restore data from logical backup files of an ApsaraDB RDS for MySQL instance to a user-created database.md).

## Precautions

-   The new RDS instance must have the same IP address whitelist, backup, and parameter settings as the original RDS instance.
-   The data information of the new RDS instance must be the same as the data information indicated by the specified data or log backup file of the original RDS instance.
-   The account information of the new RDS instance must be the same as the account information indicated by the specified data or log backup file of the original RDS instance.

## Billing

You must pay for the new RDS instance. For more information, see [Pricing, billable items, and billing methods](/intl.en-US/Purchase Guide/Pricing, billable items, and billing methods.md).

**Note:** If you use Alibaba Cloud Data Transmission Service \(DTS\) to migrate data from the new RDS instance back to the original RDS instance, you are not charged for the schema migration and full data migration.

## Restore data to a new RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where the target RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the target instance and click the instance ID.

4.  In the left-side navigation pane, click **Backup and Restoration**.

5.  In the upper-right corner of the page, click **Restore Database \(Previously Clone Database\)**.

6.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Billing Method**|    -   **Subscription**: A subscription-billed instance is an instance that you can subscribe to for a specified period of time and pay for up front. Subscription billing is more cost-effective than pay-as-you-go billing. Therefore, we recommend that you select subscription billing with a longer commitment. You can receive larger discounts for longer subscription periods.
    -   **Pay-As-You-Go**: A pay-as-you-go-billed instance is charged per hour based on your actual resource usage. We recommend that you select pay-as-you-go billing for short-term use. If you no longer need your pay-as-you-go-billed instance, you can release it to reduce costs. |
    |**Restore Mode**|    -   **By Time**: allows you to restore data to a point in time within the specified log retention period. The time is accurate to seconds. For more information about how to view or change the log backup retention period, see [Back up an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md).
    -   **By Backup Set**: allows you to restore data from a specified data backup. You can restore data only from a physical backup. You cannot restore data from a logical backup.
**Note:** The **By Time** option appears only when the log backup function is enabled. |
    |**Zone of Primary Node**|The zone to which the RDS instance belongs. A zone is an independent physical location within a region. The **Zone of Primary Node** parameter specifies the zone to which the primary RDS instance belongs. The **Zone of Secondary Node** parameter specifies the zone to which the secondary RDS instance belongs.

You can select the **Single-zone Deployment** or **Multi-zone Development** method.

    -   **Single-zone Deployment**: The **Zone of Primary Node** and the **Zone of Secondary Node** are the same.
    -   **Multi-zone Deployment**: The **Zone of Primary Node** and the **Zone of Secondary Node** are different. After you select the **Zone of Primary Node**, the system automatically allocates the **Zone of Secondary Node**.
The multi-zone deployment method provides zone-level disaster recovery for your business. We recommend that you select Multi-zone Deployment.

**Note:**

    -   After the RDS instance is created, you can view information about the RDS instance and its secondary RDS instance on the **Service Availability** page.
    -   If you select the RDS Basic Edition, the database system consists of only one RDS instance and supports only the single-zone deployment method.
![Select zones](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0650359951/p87361.png) |
    |**Instance Type**|    -   **Entry-level**: belongs to the general-purpose instance family. A general-purpose instance exclusively occupies the allocated memory and I/O resources. However, it shares CPU and storage resources with other general-purpose instances that are deployed on the same server.
    -   **Enterprise-level**: belongs to the dedicated instance family. A dedicated instance exclusively occupies the allocated CPU, memory, storage, and I/O resources. The top configuration of the dedicated instance family is the dedicated host instance family. A dedicated host instance exclusively occupies all the CPU, memory, storage, and I/O resources of the server where it is deployed.
**Note:** Each instance type supports a specific number of CPU cores, memory capacity, maximum number of connections, and maximum IOPS. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). |
    |**Capacity**|The storage capacity that the RDS instance has available to store data files, system files, binary log files, and transaction files. You can adjust the storage capacity in increments of 5 GB. **Note:** If you select local SSDs, the storage capacity of the RDS instance varies based on the instance type. This restriction does not apply if you select standard or enhanced SSDs. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). |

7.  Click **Next: Instance Configuration**.

8.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Network Type**|    -   **Classic Network**: a traditional type of network.
    -   **VPC**: A virtual private cloud \(VPC\) is an isolated network that provides higher security and better performance than the classic network. If you select the VPC network type, you must also specify the **VPC** and **VSwitch of Primary Node** parameters.
**Note:** The RDS instance must have the same network type as the ECS instance that you want to connect. If the RDS and ECS instances both have the VPC network type, they must also reside in the same VPC. Otherwise, the RDS and ECS instances cannot communicate over an internal network. |

9.  Click **Next: Confirm Order**.

10. Confirm the settings in the **Parameters** section, specify the **Purchase Plan** and the **Duration**, read and select Terms of Service, and click **Pay Now**. You need to specify the Duration only when the new RDS instance uses subscription billing.

    **Note:** If the new RDS instance uses subscription billing, we recommend that you select **Auto-Renew Enabled**. This relieves the need to renew the subscription and avoids interruptions to your workloads due to overdue payments.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5150359951/p52773.png)


## Verify data on the new RDS instance

For more information, see [Connect to an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Connect to an ApsaraDB RDS for MySQL instance.md).

## Migrate data to the original RDS instance

After you verify the data on the new RDS instance, you can migrate the data from the new RDS instance back to the original RDS instance. For more information, see [Migrate data between RDS instances](https://www.alibabacloud.com/help/zh/doc-detail/26626.htm).

**Note:** The migration does not affect workloads on the original RDS instance.

## FAQ

-   How do I restore a database that I accidentally deleted?

    ApsaraDB for RDS allows you to restore only the database that you accidentally deleted. For more information, see [Restore individual databases and tables of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md). If your RDS instance does not support the restoration of individual databases and tables, you can restore the data of the database that you accidentally deleted to a new RDS instance, verify the data on the new RDS instance, and then migrate the data from the new RDS instance back to the original RDS instance.

-   If my RDS instance does not have a data backup, can I restore its data to a point in time?

    No, you cannot restore the data of your RDS instance to a point in time if your RDS instance does not have a data backup. To restore data to a point in time, you must restore the data of a full backup that was generated before the specified point in time. Then, you must restore the data of the log backup file that was generated at the specified point in time. The log backup contains the incremental data that was backed up after the full backup was generated.

-   When I create an RDS instance to which data will be restored, why am I unable to select a VSwitch for my primary RDS instance?

    If no VSwitches are available in the zone that you specified in the Basic Configurations step, you cannot select a VSwitch for your primary RDS instance in the Instance Configuration step. In this case, you can click **go to the VPC console**. In the VPC console, create a VSwitch. Then, you can select the VSwitch for your primary RDS instance.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1630359951/p70932.png)


