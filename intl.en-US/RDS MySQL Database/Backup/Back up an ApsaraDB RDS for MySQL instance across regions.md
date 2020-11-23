# Back up an ApsaraDB RDS for MySQL instance across regions

This topic describes how to back up an ApsaraDB RDS for MySQL instance by using the cross-region backup function. This function automatically replicates the backup files of the RDS instance from the source region to a specified destination region. You can use the backup files in the destination region to manage and restore the RDS instance. In this case, the RDS instance is known as the original RDS instance.

The original RDS instance runs one of the following MySQL versions and RDS editions:

-   MySQL 8.0 on RDS High-availability Edition \(with local SSDs\)
-   MySQL 5.7 on RDS High-availability Edition \(with local SSDs\)
-   MySQL 5.6

**Note:** For more information about how to back up an ApsaraDB RDS for SQL Server instance across regions, see [Back up an ApsaraDB RDS for SQL Server instance across regions]().

The cross-region backup function is different from the default backup function. For more information about the default backup function, see [Back up an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md).

You can use a cross-region backup file of the original RDS instance to restore data to an existing or new RDS instance that resides in the destination region. For more information, see [Restore the data of an ApsaraDB RDS for MySQL instance across regions](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance across regions.md).

## Differences between cross-region and default backups

-   The cross-region backup function is disabled by default and must be manually enabled. The default backup function is enabled by default.
-   Cross-region backup files are stored in the destination region. Default backup files are stored in the source region.
-   Cross-region backup files can be restored to an existing or new RDS instance in the source or destination region. Default backup files can be restored to the original RDS instance or to a new RDS instance in the source region.
-   Cross-region backup files are independent of the original RDS instance. If you release the original RDS instance, cross-region backup files are still retained based on the specified retention period. However, default backup files are retained for up to seven days.

## Billing

The fees for the cross-region backup function include the following two parts:

-   Remote storage: USD 0.0002/GB/hour.
-   Traffic consumption: For more information, see[Billing methods and billing items](https://www.alibabacloud.com/help/zh/doc-detail/70005.htm#h2-rds-2).

## Precautions

-   Cross-region backup files can be restored to the source or destination region. However, if transparent data encryption \(TDE\) is enabled, you can restore these files only to the source region. For more information, see [Configure TDE for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md).
-   Cross-region backups do not affect default backups. These two types of backups can be used in combinations.
-   After a default backup is completed, the original RDS instance triggers a cross-region backup. This allows ApsaraDB RDS to dump the generated default backup files to the destination region.
-   After the cross-region backup function is enabled, the original RDS instance triggers a data backup to its secondary RDS instance. This applies if no valid data backup files are generated over the last 24 hours.
-   After the cross-region log backup function is enabled, the original RDS instance checks for valid log backup files that are generated over the last 24 hours.
    -   If continuous log backup files are generated following a valid log backup file, the original RDS instance dumps these log backup files.
    -   If no continuous log backup files are generated following a valid log backup file, the original RDS instance triggers a data backup to its secondary RDS instance.
-   Cross-region backups are not supported in some regions due to network reasons. The following table lists the regions that support the cross-region backup function.

    |Source region|Destination region|
    |-------------|------------------|
    |China \(Hangzhou\)|China \(Shanghai\), China \(Qingdao\), China \(Shenzhen\)|
    |China \(Shanghai\)|China \(Hangzhou\), China \(Qingdao\), China \(Shenzhen\)|
    |China \(Qingdao\)|China \(Hangzhou\), China \(Shanghai\), China \(Shenzhen\)|
    |China \(Beijing\)|China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Shenzhen\)|
    |China \(Shenzhen\)|China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\)|
    |China \(Hong Kong\)|China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Shenzhen\)|


## Enable the cross-region backup function for an RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and in the Actions column choose **More** \> **Cross-region Backup Settings**.

    **Note:**

    -   You can also click **Backup and Restoration** in the left-side navigation pane and then click **Edit** on the **Cross-region Backup** tab.
    -   If the **Cross-region Backup Settings** option or the Cross-region Backup tab does not appear, make sure that your RDS instance meets the requirements that are specified in the "Prerequisites" section of this topic.
4.  Configure the following parameters.

    ![Cross-region Backup Settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1064204061/p51473.png)

    |Parameter|Description|
    |---------|-----------|
    |**Cross-region Backup Status**|Specifies whether to enable the cross-region backup function. Select **Enable**.|
    |**Backup Region**|The destination region to which cross-region backup files are stored. Your RDS instance automatically replicates backup files to the destination region.|
    |**Cross-region Retention Period**|The number of days for which you want to retain cross-region backup files. Valid values: 7 to 1825. Unit: days. The longest cross-region backup retention period spans five years. **Note:** After your RDS instance expires or is released, its cross-region backup files are still retained based on the specified retention period. You can log on to the ApsaraDB RDS console and click Cross-region Backup in the left-side navigation pane to view the retained cross-region backup files. |
    |**Cross-region Log Backup Status:**|Specifies whether to enable the cross-region log backup function. After you enable this function, your RDS instance replicates log backup files to Object Storage Service \(OSS\) buckets in the destination region.|

5.  Click **OK**.


## Enable the cross-region backup function for multiple RDS instances at a time

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Cross-region Backup**.

3.  Click the **Pending Instances** tab.

