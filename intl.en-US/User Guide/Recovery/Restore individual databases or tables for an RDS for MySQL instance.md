# Restore individual databases or tables for an RDS for MySQL instance {#concept_ocr_swk_ngb .concept}

This topic describes how to restore individual databases or tables for an RDS for MySQL instance.

## Prerequisites {#section_o5q_1p4_ydb .section}

-   The DB engine version and edition is one of the following:
    -   MySQL 5.6 High-availability Edition
    -   MySQL 5.7 High-availability Edition \(with local SSDs\)
-   The Restore Individual Database/Table function is enabled in the console \(navigation path: **Backup and Restoration** \> **Backup Settings**\).

    ![控制台开通库表恢复](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115355/156817066044546_en-US.png)

    **Note:** After the Restore Individual Database/Table function is enabled, the backup file format changes to support database and table restoration. This function cannot be disabled once it is enabled.

-   If you want to restore data to the current RDS instance, the current RDS instance must meet the following conditions:
    -   The instance is in **Running** state and is not locked.
    -   The instance is not involved in any migration task.
    -   If you want to restore data by time, the log backup function is enabled.
    -   If you want to restore data by backup set, the instance must have at least one backup set.
-   If you want to restore data to a new RDS instance, the current RDS instance must meet the following conditions:
    -   The instance is in **Running** state and is not locked.
    -   If you want to restore data by time, the log backup function is enabled.
    -   If you want to restore data by backup set, the instance must have at least one backup set.

## Precautions {#section_slr_ynq_ngb .section}

-   The Restore Individual Database/Table function changes the format of backup files from .tar to .xbstream. After this change, the storage space occupied by backup files slightly increases. If the occupied storage space exceeds the quota of free backup space, additional fees are incurred. For more information, see [View the quota of free backup space for an RDS for MySQL instance](intl.en-US/RDS for MySQL User Guide/Database backup/View the quota of free backup space for an RDS for MySQL instance.md#). We recommend that you plan the backup cycle properly to meet your business needs while also maximizing backup space utilization.
-   The Restore Individual Database/Table function is available only when the number of tables in the RDS instance does not exceed 50,000.
-   You can select and restore up to 50 databases or tables.

## Procedure {#section_m3j_zlb_3gb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.
3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click Backup and Restoration.
5.  In the upper-right corner, click **Restore Individual Database/Table**. In the displayed dialog box, set the following parameters.

    **Note:** If the **Restore Individual Database/Table** button is unavailable, you must enable the Restore Individual Database/Table function. For more information, see [Prerequisites](#section_o5q_1p4_ydb).

    ![库/表级别恢复](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115355/156817066037783_en-US.png)

    ![库/表级别恢复参数设置1](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115355/156817066037784_en-US.png)

    |Parameter|Description|
    |---------|-----------|
    |**Restore To**|     -   **Current Instance**: restores the selected databases or tables to the current RDS instance.
    -   **New Instance**: purchases a new RDS instance and restores the selected databases or tables to the new RDS instance.
 |
    |**Restore Method**|     -   **By Backup Set**
    -   **By Time**: You can specify any time point within the log retention period. For information about how to view or change the log retention period, see [Back up the data of an RDS for MySQL instance](intl.en-US/RDS for MySQL User Guide/Database backup/Back up the data of an RDS for MySQL instance.md#).
 **Note:** The **By Time** option is available only when the log backup function is enabled.

 |
    |**Backup Set**|Select the backup set used for restoring databases or tables. **Note:** This parameter is available when you set the **Restore Method** parameter to **By Backup Set**.

 |
    |**Restore Time**|Select the time point from which you want to restore databases or tables. **Note:** This parameter is available when you set the **Restore Method** parameter to **By Time**.

 |
    |**Databases and Tables to Restore**|Select the databases or tables you want to restore.|
    |**Selected Databases and Tables**|     -   Displays the selected databases or tables. You can specify the names of the databases or tables to which data is restored.
    -   Displays the total size of the selected databases or tables, and the remaining storage space of the instance. Make sure that the remaining storage space is sufficient.
 |

6.  Click **OK**.

    **Note:** If you set **Restore To** to **New Instance**, you are directed to the page for purchasing a new RDS instance. You must set the instance parameters and complete the payment.

    |Parameter|Description|
    |---------|-----------|
    |**Edition**|     -   **Basic**: The DB system has only one instance. In this edition, compute is separated from storage, which is cost-effective. However, we recommend that you do not use this edition in production environments.
    -   **High-availability**: The DB system has two instances: one master instance and one slave instance. The two instances work in a classic high-availability architecture.
 For more information about the product series, see [Product series overview](../../../../intl.en-US/Product Introduction/Product series/Product series overview.md#). The product series available in the console vary depending on the used DB engine version.

 |
    |**Zone**| A zone is an independent physical location in a region. Zones in the same region are basically the same.

 You can create an RDS instance in the same or different zone from your ECS instance. **Note:** The new RDS instance must be in the same region as the current RDS instance.

 |
    |**CPU and Memory**| Each instance type corresponds to specific number of CPU cores, memory space, maximum number of connections, and maximum IOPS. For more information, see [Instance types](../../../../intl.en-US/Product Introduction/Instance types/Instance types.md#).

 RDS instances fall into the following types:

    -   **General-purpose instance**: A general-purpose instance owns dedicated memory and I/O resources but shares CPU and storage resources with the other general-purpose instances on the same server.
    -   **Dedicated instance**: A dedicated instance owns dedicated CPU, memory, storage, and I/O resources.
    -   **Dedicated host**: A dedicated-host instance owns all the CPU, memory, storage, and I/O resources on the server where it is deployed.
 For example, **8 Cores, 32 GB** is the specification for a general-purpose instance, **8 Cores, 32 GB \(Dedicated instance\)** is the specification for a dedicated instance, and **30 Cores, 220 GB \(Dedicated host\)** is the specification for a dedicated-host instance.|
    |**Capacity**|Used to store data files, system files, binary log files, and transaction files.|
    |**Network Type**|     -   **Classic Network**: a classic network.
    -   **VPC** \(recommend\): A Virtual Private Cloud \(VPC\) is an isolated network that is superior to a classic network in terms of security and performance.
 |


