# Restore MariaDB data {#concept_rxd_d5g_2fb .concept}

You can restore data of RDS for MariaDB TX as follows:

-   Restore data of an RDS instance to a new RDS instance \(referred to as a clone instance\).
-   Verify the data on the clone instance.
-   Migrate the data you need from the clone instance to the original instance.

**Note:** 

-   The clone instance has the same whitelist, backup settings, and parameter settings as the original instance.
-   RDS for MariaDB TX does not allow you to restore data of an instance directly to the instance itself to overwrite the existing data.

## Pricing {#section_uh5_4bq_w2b .section}

The costs are the same as purchasing a new instance. For details, see [Pricing](https://www.alibabacloud.com/product/apsaradb-for-rds#pricing).

## Prerequisites {#section_o5q_1p4_ydb .section}

-   The original instance is running properly and not locked.

-   The original instance is not undergoing a migration task.

-   To restore data to a point in time, ensure that log backup has been enabled.

-   To restore data from a backup set, ensure that at least one backup set has been generated.


## Attention {#section_qbn_ygz_xfb .section}

-   If the data volume is large, the restoration may take a long time.
-   If no resource is available when you create a clone instance, try again by choosing a different zone in the same region.

## Restore data to a new RDS instance \(clone instance\) {#section_gff_jtz_bhb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the instance is located.

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17685/155257498840804_en-US.png)

3.  Click the instance ID.
4.  In the left-side navigation pane, choose Backup and Recovery.
5.  In the upper-right corner, click **Restore Database**.
6.  In the displayed window, select a payment method:

    -   **Pay-As-You-Go**: indicates post payment. The system deducts an hourly fee from your account balance every hour. If you plan to use the instance for a short term, this method is cost-effective because you can release the instance after using it.
    -   **Subscription**: indicates prepayment. You need to pay for the instance when creating it. If you plan to use the instance for a month or more, this method is more cost-effective than Pay-As-You-Go. The longer the subscription is, the higher the discount.
    **Note:** Pay-As-You-Go instances can be changed to Subscription instances, but Subscription instances cannot be changed to Pay-As-You-Go instances.

7.  Set the instance parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Restore Type**|     -   **By Time**: You can restore data to any point in time within the log backup retention period. To view or modify the log backup retention period, see [Back up RDS data](intl.en-US/User Guide/Backup/Back up RDS data.md).
    -   **By Backup ID**
 **Note:** **By Time** is displayed only if log backup is enabled.

 |
    |**Edition**|RDS for MariaDB TX currently supports the High-availability Edition, which consists of a master node and a slave node. This edition applies to over 80% of application scenarios. For more information, see [Product series overview](../../../../../intl.en-US/Product Introduction/Product series/Product series overview.md).|
    |**Zone**|A zone is an independent area within a region. Different zones within the same region are basically the same.

You can deploy your RDS and ECS instances in the same zone or in different zones.Certain regions allow you deploy a High-availability instance across zones, such as **Zone F + Zone G**. This indicates that the master and slave nodes of the High-availability instance are in two different zones so that the disaster recovery capability is higher. This does not incur extra costs.

**Note:** The region of the clone instance is the same as that of the original instance.

|
    |**Type**|It is recommended that the specifications and storage of the clone instance be equal to higher than those of the original instance; otherwise, the data restoration may take a long time.

Each type of specification provides a specific number of CPU cores, memory, maximum number of connections, and maximum IOPS. For details, see [Instance type list](../../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md).

RDS provides the following instance type families:

    -   General: A general instance has its own memory and I/O resources, and shares CPU and storage resources with other general instances on the same server.
    -   Dedicated: A dedicated instance has it own CPU, memory, storage, and I/O resources.
 For example, **8 Cores, 32GB** is a general instance. **8 Cores, 32GB \(Dedicated\)** is a dedicated instance.|
    |**Capacity**|The capacity is used for storing data, system files, binlog files, and transaction files.|
    |**Network Type**|RDS for MariaDB TX supports the **VPC** \(short for Virtual Private Cloud\). A VPC is an isolated network and provides higher security and performance than the traditional classic network.|

