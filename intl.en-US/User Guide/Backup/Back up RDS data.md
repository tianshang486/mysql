# Back up RDS data {#concept_l1m_xgn_ydb .concept}

You can configure a backup policy to adjust the cycles of RDS data backup and log backup. You can also manually back up RDS data.

## Precautions {#section_zlc_zpq_eu2 .section}

-   Instance backup files occupy backup space. Charges are incurred if the used space exceeds the free quota. You must set a backup cycle appropriately to cater to the service requirements based on the available backup space. For information about the free quota, see [View the free quota of the backup space](intl.en-US/User Guide/Backup/View the free quota of the backup space.md#).
-   For information about billing methods and billable items, see [Billing methods and billing items](../../../../intl.en-US/Purchase Guide/Billing methods and billing items.md#).
-   For information about the charging standards for backup space usage, see [ApsaraDB RDS for MySQL pricing](https://www.alibabacloud.com/product/apsaradb-for-rds#pricing).
-   Do not perform data definition language \(DDL\) operations during a backup. If you do so, your tables may be locked and consequently the backup fails.
-   We recommend that you back up your RDS data or log data during off-peak hours.
-   If you need to back up a large volume of RDS data or log data, the backup may take a long time.
-   Backup files are reserved only for a specified period of time, therefore you need to download the backup files in time.

## Backup policies {#section_oyj_3k4_ydb .section}

ApsaraDB supports data backup and log backup. To recover data to a point in time, you must enable the log backup function. The following table lists the backup policies applicable to different database types.

|Database type|Data backup|Log backup|
|-------------|-----------|----------|
|MySQL| -   MySQL 5.5/5.6/5.7/8.0 with on-premises SSD:
    -   Automatic backup supports full physical backup.
    -   Manual backup supports full physical backup, full logical backup, and single-database logical backup.
-   MySQL 5.7/8.0 High-availability edition with SSD:
    -   Supports only snapshot-based backup, which helps to restore data to a new instance.
    -   Does not support data download.
-   MySQL 5.7/8.0 Basic edition with SSD:
    -   Supports only snapshot-based backup, which helps to restore data to a new instance.
    -   Does not support data download.

 | -   Binlog files occupy instance disk capacity.
-   When the size of a binlog file exceeds 500 MB or data has been written into the file for more than 6 hours, a new binlog file is generated. In addition, the old binlog file is uploaded asynchronouly.
-   Using the binlog upload function, you can upload binlog files to OSS. This does not affect the data recovery function and stops the binlog files from occupying instance disk space.

 **Note:** 

-   In a Basic edition, you cannot upload binlog files.
-   You cannot access the OSS buckets where binlog files are stored.

 |
|SQL Server| -   SQL Server supports full physical backup and incremental physical backup.
-   Automatic backup cycles from full backup, incremental backup to incremental backup. For example, if a full backup is performed on Monday, incremental backups are performed on Tuesday and Wednesday, and another full backup is performed on Thursday, with incremental backups on Friday and Saturday. If a full backup is manually performed at any time in the backup cycle, the next two backups are incremental backups.
-   SQL Server supports single-database backup, which enables you to back up one or more databases in a specified instance.
-   SQL Server always compresses transaction logs during the backup process. On the Backup and Recovery page of the target instance’s management console, you can click **Compress Transaction Log** to manually compress transaction logs.

 | -   RDS automatically generates log backups \(log files\). You can set the log file generation interval to 30 minutes or to the data backup interval.

The interval does not change the total size of generated log files.

-   The log backup function cannot be disabled.
-   You can set the log backup retention period to a time period ranging from 7 to 730 days.
-   You can download log files.

 **Note:** When the log file generation interval is set to 30 minutes, you can recover data of the last 30 minutes in an SQL Server Basic edition in the event of disasters such as an SSD damage.

 |
|PostgreSQL|Supports full physical backup.|After being generated, write-ahead logs \(WALs\) \(16 MB per log\) are compressed and uploaded immediately. Local files are deleted within 24 hours.|
|PPAS|Supports full physical backup.|After being generated, WALs \(16 MB per log\) are compressed and uploaded immediately. Local files are deleted within 24 hours.|
|MariaDB|Supports snapshot-based backup.| -   Binlog files occupy instance disk capacity.
-   When the size of a binlog file exceeds 500 MB or data has been written into the file for more than 6 hours, a new binlog file is generated. In addition, the old binlog file is uploaded asynchronouly.
-   Using the binlog upload function, you can upload binlog files to OSS. This does not affect the data recovery function and stops the binlog files from occupying instance disk space.

 |

## Configure automatic backup {#section_f33_lk4_ydb .section}

ApsaraDB can automatically back up RDS data and log data based on the backup policies you specify.

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.
3.  Click the ID of the instance to visit the Basic Information page.
4.  In the left-side navigation pane, click **Backup and Recovery**.
5.  On the Backup and Recovery page, select **Backup Settings** and click **Edit**.
6.  In the Backup Cycle dialog box, set backup parameters and click **OK**.

    The parameters are as follows:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7964/15656633154104_en-US.png)

    |Parameter|Description|
    |---------|-----------|
    |Data Retention Period \(days\)|Specifies the time period during which backup files are retained. The default value is 7 days. The value range is 7 to 730 days. **Note:** RDS backup files in the MySQL 5.7 Basic edition are retained for free for seven days. This retention period cannot be changed.

 |
    |Backup Cycle Frequency|This parameter can be set to one or multiple days in a week. **Note:** MariaDB TX instances are backed up every day by default. This setting cannot be changed.

 |
    |Next Backup|This parameter can be set to any time period in the unit of hour. We recommend that you select off-peak hours.|
    |Log Backup|Possible values are **Enable** and **Disable**.|
    |Log Retention Period \(days\)|     -   Specifies the number of days during which log backup files are retained. The default value is 7 days.
    -   The value range is 7 to 730 days and it must be less than or equal to the value of the Data Retention Period \(days\) parameter.
 **Note:** 

    -   RDS log backup files in the MySQL 5.7 Basic edition are retained for seven days. The retention period cannot be changed.
    -   The PostgreSQL 10.0 Basic edition does not support log backup.
 |


## Configure manual backup {#section_yvd_yk4_ydb .section}

**Note:** 

-   This section uses the backup for an RDS instance in the MySQL 5.7 High-availability edition equipped with on-premises SSD as an example.
-   RDS for MariaDB TX instances do not support manual backup.

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.
3.  Click the ID of the instance to visit the Basic Information page.
4.  Click **Back up Instance** at the upper right corner.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7964/15656633154105_en-US.png)

    **Note:** 

    -   The backup mode and policy vary with the database type. For more information, see [Backup policies](#section_oyj_3k4_ydb).
    -   If you choose single-database backup, click **\>** to select a database to be backed up. If you do not have a database, create one by referring to [Create a database](intl.en-US/User Guide/Database management/Create a database.md#).
5.  Set **Backup Mode** and **Backup Policy**, and click **OK**.

## FAQ {#section_k4f_onf_25m .section}

1.  Can I disable RDS data backup?

    No. You cannot disable RDS data backup. However, you can lower the RDS data backup frequency to at least twice a week. Data backup files are retained for 7 to 730 days.

2.  Can I disable RDS log backup?

    You cannot disable RDS log backup for instances in the MySQL/PostgreSQL Basic edition or for SQL Server instances. For other instances, you can disable RDS log backup as needed.


