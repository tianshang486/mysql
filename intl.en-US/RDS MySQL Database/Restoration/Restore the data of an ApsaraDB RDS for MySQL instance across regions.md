# Restore the data of an ApsaraDB RDS for MySQL instance across regions

This topic describes how to restore the data of an ApsaraDB RDS for MySQL instance across regions. You can restore data from a cross-region backup file to a specified destination RDS instance. This requires that you have backed up your RDS instance across regions. The destination RDS instance can be the original RDS instance. The destination RDS instance can also be a new or existing RDS instance that resides in the region to which the cross-region backup file is stored.

A cross-region backup is created. For more information, see [Back up an ApsaraDB RDS for MySQL instance across regions](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance across regions.md).

**Note:** For more information about how to restore the data of an ApsaraDB RDS for SQL Server instance cross regions, see [Restore the data of an ApsaraDB RDS for SQL Server instance across regions]().

## Precautions

Before you can connect to the new RDS instance to which you want to restore data, you may need to reset the password of the logged-on account. This applies if the original RDS instance has the database proxy feature enabled and does not have a privileged account.

## Restore data to a new RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Cross-region Backup**.

3.  Find the original RDS instance and click its ID.

    ![Cross-region restoration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5630359951/p48557.png)

4.  On the **Data Backup** tab, find the backup set that you want to use, and click **Restore** in the Actions column.

    ![Select a backup](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5630359951/p48558.png)

5.  Select **Restore to New Instance** and click **OK**.

6.  On the **Restore Database** page, click the **Subscription** or **Pay-As-You-Go** tab and configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Restore Mode**|    -   **By Backup Set**: allows you to restore data from a backup set.
    -   **By Time**: allows you to restore data to a point in time. The point in time must be within the specified log backup retention period. |
    |**Backup Set**|The backup set from which you want to restore data. This parameter appears only when you set **Restore Mode** to **By Backup Set**.|
    |**Restore Point**|The point in time to which you want to restore data. This parameter appears only when you set **Restore Mode** to **By Time**. **Note:** Both local and cross-region log backups can be used to restore data to a point in time. |
    |**Region**|The region to which the new RDS instance belongs.|
    |**Zone**|The zone where the new RDS instance resides. Each zone is an independent physical location within a region. Zones in the same region provide the same services. You can create the new RDS instance and the ECS instance to which you want to connect in the same zone or in different zones.|
    |**CPU and Memory**|The specifications of the new RDS instance. Each instance type supports a specific number of CPU cores, memory capacity, maximum number of connections, and maximum input/output operations per second \(IOPS\). For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).|
    |**Capacity**|The storage capacity that the new RDS instance has available to store data files, system files, binary log files, and transaction files.|
    |**Network Type**|    -   **Classic Network**: the traditional type of network.
    -   **VPC**: the recommended type of network. A virtual private cloud \(VPC\) is an isolated virtual network that provides higher security and better performance than the classic network. If you select the VPC network type, you must also select a VSwitch that is associated with the specified VPC. |

    **Note:** The settings of some parameters cannot be modified. These parameters include Database Engine, Version, and Edition. The same settings of these parameters must be specified for the original and new RDS instances.

7.  Specify the **Duration** and **Quantity** parameters. Then, click **Buy Now**. You must specify the Duration parameter only when the new RDS instance uses the subscription billing method.

8.  On the **Order Confirmation** page, read and select Terms of Service, Service Level Agreement, and Terms of Use. Then, click Pay Now and complete the payment.


## Restore data to an existing RDS instance

**Note:** Make sure that the single-database and -table backup function is enabled and at least one single-database and -table backup is created on the existing RDS instance.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Cross-region Backup**.

3.  Find the original RDS instance and click its ID.

    ![Cross-region restoration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5630359951/p48557.png)

4.  On the **Data Backup** tab, find the backup set that you want to use, and click **Restore** in the Actions column.

    ![Select a backup](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5630359951/p48558.png)

5.  Select **Restore to Existing Instance** and click **OK**.

6.  Configure the following parameters.

    ![Restore to Existing Instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5630359951/p101239.png)

    |Parameter|Description|
    |---------|-----------|
    |**Restore Method**|    -   **By Backup Set**: allows you to restore data from a backup set.
    -   **By Time**: allows you to restore data to a point in time. The point in time must be within the specified log backup retention period. |
    |**Region**|The region to which the existing RDS instance belongs.|
    |**Destination Instance**|The existing RDS instance to which you want to restore data.|
    |**Databases and Tables to Restore**|Select the databases and tables that you want to restore.|
    |**Selected Databases and Tables**|The new names of the databases and tables on the existing RDS instance. If you do not specify the new names, the `_backup` suffix is added to the original names.|

7.  Click **OK**.


## References

After you create an RDS instance, you must configure IP address whitelists or security groups and create accounts. For more information, see [Control access to an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.md) and [Create accounts and databases for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create accounts and databases for an ApsaraDB RDS for MySQL instance.md). If you want to connect to the RDS instance over the Internet, you must also apply for a public endpoint. For more information, see [Apply for or release a public endpoint for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Apply for or release a public endpoint for an ApsaraDB RDS for MySQL instance.md). After you complete these operations, you can connect to the RDS instance. For more information, see [Connect to an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Connect to an ApsaraDB RDS for MySQL instance.md).

## Related operations

|Operation|Description|
|---------|-----------|
|[Check whether an ApsaraDB for RDS instance can be restored across regions](/intl.en-US/API Reference/Cross-region backup and restoration/Check whether an ApsaraDB for RDS instance can be restored across regions.md)|Checks whether an ApsaraDB RDS instance has a cross-region backup set that can be used to restore data.|
|[Create disaster recovery instance](/intl.en-US/API Reference/Cross-region backup and restoration/Create disaster recovery instance.md)|Restores the data of an ApsaraDB RDS instance to a new RDS instance that resides in a region different from the region of the original RDS instance.|
|[Modify cross-region backup settings](/intl.en-US/API Reference/Cross-region backup and restoration/Modify cross-region backup settings.md)|Modifies the cross-region backup settings of an ApsaraDB RDS instance.|
|[Query cross-region backup settings](/intl.en-US/API Reference/Cross-region backup and restoration/Query cross-region backup settings.md)|Queries the cross-region backup settings of an ApsaraDB RDS instance.|
|[Query cross-region data backup files](/intl.en-US/API Reference/Cross-region backup and restoration/Query cross-region data backup files.md)|Queries the cross-region data backup files of an ApsaraDB RDS instance.|
|[Query cross-region log backup files](/intl.en-US/API Reference/Cross-region backup and restoration/Query cross-region log backup files.md)|Queries the cross-region log backup files of an ApsaraDB RDS instance.|
|[Query regions that support cross-region backup](/intl.en-US/API Reference/Cross-region backup and restoration/Query regions that support cross-region backup.md)|Queries the destination regions that are available to store cross-region backup files from a source region.|
|[Query the time range to which you can restore data by using a cross-region backup set](/intl.en-US/API Reference/Cross-region backup and restoration/Query the time range to which you can restore data by using a cross-region backup
         set.md)|Queries the restorable time range that is supported by a cross-region backup file.|
|[Query ApsaraDB for RDS instances on which cross-region backup is enabled](/intl.en-US/API Reference/Cross-region backup and restoration/Query ApsaraDB for RDS instances on which cross-region backup is enabled.md)|Queries the ApsaraDB RDS instances for which the cross-region backup function is enabled in a region and the cross-region backup settings of these instances.|

