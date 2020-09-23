# Restore the data of an ApsaraDB RDS for SQL Server instance

This topic describes how to restore the data of an ApsaraDB RDS for SQL Server instance.

You can use one of the following methods to restore the data of an RDS instance:

-   [Restore data to an existing RDS instance](#section_huifu)
-   [Restore data to a new RDS instance](#section_l2n_r4x_52b)
-   [Restore data to the original RDS instance by using a temporary RDS instance](#section_ejq_2yz_52b)

## Restore data to an existing RDS instance

You can restore some or all of the databases on an RDS instance from a backup set or to a point in time. The destination RDS instance can be the original RDS instance or another existing RDS instance.

This function is supported for RDS instances that run SQL Server 2008 R2 with standard or enhanced SSDs, SQL Server 2012, SQL Server 2016, SQL Server 2017 SE, or SQL Server 2019 SE.

Procedure

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Backup and Restoration**.

5.  In the upper-right corner of the page, click **Restore**.

6.  In the dialog box that appears, select **Restore to Existing Instance** and click OK.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6359259951/p10029.png)

7.  Configure the following parameters and click **OK**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6359259951/p10031.png)

    |Parameter|Description|
    |---------|-----------|
    |Restore Method|    -   **By Time**: allows you to restore data to a point in time within the specified log backup retention period. For more information about how to view or change the log backup retention period, see [Back up an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance.md).
    -   **By Backup Set**: allows you to restore data from a specified full or incremental backup set. |
    |Restore Time|Select the point in time to which you want to restore data. This parameter appears only when you set the Restore Method parameter to **By Time**.|
    |Backup Set|Select the backup set from which you want to restore data. This parameter appears only when you set the Restore Method parameter to **By Backup Set**.|
    |Instance|Select the destination RDS instance to which you want to restore data. By default, ApsaraDB for RDS displays the original RDS instance and all of the RDS instances that are created by using the same Alibaba Cloud account, reside in the same region, and run the same database engine version as the original RDS instance.

**Note:**

    -   If the original RDS instance belongs to the shared instance family, you cannot restore its data from a backup set to a general-purpose or dedicated RDS instance. Similarly, if the original RDS instance belongs to the general-purpose or dedicated instance family, you cannot restore its data from a backup set to a shared RDS instance.
    -   If ApsaraDB for RDS displays a large number of RDS instances, you can enter a keyword in the Instance field to search for the required destination RDS instance. |
    |Databases to Restore|    1.  Select the databases that you want to restore. By default, all of the databases on the original RDS instance are displayed and selected.
        -   If you want to restore all data of the original RDS instance, select all of the databases.
        -   If you want to restore one or more databases, select only the required databases.
    2.  Specify new names for the selected databases. By default, the original names of the selected databases are retained.

**Note:** The names of the selected databases on the original RDS instance cannot be the same as those of the existing databases on the destination RDS instance. |

    **Note:**

    -   If a selected database on the original RDS instance has the same name as an existing database on the destination RDS instance, you must select **New Name** and specify a new name for the selected database.
    -   The value of the **New Name** parameter can only contain lowercase letters, digits, underscores \(\_\), and hyphens \(-\).

## Restore data to a new RDS instance

You can restore the data of an RDS instance from a backup set or to a point in time. This process was known as instance cloning. If you restore data from a backup set, you can restore some or all of the databases whose data is included in the backup set.

You must pay for the new RDS instance. If you no longer require the original RDS instance after the restoration, we recommend that you release or unsubscribe from the original RDS instance in a timely manner. For more information, see [Release or unsubscribe from an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Instance/Release or unsubscribe from an ApsaraDB RDS for SQL Server instance.md).

This function is supported for RDS instances that run SQL Server 2008 R2 with standard or enhanced SSDs, SQL Server 2012, SQL Server 2016, or SQL Server 2017.

Procedure

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Backup and Restoration**.

5.  In the upper-right corner of the page, click **Restore**.

6.  In the dialog box that appears, select **Restore to New Instance** and click OK.

7.  On the **Restore Database \(Previously Clone Instance\)** page, configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Billing Method**|    -   **Subscription**: A subscription-billed instance is an instance that you can subscribe to for a specified period of time and pay for up front. Subscription billing is more cost-effective than pay-as-you-go billing. Therefore, we recommend that you select subscription billing with a longer commitment. You can receive larger discounts for longer subscription periods.
    -   **Pay-As-You-Go**: A pay-as-you-go-billed instance is charged per hour based on your actual resource usage. We recommend that you select pay-as-you-go billing for short-term use. If you no longer require your pay-as-you-go-billed instance, you can release it to reduce costs. |
    |**Restore Mode**|    -   **By Time**: allows you to restore data to a point in time within the specified log backup retention period. For more information about how to view or change the log backup retention period, see [Back up an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance.md).
    -   **By Backup Set**: allows you to restore data from a specified backup set.
**Note:**

    -   The **By Time** option appears only when the log backup function is enabled.
    -   You can restore some or all of the databases on the original RDS instance. |
    |**Database**|Specify whether you want to restore some or all of the databases on the original RDS instance. If you select **Part**, you must manually enter the names of the databases that you want to restore. In addition, you must separate the database names with commas \(,\).|
    |**Edition**|    -   **Basic**: Your database system consists of only one instance. Computing is separated from storage to increase cost-effectiveness.
    -   **High-availability**: Your database system consists of one primary instance and one secondary instance. The primary and secondary instances work in the classic high-availability architecture.
    -   **AlwaysOn**: Your database system consists of one primary instance, one secondary instance, and up to seven read-only instances that are created to process more read requests.
**Note:** The RDS editions available vary based on the region and database engine version you select. For more information, see [ApsaraDB for RDS edition overview](/intl.en-US/Product Introduction/Product editions/Overview of ApsaraDB for RDS editions.md). |
    |**Zone**|The zone to which the RDS instance belongs. A zone is an independent physical location within a region. The **Zone of Primary Node** parameter specifies the zone to which the primary RDS instance belongs. The **Zone of Secondary Node** parameter specifies the zone to which the secondary RDS instance belongs.

You can select the **Single-zone Deployment** or **Multi-zone Development** method.

    -   **Single-zone Deployment**: The **Zone of Primary Node** and the **Zone of Secondary Node** are the same.
    -   **Multi-zone Deployment**: The **Zone of Primary Node** and the **Zone of Secondary Node** are different. After you specify the **Zone of Primary Node**, the system automatically allocates the **Zone of Secondary Node**.
The multi-zone deployment method provides zone-level disaster recovery. We recommend that you select the multi-zone deployment method.

**Note:**

    -   After the RDS instance is created, you can view information about the RDS instance and its secondary RDS instance on the **Service Availability** page.
    -   If you select the RDS Basic Edition, the database system consists of only one RDS instance and supports only the single-zone deployment method.
![Select zones](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0650359951/p87361.png) |
    |**Instance Type**|    -   **Entry-level**: belongs to the general-purpose instance family. A general-purpose instance exclusively occupies the memory and I/O resources allocated to it, but shares CPU and storage resources with the other general-purpose instances that are deployed on the same server.
    -   **Enterprise-level**: belongs to the dedicated or dedicated host instance family. A dedicated instance exclusively occupies the CPU, memory, storage, and I/O resources allocated to it. The top configuration of the dedicated instance family is the dedicated host. A dedicated host instance occupies all the CPU, memory, storage, and I/O resources on the server where it is housed.
**Note:** Each instance type supports a specific number of CPU cores, memory capacity, maximum number of connections, and maximum IOPS. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). |
    |**Capacity**|The storage capacity that the RDS instance has available to store data files, system files, binary log files, and transaction files. You can adjust the storage capacity in increments of 5 GB. **Note:** The dedicated instance family supports exclusive allocations of resources. The storage capacity of each instance type with local SSDs in this family is fixed. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). |

