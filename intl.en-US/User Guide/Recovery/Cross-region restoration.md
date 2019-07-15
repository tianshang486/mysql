# Cross-region restoration {#concept_405831 .concept}

If you have completed [Cross-region backup](intl.en-US/User Guide/Backup/Cross-region backup.md#), you can restore data from the backup file to a new instance in the region where the original instance is located or the region where the cross-region backup file is stored.

**Note:** The cross-region backup data cannot be restored to the original instance.

## Procedure {#section_nph_85b_61u .section}

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com).
2.  In the left-side navigation pane, click **Cross-region Backup**.
3.  Find the instance and click its ID.

    ![Cross-region restoration](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/328507/156318102248557_en-US.png)

4.  On the Database Backup tab, find the target backup set and click **Restore** in the corresponding Actions column.

    ![Select backup](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/328507/156318102248558_en-US.png)

5.  On the Restore Database page, select **Subscription** or **Pay-As-You-Go** and configure the following parameters:

    |Parameter|Description|
    |---------|-----------|
    |**Restore Mode**|     -   By Backup Set: Restore the data of the backup set to a new instance.
    -   By Time: It can be set to any time point within the log backup retention period. All the data before this time point is restored to the new instance.
 |
    |**Backup Set**|When **Restore Mode** is set to **By Backup Set**, select the backup set that you want to restore.|
    |**Restore Point**|When **Restore Mode** is set to **By Time**, select the time point to restore data. **Note:** Local and cross-region logs can be restored to the specified time point.

 |
    |**Region**|Select a region for the new instance. You can only restore data to the new instance in the region where the original instance is located or the region where the backup file is located.|
    |**Zone**|Zones are independent physical areas located within a region. There are no differences between the zones. You can choose to create an RDS instance with an ECS instance in the same zone or in different zones.|
    |**Type**|Each instance type supports a specific number of CPU cores, memory, maximum number of connections, and maximum IOPS. For more information, see [Instance type list](../intl.en-US/Product Introduction/Instance types/Instance type list.md#).|
    |**Capacity**|The storage space of the instance, including the space for data, system files, binlog files, and transaction files.|
    |**Network Type**|     -   **Classic Network**: traditional network type.
    -   **VPC** \(recommended\): Virtual Private Cloud. A VPC is an isolated virtual network with higher security and performance than a classic network. You must select a VPC and a VSwitch in the VPC.
 |

6.  Specify **Duration** \(only applicable to subscription instances\) and **Quantity**, and click **Buy Now**.
7.  On the Confirm Order page, select the checkbox to agree the terms of service and complete the payment as prompted.

## Next {#section_zpa_ob4_q9u .section}

In the upper-left corner of the console, select the region where the instance is located to view the instance you just created.

After the instance is created, you must [configure a whitelist](intl.en-US/Quick Start for MySQL/Initial configuration/Configure a whitelist.md) and [create an account](intl.en-US/Quick Start for MySQL/Initial configuration/Create accounts and databases.md). If you are connecting through the external network, you must [apply for a public IP address](intl.en-US/Quick Start for MySQL/Initial configuration/Apply for an Internet address.md). You can then [connect to the instance](intl.en-US/Quick Start for MySQL/Connect to an instance.md).

