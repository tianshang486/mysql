# Restore the data of an ApsaraDB RDS for SQL Server instance across regions

This topic describes how to restore the data of an ApsaraDB RDS for SQL Server instance across regions. You can restore data from a cross-region backup file to a new RDS instance in the region to which the file is stored. This requires that you have backed up your RDS instance across regions.

A cross-region backup is created. For more information, see [t1986080.md\#]().

## Procedure

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
    |**Region**|The region to which the new RDS instance belongs.**Note:** You can select only the region to which the cross-region backup files of the original RDS instance are stored. |
    |**Zone**|The zone where the new RDS instance resides. Each zone is an independent physical location within a region. Zones in the same region provide the same services. You can create the new RDS instance and the ECS instance to which you want to connect in the same zone or in different zones.|
    |**CPU and Memory**|The specifications of the new RDS instance. Each instance type supports a specific number of CPU cores, memory capacity, maximum number of connections, and maximum input/output operations per second \(IOPS\). For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).|
    |**Capacity**|The storage capacity that the new RDS instance has available to store data files, system files, binary log files, and transaction files.|
    |**Network Type**|    -   **Classic Network**: the traditional type of network.
    -   **VPC**: the recommended type of network. A virtual private cloud \(VPC\) is an isolated virtual network that provides higher security and better performance than the classic network. If you select the VPC network type, you must also select a VSwitch that is associated with the specified VPC. |

    **Note:** The settings of some parameters cannot be modified. These parameters include Database Engine, Version, and Edition. The same settings of these parameters must be specified for the original and new RDS instances.

7.  Specify the **Duration** and **Quantity** parameters. Then, click **Buy Now**. You must specify the Duration parameter only when the new RDS instance uses the subscription billing method.

8.  On the **Order Confirmation** page, read and select Terms of Service, Service Level Agreement, and Terms of Use. Then, click Pay Now and complete the payment.


## References

After you create an RDS instance, you must configure IP address whitelists or security groups and create accounts. For more information, see [Configure a whitelist for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Configure a whitelist for an ApsaraDB RDS for SQL Server instance.md) and [Create an account for an RDS SQL Server instance](/intl.en-US/RDS SQL Server Database/Account/Create an account for an RDS SQL Server instancy.md). If you want to connect to the RDS instance over the Internet, you must also apply for a public endpoint. For more information, see [Apply for or release a public endpoint on an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Database connection/Apply for or release a public endpoint on an ApsaraDB RDS for SQL Server instance.md). After you complete these operations, you can connect to the RDS instance. For more information, see [Connect to an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Connect to an ApsaraDB RDS for SQL Server instance.md).

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