8.  Click **Next: Instance Configuration**.

9.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Network Type**|    -   **Classic Network**: the traditional type of network.
    -   **VPC**: A virtual private cloud \(VPC\) is an isolated network that provides higher security and better performance than the classic network. If you select the VPC network type, you must also specify the **VPC** and the **VSwitch of Primary Node**.
**Note:** The RDS instance must have the same network type as the ECS instance that you want to connect. If the RDS and ECS instances both have the VPC network type, they must also reside in the same VPC. Otherwise, the RDS and ECS instances cannot communicate over an internal network. |
    |**Resource Group**|The resource group to which the new RDS instance belongs.|

10. Click **Next: Confirm Order**.

11. Confirm the settings in the **Parameters** section, specify the **Purchase Plan** and the **Duration**, read and select Terms of Service, and click **Pay Now**. You only need to specify the Duration when the new RDS instance uses subscription billing.


## Restore data to the original RDS instance by using a temporary RDS instance

This function is supported for the following SQL Server versions:

-   SQL Server 2012 EE Basic
-   SQL Server 2012 Web
-   SQL Server 2016 Web
-   SQL Server 2008 R2 \(with local SSDs\)

For more information, see [Restore data of ApsaraDB RDS for SQL Server instances by using temporary instances](/intl.en-US/RDS SQL Server Database/Restoration/Restore data of ApsaraDB RDS for SQL Server instances by using temporary instances.md).

## Operations

|Operation|Description|
|---------|-----------|
|[Restore databases](/intl.en-US/API Reference/Restoration/Restore databases.md)|Restores the data of an ApsaraDB for RDS instance.|

