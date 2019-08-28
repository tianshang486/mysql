# Restore the data of an RDS for MySQL instance {#concept_vrh_qp4_ydb .concept}

If you have a data backup for an RDS for MySQL instance, you can restore the data by using the backup.

You can use one of the following methods to restore the data of an RDS for MySQL instance:

-   Method 1: Restore data to a new RDS instance, verify the data, and then migrate the data to the original RDS instance. This topic introduces this method.

    **Note:** For more information about how to restore data through a single-database logical backup, see [\(RDS for MySQL\) Restore logical backup file to on-premises database](../intl.en-US/FAQs/Data backup__recovery/(RDS for MySQL) Restore logical backup file to on-premises database.md#).

-   Method 2: Restore single-database or -table data to the original RDS instance or a new RDS instance. For more information, see [Restore MySQL databases or tables](intl.en-US/RDS for MySQL User Guide/Database restoration/Restore MySQL databases or tables.md#).

## Precautions {#section_ng5_ms5_xgb .section}

-   The whitelist settings, backup settings, and parameter settings of the new RDS instance must be the same as those of the original RDS instance.
-   The data information of the new RDS instance must be the same as that of the used backup file or that from the specified time point.
-   The new RDS instance carries the account information in the used backup file or that from the specified time point.

## Fees {#section_uh5_4bq_w2b .section}

For more information, see [ApsaraDB RDS for MySQL pricing](https://www.alibabacloud.com/product/apsaradb-for-rds#pricing).

## Prerequisites {#section_o5q_1p4_ydb .section}

The original RDS instance must meet the following conditions:

-   The instance is in the **Running** state and is not locked.
-   No migration task is being performed for the instance.
-   If you want to restore the data from a time point, the log backup function is enabled.
-   If you want to restore the data from a backup set, at least one backup set is available for the instance.

## Restore data to a new RDS instance. {#section_est_dp4_ydb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156697279636543_en-US.png)

3.  Find the target RDS instance and click its ID.
4.  In the left-side navigation pane, click **Backup and Restoration**.
5.  In the upper-right corner, click **Restore Database \(Previously Clone Database\)**.
6.  On the displayed Restore Database \(Previously Clone Instance\) page, select a billing method:

    -   **Pay-As-You-Go**: Fees are calculated by hour according to the actual job size. This billing method is suitable to a short-term RDS instance, which can be released immediately after you finish the data restoration.
    -   **Subscription**: Fees are estimated in advance, and the relevant usage allocation is paid for when you create an RDS instance. This billing method is suitable to a long-term RDS instance, which is cheaper than a Pay-As-You-Go instance. Additionally, a longer duration of purchase indicates a higher discount rate.
    **Note:** You can change the billing method of an RDS instance from Pay-As-You-Go to Subscription but not from Subscription to Pay-As-You-Go.

7.  Set the parameters of the new RDS instance.

    |Parameter|Description|
    |---------|-----------|
    |**Restore Mode**|     -   **By Time**: You can select any time point within the specified log backup retention period. For more information about how to view or change the log backup retention period, see [Back up the data of an RDS for MySQL instance](intl.en-US/RDS for MySQL User Guide/Database backup/Back up the data of an RDS for MySQL instance.md#).
    -   **By Backup Set**
 **Note:** The **By Time** option is available only when the log backup function is enabled.

 |
    |**Zone**| A zone is a physical area within a region. Different zones in the same region are basically the same.

 You can create an RDS instance in the same or different zone from the corresponding ECS instance. **Note:** The new RDS instance must be located in the same region as the original RDS instance.

 |
    |**CPU and Memory**| The type \(including the CPU and memory specifications\) of the new RDS instance. The CPU, memory, and storage capacity specifications of the new RDS instance must be higher than hose of the original RDS instance. Otherwise, the data restoration may take a long time.

 Each instance type supports a specific number of CPU cores, memory size, maximum number of connections, and maximum IOPS. For more information, see [Instance type list](../intl.en-US/Product Introduction/Instance types/Instance type list.md#).

 RDS instances fall into the following three type families:

    -   **General-purpose instance**: A general-purpose instance owns dedicated memory and I/O resources, but shares CPU and storage resources with the other general-purpose instances on the same server.
    -   **Dedicated instance**: A dedicated instance owns dedicated CPU, memory, storage, and I/O resources.
    -   **Dedicated host**: A dedicated-host instance owns all the CPU, memory, storage, and I/O resources on the server where it is located.
 For example, **8 Cores, 32 GB** indicates a general-purpose instance, **8 Cores, 32 GB \(Dedicated Instance\)** indicates a dedicated instance, and 30 Cores, 220GB \(Dedicated Host\)**30 Cores, 220 GB \(Dedicated Host\)** indicates a dedicated-host instance.|
    |**Capacity**|Used for storing data, system files, binlog files, and transaction files.|
    |**Network Type**|     -   **Classic Network**: a classic network.
    -   **VPC** \(recommended\): A VPC is an isolated network environment that provides better security and performance than a classic network.
 |

8.  Optional. If the new RDS instance uses the Subscription billing method, set the **Duration** and **Quantity** parameters.
9.  Click **Buy Now**.
10. On the Order Confirmation page, select **Terms of Service, Service Level Agreement, and Terms of Use**, then click **Pay Now** to complete the payment.

## Verify data in the new RDS instance {#section_k2y_np4_ydb .section}

For more information, see [Connect to an RDS for MySQL instance](../intl.en-US/Quick Start for MySQL/Connect to an RDS for MySQL instance.md#).

## Migrate data to the original RDS instance {#section_jtd_v11_ydb .section}

After verifying the data in the new RDS instance, you can migrate the data to the original RDS instance.

Data migration refers to migrating data from one RDS instance \(the source RDS instance\) to another \(the destination RDS instance\). The data migration operation does not interrupt the source RDS instance.

**Precautions**

Do not perform DDL operations during the data migration. Otherwise, the data migration may fail.

**Procedure**

1.  Log on to the [DTS console](http://dts.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the upper-right corner, click **Create Migration Task**.
4.  Enter the migration task name, source database information, and destination database information.

    Parameter description:

    -   **Task Name**: By default, DTS automatically generates a name for each migration task. You can change the name as needed.
    -   **Source Database** 

        -   **Instance Type**: Select **RDS Instance**.
        -   **Instance Region**: Select the region where the new RDS instance is located.
        -   **RDS Instance ID**: Select the ID of the new RDS instance.
        -   **Database Account**: Enter the username of the account for the new RDS instance.
        -   **Database Password**: Enter the password of the account for the new RDS instance.
        -   **Connection**: Select **Non-encrypted**. If the new RDS instance supports [SSL encryption](intl.en-US/RDS for MySQL User Guide/Data security/Configure SSL encryption.md#) and has SSL encryption enabled, then you must select **SSL-encrypted**.
        **Note:** The values of the **Instance Type** and **RDS Instance ID** parameters determine which of the other parameters are displayed.

    -   **Destination Database** 

        -   **Instance Type**: Select **RDS Instance**.
        -   **Instance Region**: Select the region where the original RDS instance is located.
        -   **RDS Instance ID**: Select the ID of the original RDS instance.
        -   **Database Account**: Enter the username of the account for the original RDS instance.
        -   **Database Password**: Enter the password of the account for the original RDS instance.
        -   **Connection**: Select **Non-encrypted**. If the original RDS supports [SSL encryption](intl.en-US/RDS for MySQL User Guide/Data security/Configure SSL encryption.md#) and has SSL encryption enabled, then you must select**SSL-encrypted**.
        **Note:** The values of the **Instance Type** and **RDS Instance ID** parameters determine which of the other parameters are displayed.

    ![DTS设置迁移任务参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41850/156697279839851_en-US.png)

5.  Click **Set Whitelist and Next**.
6.  Select **Schema Migration** and **Full Data Migration** next to **Migration Types**.
7.  In the **Available** section, select the objects you want to migrate. Then click **\>** to move the selected objects to the **Selected** section.

    **Note:** DTS checks for objects that have the same name. If the destination RDS instance has an object whose name is the same as the name of an object to be migrated, the data migration fails.

    In such case, take one of the following two operations:

    -   In the **Selected** section, move the pointer over the object whose name you want to change, click **Edit**, and in the displayed dialog box enter the new object name.
    -   Rename the object in the destination RDS instance.
    ![DTS选择迁移类型和迁移对象](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7959/15669727993949_en-US.png)

8.  Click **Precheck**.
9.  Optional. If the migration task fails the precheck, click ![查看预检结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41850/156697279940361_en-US.png) next to the check item whose **Result** is **Failed**, and resolve the problem according to the failure information.

    ![查看预检结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7959/15669727993951_en-US.png)

10. On the page that displays migration tasks, select the migration task you created, then click **Start**.

    ![DTS启动迁移任务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7959/15669728033952_en-US.png)

11. When the migration task passes the precheck, click **Next**.
12. In the Confirm Settings dialog box, confirm the configuration, select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**, and click **Buy and Start**.