4.  Select the RDS instances and below the instance list click **Backup Settings**.

    **Note:** You can also click **Settings** in the Cross-region Backup Settings column of a single RDS instance to enable the cross-region backup function only for that RDS instance.

    ![Pending Instances tab](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8530359951/p101227.png)

5.  Configure the following parameters.

    ![Enable the cross-region backup function for multiple RDS instances at a time](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8530359951/p101226.png)

    |Parameter|Description|
    |---------|-----------|
    |**Cross-region Backup Status**|Specifies whether to enable the cross-region backup function. Select **Enable**.|
    |**Backup Region**|The destination region to which cross-region backup files are stored. Your RDS instance automatically replicates backup files to the destination region.|
    |**Cross-region Retention Period**|The number of days for which you want to retain cross-region backup files. Valid values: 7 to 1825. Unit: days. The longest cross-region backup retention period spans five years. **Note:** After your RDS instance expires or is released, its cross-region backup files are still retained based on the specified retention period. You can log on to the ApsaraDB RDS console and click Cross-region Backup in the left-side navigation pane to view the retained cross-region backup files. |
    |**Cross-region Log Backup Status:**|Specifies whether to enable the cross-region log backup function. After you enable this function, your RDS instance replicates log backup files to Object Storage Service \(OSS\) buckets in the destination region.|

6.  Click **OK**.


## Modify the cross-region backup settings of an RDS instance

A menu item named Cross-region Backup is added to the homepage of the ApsaraDB RDS console. You can modify the cross-region backup settings of an RDS instance even after the RDS instance is released.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Cross-region Backup**.

3.  Find the RDS instance and in the Cross-region Backup Settings column click **Settings**. Then, you can modify the cross-region backup settings of the RDS instance based on your business requirements.

    **Note:** If the RDS instance is released, you can modify only the cross-region backup retention period.


## Disable the cross-region backup function for an RDS instance

Perform the following steps:

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Cross-region Backup**.

3.  Find the RDS instance and in the Cross-region Backup Settings column click **Settings**.

4.  Set the **Cross-region Backup Status** parameter to **Disabled** and the **Cross-region Retention Period** parameter to **7** days.

    **Note:** After the cross-region backup function is disabled, no new cross-region backup files are generated. However, the existing cross-region backup files are still retained for at least seven days. You must set the cross-region backup retention period to seven days. After the retention period elapses, all of the existing cross-region backup files are deleted. You are no longer charged for the storage of these backup files.

5.  Click **OK**.


## View the cross-region backup settings of an RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Cross-region Backup**. Then, you can view the cross-region backup settings of all RDS instances.

    ![Cross-region Backup page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8530359951/p62686.png)


## FAQ

Why am I still charged after I disable the cross-region backup function for my RDS instance?

After you disable the cross-region backup function for your RDS instance, you must still pay for the storage of the existing cross-region backup files within the specified retention period. This applies even if the function no longer consumes traffic and your RDS instance no longer generates new cross-region backup files. The existing cross-region backup files are retained for at least seven days. You can set the retention period to seven days. For more information, see the "[Modify the cross-region backup settings of an RDS instance](#section_ryt_44l_xhb)" section of this topic. After the retention period elapses, all of the existing cross-region backup files are deleted. You are no longer charged for the storage of these backup files.

## Related operations

|Operation|Description|
|---------|-----------|
|[Check whether an ApsaraDB for RDS instance can be restored across regions](/intl.en-US/API Reference/Cross-region backup and restoration/Check whether an ApsaraDB for RDS instance can be restored across regions.md)|Checks whether an ApsaraDB RDS instance has a cross-region backup set that can be used to restore data.|
|[Create disaster recovery instance](/intl.en-US/API Reference/Cross-region backup and restoration/Create disaster recovery instance.md)|Restores the data of an ApsaraDB RDS instance to a new RDS instance that resides in a region different from the region of the original RDS instance.|
|[Modify cross-region backup settings](/intl.en-US/API Reference/Cross-region backup and restoration/Modify cross-region backup settings.md)|Modifies the cross-region backup settings of an ApsaraDB for RDS instance.|
|[Query cross-region backup settings](/intl.en-US/API Reference/Cross-region backup and restoration/Query cross-region backup settings.md)|Queries the cross-region backup settings of an ApsaraDB RDS instance.|
|[Query cross-region data backup files](/intl.en-US/API Reference/Cross-region backup and restoration/Query cross-region data backup files.md)|Queries the cross-region data backup files of an ApsaraDB RDS instance.|
|[Query cross-region log backup files](/intl.en-US/API Reference/Cross-region backup and restoration/Query cross-region log backup files.md)|Queries the cross-region log backup files of an ApsaraDB RDS instance.|
|[Query regions that support cross-region backup](/intl.en-US/API Reference/Cross-region backup and restoration/Query regions that support cross-region backup.md)|Queries the destination regions that are available to store cross-region backup files from a source region.|
|[Query the time range to which you can restore data by using a cross-region backup set](/intl.en-US/API Reference/Cross-region backup and restoration/Query the time range to which you can restore data by using a cross-region backup
         set.md)|Queries the restorable time range that is supported by a cross-region backup file.|
|[Query ApsaraDB for RDS instances on which cross-region backup is enabled](/intl.en-US/API Reference/Cross-region backup and restoration/Query ApsaraDB for RDS instances on which cross-region backup is enabled.md)|Queries the ApsaraDB RDS instances for which the cross-region backup function is enabled in a region and the cross-region backup settings of these instances.|

