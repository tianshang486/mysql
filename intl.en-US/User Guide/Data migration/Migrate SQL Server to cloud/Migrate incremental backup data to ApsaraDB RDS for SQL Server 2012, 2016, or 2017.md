# Migrate incremental backup data to ApsaraDB RDS for SQL Server 2012, 2016, or 2017 {#concept_bsg_zcw_ydb .concept}

## Scenarios {#section_ntt_5dw_ydb .section}

You can migrate incremental backup data to ApsaraDB RDS for SQL Server 2012, 2016, or 2017. Your service will be disconnected for a few minutes during the migration process. You can migrate incremental backup data in the following scenarios:

-   You need to physically migrate data to an ApsaraDB RDS for SQL Server instance.

**Note:** 

-   Physical migration is the migration of backup files. Logical migration is the migration of data by executing DML statements in the ApsaraDB RDS for SQL Server instance.
-   Physical migration guarantees 100% consistency between the source and destination databases. Logical migration cannot guarantee 100% consistency of database information such as index fragmentation and statistical information.
-   You need to use incremental migration for time-sensitive business to limit the disconnection time to a few minutes.

**Note:** 

If your business has a data volume of less than 100 GB, and does not provide time-sensitive services, we recommend that you use full backup data migration. This process will disconnect the business for a longer period of time, such as two hours. For more information, see [Migrate full backup data to RDS for SQL Server 2012/2016/2017](intl.en-US/User Guide/Data migration/Migrate SQL Server to cloud/Migrate full backup data to RDS for SQL Server 2012__2016__2017.md#).


This topic describes how to use the full backup file and differential or log files that are stored in your OSS bucket to incrementally migrate your on-premises SQL Server database to a database in an ApsaraDB RDS for SQL Server instance.

## Procedure {#section_psh_d2w_ydb .section}

![](images/6187_en-US.png)

The procedure is explained on a timeline basis.

|Migration phase|Step|Description|
|---------------|----|-----------|
|Full backup and restoration|Step 1: Before 00:00|Complete the following preparatory work: -   Execute the DBCC CHECKDB statement.
-   Shut down the local backup system.
-   Change the recovery model of the on-premises database to full.

 |
|Step 2: 00:01|Perform full backup on the on-premises database.|
|Step 3: 02:00|Full backup is completed. Time taken: one hour. Upload the backup file to the OSS bucket.|
|Step 4: 03:00|The backup file is uploaded. Time taken: one hour. Restore data from the backup file to the RDS instance in the ApsaraDB for RDS console.|
|Step 5: 22:00|The backup file is restored. Time taken: 19 hours. Perform incremental log backup and upload the log file to the OSS bucket.|
|Incremental backup and restoration|Step 6: 22:20|The log file is backed up and uploaded. Time taken: 20 minutes. Restore incremental data to the RDS instance by using the log file in the ApsaraDB for RDS console.|
|Step 7: 22:30| -   The incremental data is restored. Time taken: 10 minutes.
-   Repeat step 6 and step 7 to back up and upload log files and restore incremental data to the instance until the last log file is less than 500 MB.
-   **Stop writing data to the on-premises database from your on-premises application. Perform incremental log backup and restoration for the last time.**

 |
|Database opening|Step 8: 22:34|The last log file is incrementally migrated to the instance. Time taken: four minutes. Prepare to bring the database online.|
|Step 9: 22:35|The database comes online. If you choose to execute the DBCC statement asynchronously, the database is opened and can be used in one minute.|

**From the preceding procedure, you can see that you do not need to stop your application until the last log file is generated.** In this case, you only need to stop your application for five minutes.

## Prerequisites {#section_bdr_f2w_ydb .section}

-   **The ApsaraDB RDS for SQL Server instance must be one of the following editions:** 
    -   ApsaraDB RDS for SQL Server 2012/2016 Web Edition
    -   ApsaraDB RDS for SQL Server 2012 Enterprise Basic Edition
    -   ApsaraDB RDS for SQL Server 2012/2016 Standard/Enterprise Edition
    -   ApsaraDB RDS for SQL Server 2017 Enterprise Cluster Edition
-   **Grant access permissions on OSS buckets to your RDS account.** 

    After you have granted the access permissions, the system creates a role named **AliyunRDSImportRole** in RAM. Do not modify or delete this role. Otherwise, you will not be able to download the backup files when you migrate a database to the RDS instance. If you modify or delete this role, you must re-authorize your RDS account.

-   **Create an OSS bucket.** 

    Create an OSS bucket that is in the same region as the destination instance. Skip this step if you already have an OSS bucket. For more information about how to create a bucket, see [Create a bucket](https://www.alibabacloud.com/help/zh/doc-detail/31885.htm?spm=a2c63.p38356.a3.4.40b84251jSxsqH).

-   **Make sure the database recovery model is full.** 

    If you need to incrementally migrate your database to the RDS instance, the recovery model of the database must be full. If you set the recovery model to simple, the transaction log will not be backed up. Therefore, the migration may take more time if the differential backup file is large.

-   **Storage requirements for the ApsaraDB RDS for SQL Server instance.** 

    Make sure that the ApsaraDB RDS for SQL Server instance has enough storage space. If not, you must increase the space before migration.

-   **The names of databases in the ApsaraDB RDS for SQL Server instance must be unique.** 

    If the instance contains a database that has the same name as the source database, you must back up and delete it from the instance before migration.

-   **Create a privileged account for the ApsaraDB RDS for SQL Server instance.** 

    Create a privileged account for the destination instance in the ApsaraDB for RDS console. Skip this step if you already have a privileged account.

-   **Shut down the local backup system.** 

    Shut down the backup system of the local environment to ensure the success of the migration. Otherwise, the migration may fail because the local backup system automatically backs up the on-premises database.

-   **Execute the DBCC CHECKDB statement.** 

    Execute the DBCC CHECKDB\('xxx'\) statement in the on-premises database to make sure that there are no allocation or consistency errors. If the check succeeds, the following messages are returned:

    ``` {#codeblock_sxd_p67_h8m}
    Checkdb found 0 allocation errors and 0 consistency errors in database 'xxx '.
      DBCC execution completed. If DBCC printed error messages, contact your system administrator.
    ```

    If the output contains any error messages, you must fix the on-premises database to prevent migration failure.


## Limits {#section_pdf_l2w_ydb .section}

-   **Version of backup files** 

    Migrating data from a backup file of a later version to a database of an earlier version is not supported. For example, you cannot migrate from SQL Server 2016 to ApsaraDB RDS for SQL Server 2012.

-   **Suffix of backup files** 

    The names of backups files can only end with .bak, .diff, .trn, or .log. If you do not use the script in this topic to generate a backup file, you must use the following suffixes:

    -   bak: indicates a full backup file.
    -   diff: indicates a differential backup file.
    -   trn and log: indicate a transaction log backup.
-   **Name of backup files**

    The names of backup files cannot contain special characters such as at signs \(@\) and vertical bars \(|\). Otherwise, the backup data stored in the OSS bucket cannot be migrated to the instance.


## Demo {#section_mwg_5fw_ydb .section}

## Back up the on-premises database {#section_hfj_vzw_b2b .section}

**Note:** Before you make a full backup of the on-premises database, make sure to shut down the backup system for the local environment.

1.  Download the [backup script](https://rdshelpattachments.oss-cn-beijing.aliyuncs.com/Migration/RDSBackupSpecifiedDatabasesToLocal.sql) and open it with SQL Server Management Studio \(SSMS\).
2.  Modify the following parameters as needed:

    |Parameter|Description|
    |---------|-----------|
    |@backup\_databases\_list|The databases to be backed up. Separate multiple databases with semicolons \(;\) or commas \(,\).|
    |@backup\_type|The type of the backup. Valid values:     -   FULL: full backup
    -   DIFF: differential backup
    -   LOG: log backup
 |
    |@backup\_folder|The local directory that stores the backup file. A directory will be automatically created if not specified.|
    |@is\_run|Specifies whether to perform a backup. Valid values:     -   1: performs a backup.
    -   0: only performs a check.
 |

3.  Execute the backup script.

## Upload the backup file to OSS {#section_agb_p1x_b2b .section}

Upload the backup file to your OSS bucket after the on-premises database is backed up.

-   Method 1: Use ossbrowser

    We recommend that you use the ossbrowser tool to upload the backup file to OSS. For more information, see [ossbrowser](https://www.alibabacloud.com/help/zh/doc-detail/61872.htm).

-   Method 2: Use the OSS console

    If the backup file is smaller than 5 GB, you can upload the file in the OSS console. For more information, see [Upload an object](https://www.alibabacloud.com/help/zh/doc-detail/31886.htm).

-   Method 3: Use the operations of the OSS API

    If you want to complete the migration unattended, you can use the OSS API to perform a multipart or resumable upload. For more information, see [Multipart upload and resumable upload](https://www.alibabacloud.com/help/zh/doc-detail/31850.htm).


## Create the migration task {#section_tmd_xfk_zww .section}

1.  Log on to the [ApsaraDB for RDS console](https://rdsnew.console.aliyun.com/).
2.  In the upper-left corner of the page, select the region where the instance is located.

    ![Select a region where the instance is located.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156801771536543_en-US.png)

3.  Click the ID of the instance to go to the Basic Information page.
4.  In the left-side navigation pane, click **Backup and Restoration**.
5.  In the upper-right corner of the page, click **Migrate OSS Backup Data to RDS**.
6.  If you are using the feature for the first time, you must perform the following steps to authorize the RDS account to access OSS:
    1.  Click Authorize on the Import data step of the Import Guide wizard, as shown in the following figure.

        ![](images/6199_en-US.png)

    2.  Go to the Cloud Resource Access Authorization page and click **Confirm Authorization Policy** to complete the authorization.
7.  On the Import data step of the Import Guide wizard, configure the following parameters and click **OK** to upload the backup file to OSS.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7998/15680177156114_en-US.png)

    |Parameter|Description|
    |---------|-----------|
    |Database Name|Enter the name of the destination database in the destination instance. **Note:** The name of the database must meet the requirements of SQL Server.

 |
    |OSS Bucket|Select the OSS bucket to store the backup file.|
    |OSS Subfolder Name|Enter the name of the OSS subfolder to store the backup file.|
    |OSS File|Enter the prefix of the backup file name and click the search icon. A list of files is displayed. The list contains the name, size, and update time of each file that matches the query. Select the backup file that you need to restore.|
    |Cloud Migration Plan|     -   Immediate Access \(Full Backup\): You can use a full backup file to migrate your database to the instance. Select **Immediate Access \(Full Backup\)**.
    -   Access Pending \(Incremental Backup\): You can use a full backup file and a differential or log file to incrementally migrate your database to the instance.
 |
    |Consistency Check Mode|     -   Asynchronous DBCC: If the database contains a large volume of data, the DBCC CHECKDB statement will take a long time to execute. The DBCC CHECKDB statement is asynchronously executed after the database is opened to decrease the time spent on opening the database and minimize downtime. If your application requires a short downtime, and the result of DBCC CHECKDB does not affect your business, we recommend that you select Asynchronous DBCC.
    -   Synchronous DBCC: If you need to execute the DBCC CHECKDB statement to identify consistency errors, we recommend that you choose Synchronous DBCC. In this case, the database takes more time to be opened.
 |

    You can click Refresh to view the latest status of the migration task. If the migration fails, you can view the task description and troubleshoot errors by referring to the Common errors section in this topic.


## Import differential or log files {#section_qxz_y4w_kkz .section}

After the full backup file of the on-premises database is migrated to the instance, you need to migrate data from the differential or log files. The procedure is as follows.

1.  Log on to the [ApsaraDB for RDS console](https://rdsnew.console.aliyun.com/?spm=a2c63.p38356.a3.17.165742516hVXZz).
2.  In the upper-left corner of the page, select the region where the instance is located.

    ![Select the region](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156801771536543_en-US.png)

3.  Click the ID of the instance to go to the Basic Information page.
4.  In the left-side navigation pane, click **Backup and Restoration**.
5.  In the upper-right corner of the page, click **Migrate OSS Backup Data to RDS**.

    Find the database that you want to import incremental data to, and click **Upload Incremental Files** next to the database. The Upload Incremental Files dialog box appears, as shown in the following figure.

    ![](images/4345_en-US.png)

6.  Configure the parameters, and click **OK** to import the differential or log file.

    If you have multiple log files, you can use the same method to import the log files one by one.

    When you upload incremental files, ensure that the last file is not larger than 500 MB to reduce the time of incremental migration. You can click **Refresh** to view the latest status of the migration task.

    **Note:** Before the last log file is generated, you must stop writing data to the on-premises database to ensure the data consistency between the on-premises database and the ApsaraDB RDS for SQL Server database.


## Open the database {#section_9l3_lqk_esd .section}

After backup files are migrated, the ApsaraDB RDS for SQL Server database is in the In Recovery or Restoring state. If your instance is of the High-availability Edition, it is in the In Recovery state. If your instance is of the Basic Edition, it is in the Restoring state. The database in either state cannot be read or written, and the database needs to be opened as follows:

1.  Log on to the [ApsaraDB for RDS console](https://rdsnew.console.aliyun.com/?spm=a2c63.p38356.a3.20.165742516hVXZz).
2.  Select the region where the destination instance is located and click the ID of the destination instance to go to the Basic Information page.
3.  In the left-side navigation pane, click **Backup and Restoration**.
4.  In the upper-right corner of the page, click **Migrate OSS Backup Data to RDS**.
5.  Find the database that you need to restore backup files to, and click **Open Database** to the right of the database.

    ![](images/4346_en-US.png)

6.  In the Open Database dialog box that appears, select a consistency check mode. There are two ways to perform a database consistency check:
    -   Asynchronous DBCC: The DBCC CHECKDB statement is asynchronously executed after the database is opened. If the database contains a large volume of data, the DBCC CHECKDB statement will take a long time to execute. Asynchronous DBCC decreases the time spent on opening the database and minimizes downtime. If your application requires a short downtime, and the result of DBCC CHECKDB does not affect your business, we recommend that you select Asynchronous DBCC.

    -   Synchronous DBCC: If you need to execute the DBCC CHECKDB statement to identify consistency errors, we recommend that you choose Synchronous DBCC.


## View migration records {#section_j5n_bgk_zdb .section}

You can view migration records over a period of time. The procedure is as follows:

On the Backup and Restoration page, click the **Backup Data Upload History** tab. By default, migration records of the past week are displayed. You can also modify the time range to view the records over a specific period of time.

![](images/4347_en-US.png)

## View file details of a migration task {#section_v4r_lcy_b2b .section}

If you need to view the details of all the backup files for a migration task, you can perform the following steps:

On the Backup and Restoration page, click the Backup Data Upload History tab. Click **View File Details** to the right of the migration task. The View File Details message appears, and displays details of all backup files related to the task.

![](images/4348_en-US.png)

## Common errors {#section_oqm_mlw_ydb .section}

For more information about common errors that may occur during the full backup migration, see [Migrate full backup data to RDS for SQL Server 2012/2016/2017](intl.en-US/User Guide/Data migration/Migrate SQL Server to cloud/Migrate full backup data to RDS for SQL Server 2012__2016__2017.md#). The following errors may occur during incremental migration.

 **Failed to open the database** 

Error message:

``` {#codeblock_q93_2bp_pb7}
Failed to open database xxx.
```

**Cause:** Some advanced features enabled by the on-premises database are migrated to the ApsaraDB RDS for SQL Server database. If your ApsaraDB RDS for SQL Server instance does not support these features, the database fails to be opened.

For example, if your on-premises database of the SQL Server Enterprise Edition enables the Data Compression or Partition feature, and you migrate the database to the database of the ApsaraDB RDS for SQL Server Web Edition, the error message is displayed.

**You can use the following methods to solve the problem:**

-   Disable the advanced features on the on-premises SQL Server database, back up the data again, and migrate the data by using OSS.

-   Purchase an ApsaraDB RDS for SQL Server instance that is of the same edition as the on-premises database. For example, if the on-premises database is of the SQL Server 2012 Enterprise Edition, you must purchase an instance of the ApsaraDB RDS for SQL Server Enterprise Basic or High-availability Edition.


 **The log sequence numbers \(LSN\) in the database backup chain are not in sequence** 

**Error message:** 

``` {#codeblock_37t_bi4_zcb}
The log in this backup set begins at LSN XXX, which is too recent to apply to the database.
        RESTORE LOG is terminating abnormally.
```

**Cause**: In SQL Server databases, differential or log files must be restored in order of the LSN sequence. Otherwise, the error message is displayed.

**Solution:** Restore the differential or log file that has the proper LSN. You can restore the files based on the backup time.

 **Asynchronous DBCC CHECKDB succeeds** 

**Message:** 

``` {#codeblock_pm4_dsv_khv}
Success to DBCC checkdb asynchronously.
```

**Description:** The DBCC CHECKDB statement consumes a large amount of resources and time. Therefore, you can perform the consistency check by executing the statement asynchronously to improve the efficiency of incremental migration. If this message is displayed, it indicates that there is no consistency error in your databases. The opposite error message is described in the following section.

 **Asynchronous DBCC CHECKDB fails** 

**Error message:** 

``` {#codeblock_cva_lxc_sij}
asynchronously DBCC checkdb failed: CHECKDB found 0 allocation errors and 2 consistency
        errors in table 'XXX' (object ID XXX).
```

**Cause:** Consistency errors occur in your databases.

**You can use the following methods to solve the problem:**

-   Execute the following statement in the ApsaraDB RDS for SQL Server database:

``` {#codeblock_r5w_2ww_oqj}
DBCC CHECKDB (DBName,REPAIR_ALLOW_DATA_LOSS)
```

    **Note:** Your data may be lost when you use this statement to fix errors.

-   1.  Execute the following statement in the on-premises database:

    ``` {#codeblock_aeq_8ac_n23}
    DBCC CHECKDB (DBName,REPAIR_ALLOW_DATA_LOSS)
    ```

2.  Back up the on-premises database again.
3.  Delete the corresponding database from the ApsaraDB RDS for SQL Server instance.
4.  Incrementally migrate the on-premises database to the instance again.

 **The file types are unmatched** 

**Error message:** 

``` {#codeblock_22k_rrn_00x}
Backup set (xxx) is a Database FULL backup, we only accept transaction log or differential backup.
```

**Cause:** After full migration is finished, you can only upload differential or log files. If you upload a full backup file, the error message is displayed.

**Solution:** You must upload a differential or log file.

 **The number of migrated databases reaches the limit** 

**Error message:** 

``` {#codeblock_ai5_tkh_b0g}
The database (xxx) migration failed due to databases count limitation.
```

**Cause:** You can only migrate 50 databases to an ApsaraDB RDS for SQL Server High-availability or Cluster Edition instance. If the limit is exceeded, the error message is displayed. The limit for ApsaraDB RDS for SQL Server Basic Edition instances is 100. There is no limit for ApsaraDB RDS for SQL Server 2008 R2 instances.

**Solution:** You can migrate the database to another instance or delete unnecessary databases from the current instance.

**Note:** Each database in an ApsaraDB RDS for SQL Server High-availability or Cluster Edition instance consumes three processes. If there are multiple databases in an instance, the instance will consume a large amount of connection processes. Therefore, the instance becomes unstable because it may fail to connect to resources that are stored in Service Worker. To ensure stability and efficiency, the maximum number of databases in an ApsaraDB RDS for SQL Server High-availability or Cluster Edition instance is limited to 50.

## Related operations {#section_hcn_555_jgb .section}

|Operation|Description|
|---------|-----------|
|[../DNMYSQ1851749/EN-US\_TP\_8160.md\#](../intl.en-US/API Reference/Migrate SQL Server to the cloud/CreateMigrateTask.md#)|Restores the backup files from OSS to the RDS instances.|
|[../DNMYSQ1851749/EN-US\_TP\_14732.md\#](../intl.en-US/API Reference/Migrate SQL Server to the cloud/CreateOnlineDatabaseTask.md#)|Opens a database when migrating backup data to RDS.|
|[../DNMYSQ1851749/EN-US\_TP\_8161.md\#](../intl.en-US/API Reference/Migrate SQL Server to the cloud/DescribeMigrateTasks.md#)|Queries the list of migration tasks.|
|[../DNMYSQ1851749/EN-US\_TP\_8162.md\#](../intl.en-US/API Reference/Migrate SQL Server to the cloud/DescribeOssDownloads.md#)|Queries the details of the backup data files which are uploaded to OSS.|

