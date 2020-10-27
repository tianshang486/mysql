# Restore the data of an ApsaraDB RDS for PostgreSQL instance

The topic describes how to restore the data of an ApsaraDB RDS for PostgreSQL instance to a new RDS instance.

The original RDS instance whose data you want to restore must meet the following requirements:

-   The original RDS instance is in the Running state and is not locked.
-   The original RDS instance does not have ongoing migration tasks.
-   If you want to restore data to a point in time, the log backup function is enabled for the original RDS instance.
-   If you want to restore data from a backup set, the original RDS instance has at least one backup set.

ApsaraDB RDS for PostgreSQL allows you to restore data from a backup set or to a point in time. The following procedure is used to restore data:

1.  Restore data to a new RDS instance. This process was known as instance cloning.
2.  Log on to the new RDS instance and verify the data.
3.  Migrate the data to the original RDS instance.

## Precautions

-   The new RDS instance must have the same IP address whitelist, backup, and parameter settings as the original RDS instance.
-   The data and account information of the new RDS instance must be the same as the data and account information that is indicated by the specified data or log backup file of the original RDS instance.

## Billing

The restoration fee is the same as the fee that is required to purchase a new RDS instance. For more information, visit the [ApsaraDB RDS](https://www.alibabacloud.com/product/apsaradb-for-rds#pricing) buy page.

## Restore data to a new RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Backup and Restoration**.

5.  In the upper-right corner of the page, click **Restore Database \(Previously Clone Database\)**.

6.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Billing Method**|    -   **Subscription**: A subscription instance is an instance that you can subscribe to for a specified period of time and pay for up front. Subscription billing is more cost-effective than pay-as-you-go billing. Therefore, we recommend that you select subscription billing with a longer commitment. You can receive larger discounts for longer subscription periods.
    -   **Pay-As-You-Go**: A pay-as-you-go instance is charged per hour based on your actual resource usage. We recommend that you select pay-as-you-go billing for short-term use. If you no longer need your pay-as-you-go instance, you can release it to reduce costs. |
    |**Restore Mode**|    -   **By Time**: allows you to restore data to a point in time within the specified log backup retention period. For more information about how to view or change the log backup retention period, see [Back up an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Backup/Back up an ApsaraDB RDS for PostgreSQL instance.md).
    -   **By Backup Set**: allows you to restore data from a specified backup set.
**Note:** The **By Time** option appears only when the log backup function is enabled. |
    |**Edition**|
    |**Zone of Primary Node** and Zone of Secondary Node|The zone to which the RDS instance belongs. A zone is an independent physical location within a region. The **Zone of Primary Node** parameter specifies the zone to which the primary RDS instance belongs. The **Zone of Secondary Node** parameter specifies the zone to which the secondary RDS instance belongs.

You can select the **Single-zone Deployment** or **Multi-zone Development** method.

    -   **Single-zone Deployment**: The **Zone of Primary Node** and the **Zone of Secondary Node** are the same.
    -   **Multi-zone Deployment**: The **Zone of Primary Node** and the **Zone of Secondary Node** are different. After you specify the **Zone of Primary Node**, the system automatically allocates the **Zone of Secondary Node**.
The multi-zone deployment method provides zone-level disaster recovery. We recommend that you select the multi-zone deployment method.

**Note:**

    -   After the RDS instance is created, you can view information about the RDS instance and its secondary RDS instance on the **Service Availability** page.
    -   If you select the RDS Basic Edition, the database system consists of only one RDS instance and supports only the single-zone deployment method.
![Select zones](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0650359951/p87361.png) |
    |**Instance Type**|
    |**Capacity**|

7.  Click **Next: Instance Configuration**.

8.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Network Type**|    -   **Classic Network**: the traditional type of network.
    -   **VPC**: A virtual private cloud \(VPC\) is an isolated network that provides higher security and better performance than the classic network. If you select the VPC network type, you must also specify the **VPC** and the **VSwitch of Primary Node**.
**Note:** The RDS instance must have the same network type as the ECS instance that you want to connect. If the RDS and ECS instances both have the VPC network type, they must also reside in the same VPC. Otherwise, the RDS and ECS instances cannot communicate over an internal network. |
    |**Resource Group**|The resource group to which the new RDS instance belongs.|

9.  Click **Next: Confirm Order**.

10. Confirm the settings in the **Parameters** section, specify the **Purchase Plan** and **Duration** parameters, read and select Terms of Service, and then click **Pay Now**. You must specify the Duration parameter only when the new RDS instance uses the subscription billing method.


## Log on to the new RDS instance and verify the data

For more information, see [Connect to an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Connect to an ApsaraDB RDS for PostgreSQL instance.md).

## Migrate data to the original RDS instance

After you verify the data on the new RDS instance, you can migrate the data from the new RDS instance back to the original RDS instance. For more information, see [Migrate data between RDS instances](https://www.alibabacloud.com/help/zh/doc-detail/26626.htm).

**Note:** The migration does not affect workloads on the original RDS instance.