8.  Set the duration \(for Subscription instances only\) and quantity of the instances to be created.
9.  Click **Buy Now**.
10. Review order information, select **Product Terms of Service and Service Level Notice and Terms of Use**, and complete the payment.

## Log on to the clone instance and verify the data {#section_k2y_np4_ydb .section}

For information about how to log on to an instance, see [Connect to an instance](../../../../../intl.en-US/Quick Start for MariaDB TX/Connect to an instance.md).

## Migrate data to the original instance {#section_jtd_v11_ydb .section}

After verifying the data on the clone instance, if necessary, you can migrate the data you need from the clone instance to the original instance.

Data migration indicates copying data from one instance \(source instance\) to another \(target instance\) and does not affect the source instance.

**Attention**

DDL operations are not allowed during the migration; otherwise, the migration may fail.

**Procedure**

1.  Log on to the [DTS console](http://dts.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Data Migration**.
3.  Click **Create Migration Task**.
4.  Enter the task name, source database information, and target database information.

    -   Task name: A default task name is generated automatically . It is recommended that you set a meaningful name so that the task can be identified easily.

    -   Source database information:

        -   **Instance Type**: Select **RDS Instance**.
        -   **Instance Region**: Select the region where the clone instance is located.
        -   **RDS Instance ID**: Select the ID of the clone instance.

            **Note:** This parameter is displayed only if you have selected **RDS Instance** for **Instance Type**.

        -   **Database Account**: Enter the account name of the clone instance.
        -   **Database Password**: Enter the password of the preceding account.
        -   **Connection method**: Generally, select **Non-encrypted connection**. If [SSL encryption](intl.en-US/User Guide/Security/Set SSL encryption.md#) has been enabled for the instance, select **SSL secure connection**.

            **Note:** This parameter is displayed only if you have selected certain RDS instances.

    -   Target database information:

        -   **Instance Type**: Select **RDS Instance**.
        -   **Instance Region**: Select the region where the original instance is located.
        -   **RDS Instance ID**: Select the ID of the original instance.

            **Note:** This parameter is displayed only if you have selected **RDS Instance** for **Instance Type**.

        -   **Database Account**: Enter the account name of the original instance.
        -   **Database Password**: Enter the password of the preceding account.
        -   **Connection method**: Generally, select **Non-encrypted connection**. If [SSL encryption](intl.en-US/User Guide/Security/Set SSL encryption.md#) has been enabled for the instance, select **SSL secure connection**.

            **Note:** This parameter is displayed only if you have selected certain RDS instances.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7967/155257498840810_en-US.png)

5.  Click **Authorized Whitelist and Enter Into Next Step**.
6.  Select **Migrate object structure** and **Migrate existing data**.
7.  In the left pane, select objects and click **\>** to add them to the right.

    **Note:** DTS will perform a data check. If an object in the target instance has the same name as an object to be migrated, the migration fails.

    If an object in the target instance has the same name as an object to be migrated, do either of the following:

    -   In the right pane, place your mouse over an object and click **Edit** to modify the object name.
    -   Rename the object in the target instance.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7967/155257498840814_en-US.png)

8.  Click **Pre-check and Start**.
    -   If the pre-check succeeds, go to step 11.
    -   If the pre-check fails, go to step 9.
9.  If the pre-check fails, click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22161/155257498840827_en-US.png) next to the failed item to view details.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7959/15525749883951_en-US.png)

10. After fixing all problems, select the migration task in the migration task list and click **Start**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7967/155257498940816_en-US.png)

11. If the pre-check succeeds, click **Next**.
12. On the Confirm Purchase Configuration dialog box, confirm the configuration, select **Service Terms of Data Transmission \(Pay-As-You-Go\)**, and click **Buy and Start Now**.

