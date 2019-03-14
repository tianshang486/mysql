# Restore SQL Server Data {#concept_o52_hlx_52b .concept}

You can restore data of RDS for SQL Server in any of the following ways.

-   [Restore to an existing RDS instance](#)
-   [Restore to new RDS instance](#)
-   [Restore to a temporary RDS instance](#)

## Attention {#section_qbn_ygz_xfb .section}

If the data volume is large, the restoration may take a long time.

## Restore data to an existing RDS instance {#section_huifu .section}

You can restore all or part of the databases in your instance to an existing RDS instance.

**Applicable scope**

This method applies to RDS for SQL Server 2016 or 2012 instances.

**Procedure**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the instance is located.

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17685/155257485240804_en-US.png)

3.  Click the instance ID.
4.  In the left-side navigation pane, choose Backup and Recovery.
5.  In the upper-right corner of the page, click **Restore**.
6.  \(This step is for high-availability series only.\) Select**Restore to Existing Instance** and click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17685/155257485210029_en-US.png)

7.  Set the following parameters, and then click**OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17685/155257485210031_en-US.png)

    **Note:** If the existing instance already has a database that has the same name as the database to be restored, you need to modify New Name.

    |Parameter|Description|
    |---------|-----------|
    |**Restore Method**|To restore data to an existing instance, select **By Backup Set**.|
    |**Backup Set**|Select the backup set to restore.By default, the system displays all full backup sets under the current instance.

|
    |**Instance**|Select the instance to which the backup set will be restored.By default, the system displays the current instance and all instances that belong to the current Alibaba account and current region and have the same database version as the current instance.

**Note:** If many instances are displayed, you can use the search box.

|
    |**Databases to restore**|     1.  Select the database to restore. All databases in the backup set are displayed and selected by default.
        -   To restore data of the entire instance, retain the default selection \(All databases are selected\).
        -   To restore certain databases, select only these databases.
    2.  Set the database names that are displayed after the databases are restored. By default, the database names in the backup set are used.

**Note:** The database names cannot be the same as the existing database names in the target instance.

 |


## Restore to a new RDS instance {#section_l2n_r4x_52b .section}

This function is also called "clone instance", used to restore the historical backup of the instance to a new instance. You can restore data by time or backup set. When restoring by backup set, you can restore all or part of the databases in the backup set.

**Pricing**

The costs are the same as purchasing a new instance. For details, see [Pricing](https://www.alibabacloud.com/product/apsaradb-for-rds#pricing).

**Applicable scope**

This method applies to the following instances:

-   SQL Server 2017 Cluster series
-   SQL Server 2012/2016 Enterprise Edition High-Availability series
-   SQL Server 2012/2016 Standard Edition High-Availability series

**Procedure**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the instance is located.

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17685/155257485240804_en-US.png)

3.  Click the instance ID.
4.  In the left-side navigation pane, choose Backup and Recovery.
5.  In the upper-right corner of the page, click **Restore**.
6.  Select **Restore to New Instance** and click **OK**.
7.  In the displayed window, select a payment method:

    -   **Pay-As-You-Go**: indicates post payment. The system deducts an hourly fee from your account balance every hour. If you plan to use the instance for a short term, this method is cost-effective because you can release the instance after using it.
    -   **Subscription**: indicates prepayment. You need to pay for the instance when creating it. If you plan to use the instance for a month or more, this method is more cost-effective than Pay-As-You-Go. The longer the subscription is, the higher the discount.
    **Note:** Pay-As-You-Go instances can be changed to Subscription instances, but Subscription instances cannot be changed to Pay-As-You-Go instances.

8.  Set the instance parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Restore Type**|     -   **By Time**: You can restore data to any point in time within the log backup retention period. To view or modify the log backup retention period, see [Back up RDS data](intl.en-US/User Guide/Backup/Back up RDS data.md).
    -   **By Backup ID**
 **Note:** **By Time** is displayed only if log backup is enabled.

 |
    |**Database**|     -   **All**: Restore all databases in the backup set.
    -   **Part**: Restore part of the databases in the backup set.
 |
    |**Edition**|     -   High-availability: consists of a master node and a slave node. This edition applies to over 80% of application scenarios.
    -   AlwaysOn \(Cluster\) Edition: provides one master node, one slave node, and up to seven read-only nodes that horizontally scale read capabilities. For more information, see [Cluster Edition \(AlwaysOn Edition\)](../../../../../intl.en-US/Product Introduction/Product series/Cluster Edition (AlwaysOn Edition).md).
 |
    |**Zone**|A zone is an independent area within a region. Different zones within the same region are basically the same.

You can deploy your RDS and ECS instances in the same zone or in different zones.**Note:** The region of the clone instance is the same as that of the original instance.

|
    |**Type**|It is recommended that the specifications and storage of the clone instance be equal to higher than those of the original instance; otherwise, the data restoration may take a long time.

Each type of specification provides a specific number of CPU cores, memory, maximum number of connections, and maximum IOPS. For details, see [Instance type list](../../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md).

RDS provides the following instance type families:

    -   General: A general instance has its own memory and I/O resources, and shares CPU and storage resources with other general instances on the same server.
    -   Dedicated: A dedicated instance has it own CPU, memory, storage, and I/O resources.
 For example, **8 Cores, 32GB** is a general instance. **8 Cores, 32GB \(Dedicated\)** is a dedicated instance.|
    |**Capacity**|The capacity is used for storage data, system files, and transaction files.|
    |**Network Type**|     -   **Classic Network**: Traditional network type.
    -   **VPC** \(recommended\): VPC is short for Virtual Private Cloud. A VPC is an isolated network and provides higher security and performance than the traditional classic network.
 |

9.  Click **Buy Now**.
10. Review order information, select **Product Terms of Service and Service Level Notice and Terms of Use**, and complete the payment.

## Restore data to a temporary instance {#section_ejq_2yz_52b .section}

This method applies to the following instances:

-   SQL Server 2012 Enterprise Edition Basic series
-   SQL Server 2012/2016 Web Edition Basic series
-   SQL Server 2008 R2

For detailed operations, see[Recover data to a temporary instance \(RDS for SQL Server\)](intl.en-US/User Guide/Recovery/Recover data to a temporary instance (RDS for SQL Server).md).

