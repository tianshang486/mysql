# Back up an ApsaraDB RDS for MySQL instance

This topic describes how to back up an ApsaraDB RDS for MySQL instance. ApsaraDB RDS for MySQL supports automatic and manual backups. If the data of an RDS instance is lost or corrupted, you can restore the instance by using the backup files. If the instance is attached with local SSDs, you can retain the backup files for a specific period of time after you release the instance.

For more information about how to back up RDS instances that run other database engines, see the following topics:

-   [Back up an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance.md)
-   [Back up an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Backup/Back up an ApsaraDB RDS for PostgreSQL instance.md)
-   [Back up an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Backup/Back up an ApsaraDB RDS for PPAS instance.md)
-   [Automatically back up the data of an RDS MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Backup/Automatically back up the data of an RDS MariaDB instance.md)

**Note:** This topic describes the default backup feature, which stores backup files to the region where your RDS instance resides. You can also store backup files to a different region. For more information, see [Back up an ApsaraDB RDS for MySQL instance across regions](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance across regions.md).

## Features

-   If your RDS instance is attached with local SSDs, you can retain the backup files for a long period of time. In addition, you can specify a policy that is used to retain the backup files after you release the instance. This allows you to avoid data losses that are caused by unintentional operations. For more information, see [Modify the backup settings of an RDS instance that is attached with local SSDs](#section_f33_lk4_ydb).
-   If your RDS instance is attached with standard or enhanced SSDs, you can perform minute-level snapshot backups. For more information, see [Modify the backup settings of an RDS instance that uses standard or enhanced SSDs](#section_hwp_vv2_lct).

## Billing

Each RDS instance is allocated with a free quota for backup storage. If your backup storage usage exceeds the free quota, you are charged for the extra backup storage that you use. We recommend that you specify a proper backup cycle based on your business requirements to maximize the usage of the free backup storage. For more information about the free quota for backup storage, see [View the free quota for backup storage of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/View the free quota for backup storage of an ApsaraDB RDS for MySQL instance.md).

After the free quota is exhausted, your backup storage usage is charged based on the specified retention period. For more information about the pricing of regular backup files that are retained for 730 days or less,visit the [ApsaraDB RDS pricing page](https://www.alibabacloud.com/product/apsaradb-for-rds#pricing). For more information about the pricing of archived backup files that are retained for more than 730 days, see [Pricing of Long-Term Backup Files on Alibaba Cloud International Site](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/141303/cn_zh/1582881893267/%E5%9B%BD%E9%99%85%E7%AB%99%E9%95%BF%E6%9C%9F%E5%A4%87%E4%BB%BD%E6%94%B6%E8%B4%B9%E8%AF%B4%E6%98%8E.xls).

## Precautions

-   Your RDS instance can archive backup files only when the instance is attached with local SSDs.
-   Do not execute data definition language \(DDL\) statements during a backup. These statements trigger locks on tables, and the backup may fail as a result the locks.
-   We recommend that you back up your RDS instance during off-peak hours.
-   If your RDS instance has a large amount of data, backing up the instance may require a long time.
-   Backup files are retained based on the specified retention period. Before the retention period elapses, we recommend that you download the required backup files to your computer.
-   If the number of tables that are created on your RDS instance exceeds 50,000, you cannot restore individual databases or tables. For more information, see [Restore individual databases and tables of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md). If the number of tables exceeds 600,000, you cannot back up your RDS instance. In these cases, we recommend that you shard the databases on your RDS instance.

## Overview of data and log backups

|Data Backup|Log backup|
|-----------|----------|
|Data backups are copies of the data in the databases on your RDS instance. These backups include physical, logical, and snapshot backups. You can use these backups to restore your RDS instance. For more information, see [Restore the data of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance.md). Your RDS instance automatically creates physical or snapshot backups based on the storage media that you use: -   MySQL 5.5, 5.6, 5.7, and 8.0 on RDS High-availability or Enterprise Edition with local SSDs:
    -   Supports full physical backups when you perform automatic backups.
    -   Support full physical backups, full logical backups, and single-database logical backups when you perform manual backups.
-   MySQL 5.7 and 8.0 on RDS High-availability Edition with standard or enhanced SSDs:

Supports only snapshot backups. Snapshot backup files can be used to restore data to a new RDS instance. You cannot download snapshot backup files.

-   MySQL 5.7 and 8.0 on RDS Basic Edition with standard SSDs:

Supports only snapshot backups. Snapshot backup files can be used to restore data to a new RDS instance. You cannot download snapshot backup files.


|Log backups are copies of the binary log files that are generated on your RDS instance. You can use log backup files to restore the data of your RDS instance to a previous point in time. For more information, see [Restore the data of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance.md). Your RDS instance automatically backs up the binary log files. **Note:**

-   Log backup files occupy disk space on your RDS instance.
-   If a log backup file reaches 500 MB in size or the write operation exceeds 6 hours, your RDS instance starts to write data to a new log backup file. The old log backup file is then asynchronously uploaded to Alibaba Cloud Object Storage Service \(OSS\).
-   After a log backup file is uploaded to OSS, the file no longer occupies disk space on your RDS instance. However, you can still use this log backup file to restore data.
-   The RDS Basic Edition does not support the upload of log backup files to OSS.
-   You cannot access the OSS buckets that store log backup files. |

## Modify the backup settings of an RDS instance that is attached with local SSDs

ApsaraDB RDS automatically backs up each RDS instance based on the specified backup policy.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Backup and Restoration**.

5.  On the **Backup and Restoration** page, click the **Backup Settings** tab and then the **Edit** button.

6.  Configure the following parameters and click **OK**.

    ![Modify the backup settings of an RDS instance that is attached with local SSDs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9430359951/p86591.png)

    |Parameter|Description|
    |---------|-----------|
    |**Backup Cycle**|The cycle based on which you want to create a backup. You can select one or more days of the week. **Note:** For data security purposes, we recommend that you back up your RDS instance at least twice a week. |
    |**Backup Time**|The hour at which you want to create a backup. We recommend that you select an off-peak hour.|
    |**Retention Period**|The period of time for which you want to retain backup files. You can specify a number of days or select **long term backup**.     -   If you specify a number of days, ApsaraDB RDS deletes backup files that are stored longer than the specified retention period. If you select the **long term backup** option, ApsaraDB RDS does not delete backup files. If you want to retain backup files after you release your RDS instance, set the **Backup Retention Policy After Release** parameter to **Latest** or **All**.
    -   If the specified retention period does not exceed 730 days, backup files are retained as regular backup files.
    -   If the specified retention period exceeds 730 days, backup files that are stored longer than 730 days are automatically converted into archived backup files. Therefore, you must specify an archived backup retention period. For example, if you select Monthly and then enter 2 in the unit field, ApsaraDB RDS retains the first two archived backup files that are generated per month.

![Configure the backup cycle](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9430359951/p86587.png) |
    |**Log Backup**|The switch that is used to enable or disable the log backup feature. **Note:** If you disable this feature, all of the log backup files are deleted and you cannot restore the data of your RDS instance to a previous point in time. |
    |**Log Retention Period \(Days\)**|    -   The number of days for which you want to retain log backup files. Valid values: 7 to 730. Default value: 7.
    -   The log backup retention period must be less than or equal to the data backup retention period. |
    |**Restore Individual Database/Table**|The feature that is used to restore individual databases and tables. After you enable this feature, ApsaraDB RDS changes the backup file format to support this feature. By default, this feature is enabled and cannot be disabled. For more information, see [Restore individual databases and tables of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md).|
    |**Backup Retention Policy After Release**|The policy that is used to retain data backup files after your RDS instance is released. Valid values: **None**, **Latest**, and **All**. To prevent data losses that are caused by overdue payments or unintentional operations, we recommend that you select **Latest** or **All**.

**Note:** ApsaraDB RDS permanently retains data backup files free of charge. |


## Modify the backup settings of an RDS instance that uses standard or enhanced SSDs

ApsaraDB RDS automatically backs up each RDS instance based on the specified backup policy.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Backup and Restoration**.

5.  On the **Backup and Restoration** page, click the **Backup Settings** tab and then the **Edit** button.

6.  Configure the following parameters and click **OK**.

    ![Modify the backup settings of an RDS instance that are attached with standard or enhanced SSDs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9430359951/p134971.png)

    |Parameter|Description|
    |---------|-----------|
    |**Snapshot Backup Period**|The cycle based on which you want to create a backup. You can select one or more days of the week. **Note:** For data security purposes, we recommend that you back up your RDS instance at least twice a week. |
    |**Snapshot Backup Start Time**|The hour at which you want to create a backup. We recommend that you select an off-peak hour.If you want to increase the snapshot backup frequency, select **Increase Snapshot Frequency** and specify a snapshot backup frequency. |
    |**Snapshot Backup Retention**|The number of days for which you want to retain snapshot backup files. By default, the maximum snapshot backup retention period is 730 days. However, if you select **Increase Snapshot Frequency**, the maximum snapshot backup retention period is shortened based on the specified snapshot backup frequency. You can calculate the maximum snapshot backup retention period based on the following formula:Maximum snapshot backup retention period = \(900/Number of backups created per day/Number of backups created per week × 7\). The result is rounded down to the next integer.

For example, if you select two days of the week and then select the Every 30 Minutes frequency, the maximum snapshot backup retention period is 65 days based on the following calculation: Maximum snapshot backup retention period = ⌊900/\(24 × 2 \)/2 × 7⌋ = 65 \(days\). |
    |**Log Backup**|The switch that is used to enable or disable the log backup feature. **Note:** If you disable this feature, all of the log backup files are deleted and you cannot restore the data of your RDS instance to a previous point in time. |
    |**Log Retention Period \(Days\)**|    -   The number of days for which you want to retain log backup files. Valid values: 7 to 730. Default value: 7.
    -   The log backup retention period must be shorter than or equal to the data backup retention period.
**Note:** If your RDS instance runs MySQL 5.7 on RDS Basic Edition with standard SSDs, the log retention period is seven days and cannot be changed. |
    |**Single-digit Second Backup**|The switch that is used to enable the single-digit second backup feature. This feature allows you to take snapshots in seconds. ApsaraDB RDS retains up to 10 snapshot backup files. If the number of retained snapshot backup files reaches 10, the next snapshot backup fails. Therefore, we recommend that you set the **Snapshot Backup Retention** parameter to a value that is less than or equal to 10. **Note:** This feature is supported only when your RDS instance uses enhanced SSDs. |


## Manually back up an RDS instance

In this example, the RDS instance runs MySQL 5.7 on RDS High-availability Edition and is attached with local SSDs.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the upper-right corner of the page, click **Back Up Instance**.

5.  Specify a backup mode and a backup policy. Then, click **OK**.

    ![Physical Backup](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9430359951/p40345.png)

    **Note:** If you select the **Logical Backup** mode and then the **Single-Database Backup** policy, you must also select databases from the left-side list and click the **\>** icon to move the selected databases to the right-side list. If no databases are available, you must create databases before you back up your RDS instance. For more information, see [Create accounts and databases for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create accounts and databases for an ApsaraDB RDS for MySQL instance.md).

    ![Single-database logical backup](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9430359951/p40344.png)

6.  In the upper-right corner of the page, click the **Task Progress** button to view the progress of the backup task.

    ![View the progress of the backup task](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3550359951/p66932.png)

    **Note:**

    -   After the backup task is completed, you can go to the **Backup and Restoration** page to download the backup file. Some RDS instances do not support the download of backup files. For more information, see [Download data and log backup files of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Download data and log backup files of an ApsaraDB RDS for MySQL instance.md).

        ![Download a backup file](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3550359951/p66935.png)

    -   The retention period of backup files that are generated from manual backups is specified by the **Data Backup Retention** parameter. For more information, see the parameters described in [Step 6](#table_dn7_r06_h1k).

## FAQ

1.  How do I query data from backup files?

    If you have full logical backup files, you can use Alibaba Cloud Database Backup \(DBS\) to query data from these files. This way, you do not need to restore the data of these files. For more information, see [Overview]().

2.  Can I disable the data backup feature of my RDS instance?

    No, you cannot disable the data backup feature of your RDS instance. However, you can reduce the backup frequency to as low as twice a week. The data backup retention period must span at least seven days.

3.  Can I disable the log backup feature of my RDS instance?

    Yes, if you are not using the RDS Basic Edition, you can disable the log backup feature of your RDS instance.

4.  Why did my backup task fail?

    You may have executed DDL statements when the backup task was in progress. DDL statements trigger locks on tables. Your backup task may have failed as a result of the table locks.

5.  My RDS instance has a small volume of data. However, the size of the generated snapshot is large. Why?

    ApsaraDB RDS eliminates empty blocks when it takes a snapshot of your RDS instance. This allows the size of the snapshot to be smaller than the required disk space. Each block is 2 MB in size. However, if write operations are scattered, a large number of blocks are not full. For example, if 3 MB of data is written across two, three, or four blocks, each of the blocks is not full. When ApsaraDB RDS calculates the size of the snapshot, it counts in all of these non-empty blocks to which data is written. As a result, the disk space that is occupied by the snapshot is greater than the actual size of the snapshot.

6.  After I release my RDS instance, how do I restore data by using a retained backup file?

    Log on to the ApsaraDB RDS console and go to the **Backup for Deleted Instances** page. Then, download the required backup file and restore data to an on-premises database.

    ![Backup for Deleted Instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9430359951/p86993.png)


## References

-   [Download data and log backup files of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Download data and log backup files of an ApsaraDB RDS for MySQL instance.md)
-   [Restore the data of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance.md)

## Related operations

|Operation|Description|
|---------|-----------|
|[Create backup set](/intl.en-US/API Reference/Backup and recovery/Create backup set.md)|Creates a data backup for an ApsaraDB RDS instance.|
|[Query backup sets](/intl.en-US/API Reference/Backup and recovery/Query backup sets.md)|Queries the data backup files of an ApsaraDB RDS instance.|
|[Query backup settings](/intl.en-US/API Reference/Backup and recovery/Query backup settings.md)|Queries the backup settings of an ApsaraDB RDS instance.|
|[Modify backup settings](/intl.en-US/API Reference/Backup and recovery/Modify backup settings.md)|Modifies the backup settings of an ApsaraDB RDS instance.|
|[Delete backup sets](/intl.en-US/API Reference/Backup and recovery/Delete backup sets.md)|Deletes the data backup files of an ApsaraDB RDS instance.|
|[Query backup tasks](/intl.en-US/API Reference/Backup and recovery/Query backup tasks.md)|Queries the backup tasks of an ApsaraDB RDS instance.|
|[Query log backup files](/intl.en-US/API Reference/Backup and recovery/Query log backup files.md)|Queries the binary log files of an ApsaraDB RDS instance.|

