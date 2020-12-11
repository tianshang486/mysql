# Migrate incremental backup data to ApsaraDB RDS for SQL Server 2012, 2014, 2016, 2017, or 2019

You can migrate the incremental backup data of a self-managed SQL Server database to an ApsaraDB RDS instance that runs SQL Server 2012, 2014, 2016, 2017, or 2019. The migration requires only a few minutes. This significantly shortens the duration of interruptions to your workloads.

-   Your RDS instance runs one of the following SQL Server versions and RDS editions:
    -   SQL Server 2017 EE on RDS Cluster Edition
    -   SQL Server 2012 SE, 2012 EE, 2014 SE, 2016 SE, 2016 EE, 2017 SE, and 2019 SE on RDS High-availability Edition
    -   SQL Server 2012 EE Basic, 2012 Web, and 2016 Web on RDS Basic Edition
-   The Object Storage Service \(OSS\) bucket used to store the backup files resides in the same region as your RDS instance. For more information about how to create an OSS Bucket, see [Create buckets](/intl.en-US/Quick Start/Create buckets.md).
-   The self-managed database uses the FULL recovery model.

    **Note:** If you want to migrate incremental backup data from the self-managed database to your RDS instance, make sure that the self-managed database uses the FULL recovery model. If the SIMPLE recovery model is used, the transaction logs of the self-managed database are not backed up. In this case, you can use only the differential backup file, which may be large and prolong the migration.

-   The remaining storage space of your RDS instance is sufficient. If the space is insufficient, you must increase it before migration.
-   The destination database on your RDS instance has a different name from the self-managed database.
-   A privileged account is created for your RDS instance. For more information, see [Create accounts and databases for an ApsaraDB for RDS instance running SQL Server 2012, 2016, 2017 SE, or 2019](/intl.en-US/RDS SQL Server Database/Quick start/Creating accounts and databases/Create accounts and databases for an ApsaraDB for RDS instance running SQL Server
         2012, 2016, 2017 SE, or 2019.md).
-   The DBCC CHECKDB statement is executed, and the execution result indicates that no allocation errors or consistency errors occur.

    **Note:** If no allocation errors or consistency errors occur, the following execution result is returned:

    ```
    ...
    CHECKDB found 0 allocation errors and 0 consistency errors in database 'xxx'.
    DBCC execution completed. If DBCC printed error messages, contact your system administrator.
    ```


You can migrate incremental backup data in the following scenarios:

-   Migrate data to your RDS instance in physical mode, instead of the logical mode.

    **Note:**

    -   Physical migration uses physical backup files. Logical migration requires DML statements.
    -   Physical migration ensures 100% data consistency between the source and destination databases. Logical migration cannot ensure 100% data consistency. For example, index fragmentation and statistical information may be inconsistent.
-   Migrate data with only minute-level business interruptions.

    **Note:** If your business can tolerate a longer interruption, such as two hours, and the self-managed database has less than 100 GB of data, we recommend that you use a full backup file for migration. For more information, see [Migrate full backup data to ApsaraDB RDS for SQL Server 2012,2014, 2016, 2017, or 2019](/intl.en-US/RDS SQL Server Database/Data migration/Migrate data from a user-created database to an RDS SQL Server database/Migrate full backup data to ApsaraDB RDS for SQL Server 2012,2014, 2016, 2017, or 2019.md).


In this topic, the migration is performed by using the full, log, and differential backup files that are stored in an OSS bucket.

## Precautions

-   This solution allows you to migrate the backup files of only one self-managed database at a time. If you want to migrate the backup files of multiple or all self-managed databases at a time, we recommend that you use the instance-level migration solution. For more information, see [Migrate data from an on-premises SQL Server instance to an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Data migration/Migrate data from a user-created database to an RDS SQL Server database/Migrate data from an on-premises SQL Server instance to an ApsaraDB RDS for SQL Server instance.md).
-   If the SQL Server version of the self-managed database is later than that of your RDS instance, you cannot migrate the backup files of the self-managed database to your RDS instance. For example, if the self-managed database runs SQL Server 2016 and your RDS instance runs SQL Server 2012, you cannot migrate the backup files of the self-managed database to your RDS instance.
-   The names of backup files cannot contain special characters, such as at signs \(@\) and vertical bars \(\|\). If the file names contain special characters, the migration fails.
-   After the service account of your RDS instance is granted the access permission on the OSS bucket, the system creates a role named **AliyunRDSImportRole** in RAM. Do not modify or delete this role. If you have modified or deleted this role, you cannot download the backup files when you migrate data to your RDS instance. In this case, you must re-authorize the service account of your RDS instance.
-   Before the migration is complete, do not delete the backup files from the OSS bucket. If you delete the backup files before the migration is complete, the migration fails.
-   The names of backup files can be suffixed only with bak, diff, trn, or log. If you do not use the script in this topic to generate a backup file, you must name the backup file with one of the following suffixes:
    -   bak: indicates a full backup file.
    -   diff: indicates a differential backup file.
    -   trn and log: indicate a log backup file.

## Procedure example

![](../images/p6187.png)

This flowchart shows the migration procedure on a timeline.

|Migration phase|Step|Description|
|---------------|----|-----------|
|Full backup and restoration|Step 1. Before 00:00|Complete the following preparatory work: -   Execute the DBCC CHECKDB statement and verify that no allocation errors or consistency errors occur.
-   Shut down the backup system of the self-managed database.
-   Change the recovery model of the self-managed database to FULL. |
|Step 2. 00:01|Perform a full backup on the self-managed database.|
|Step 3. 02:00|The full backup is complete. Time taken: one hour. Upload the full backup file to the OSS bucket.|
|Step 4. 03:00|The full backup file is uploaded. Time taken: one hour. Restore data from the full backup file to your RDS instance in the ApsaraDB RDS console.|
|Step 5. 22:00|The data of the full backup file is restored. Time taken: 19 hours. Perform an incremental log backup and upload the log backup file to the OSS bucket.|
|Incremental backup and restoration|Step 6. 22:20|The incremental log backup is complete, and the log backup file is uploaded. Time taken: 20 minutes. Restore data from the log backup file to your RDS instance in the ApsaraDB RDS console.|
|Step 7. 22:30|-   The data of the log backup file is restored. Time taken: 10 minutes.
-   Repeat Step 6 and Step 7 to back up incremental logs, upload the log backup files to the OSS bucket, and restore data from the log backup files to your RDS instance until the size of the last log backup file is less than 500 MB.
-   Before you perform the last incremental log backup, stop writing data to the self-managed database. Then, upload the last log backup file to the OSS bucket and restore data from the last log backup file. |
|Database opening|Step 8. 22:34|The data of the last log backup file is restored. Time taken: 4 minutes. Bring the destination database on your RDS instance online.|
|Step 9. 22:35|The destination database is online. If you choose to execute the DBCC statement in asynchronous mode, the destination database can be brought online within 1 minute.|

The preceding procedure shows that you do not need to stop your application until the last log backup. In this example, the application is interrupted for no more than 5 minutes.

## Back up the self-managed database

1.  Download the [backup script](https://rdshelpattachments.oss-cn-beijing.aliyuncs.com/Migration/RDSBackupSpecifiedDatabasesToLocal.sql) and open it by using SQL Server Management Studio \(SSMS\).

2.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |@backup\_databases\_list|Specify the database that you want to back up. You can specify multiple databases to back up at the same time. In this case, you must separate multiple databases with semicolons \(;\) or commas \(,\).|
    |@backup\_type|Specify the type of backup that you want to perform. Valid values:     -   FULL: full backup
    -   DIFF: differential backup
    -   LOG: log backup |
    |@backup\_folder|Specify the directory in which you want to store the backup files on your computer. If the specified directory does not exist, the system automatically creates a directory.|
    |@is\_run|Specify whether to perform a backup or a check. Valid values:     -   1: Perform a backup.
    -   0: Perform a check. |

3.  Run the backup script.


## Upload the full backup file to the OSS bucket

After the self-managed database is backed up, you must upload the full backup file to the OSS bucket. The following methods are available for uploading:

-   Method 1: Use ossbrowser

    We recommend that you use the ossbrowser tool to upload the full backup file. For more information, see [ossbrowser](https://www.alibabacloud.com/help/doc-detail/61872.html).

-   Method 2: Use the OSS console

    If the size of the full backup file is less than 5 GB, you can upload it in the OSS console. For more information, see [Upload objects](https://www.alibabacloud.com/help/doc-detail/31886.html).

-   Method 3: Call an OSS operation

    You can call an OSS operation to upload the full backup file in resumable mode. For more information, see [Multipart upload and resumable upload](https://www.alibabacloud.com/help/doc-detail/31850.html).


## Create a migration task

1.  Log on to the [ApsaraDB RDS console](https://rdsnew.console.aliyun.com/).

2.  In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Backup and Restoration**.

5.  Click **Restore Backup Data to RDS**. In the dialog box that appears, select **OSS Manual \(Restore Backup Data to RDS\)** and click **Next**.

    **Note:** In **DBS Auto \(Restore Backup Data to RDS\)** mode, the migration is fast and stable. For more information, see [Restore SQL Server backup data to the cloud]().

6.  In the **Import Guide** wizard, click **Next** twice.

    **Note:** When you use the OSS-based migration for the first time, you must authorize the service account of your RDS instance to access the OSS bucket. Click the button for **authorizing** and agree to authorize the service account. Otherwise, the **OSS Bucket** drop-down list in the Import Data step is empty.

7.  In the Import Data step, configure the following parameters.

    ![Import Data](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3321186061/p180273.png)

    |Parameter|Description|
    |---------|-----------|
    |**Database Name**|Enter the name of the destination database on your RDS instance. The destination database stores the data that is migrated from the self-managed database. The name can be different from the name of the self-managed database. **Note:** The name of the destination database must meet the requirements of open source SQL Server. |
    |**OSS Bucket**|Select the OSS bucket that stores the backup files.|
    |**OSS Subfolder Name**|Enter the name of the OSS bucket folder that stores the backup files.|
    |**OSS File**|Click the search icon to search for a backup file by using the prefix-based fuzzy match. The system displays the name, size, and update time of the backup file. Select the backup file that you want to upload to the OSS bucket.|
    |**Cloud Migration Method**|    -   Immediate Access \(Full Backup\): Select this option if only a full backup file is available. For this example, select **Immediate Access \(Full Backup\)**. This way, the CreateMigrateTask operation applies the parameter settings `BackupMode = FULL` and `IsOnlineDB = True` when it is called.
    -   Access Pending \(Incremental Backup\): Select this operation if log and differential backup files are also available. If you select this option, the CreateMigrateTask operation applies the parameter settings `BackupMode = UPDF` and `IsOnlineDB = False` when it is called. |
    |**Consistency Check Mode**|    -   Asynchronous DBCC: The DBCC CHECKDB statement is executed after the destination database is opened. This reduces the time to open the destination database and minimizes the downtime of your application. This mode is suitable for databases that contain a large volume of data because the execution is time-consuming in this scenario. If your application can tolerate only a short downtime and the execution result of the DBCC CHECKDB statement does not affect your business, we recommend that you select Asynchronous DBCC. This way, the CreateMigrateTask operation applies the parameter setting `CheckDBMode = AsyncExecuteDBCheck` when it is called.
    -   Synchronous DBCC: The DBCC CHECKDB statement is executed when the destination database is opened. If you want to execute the DBCC CHECKDB statement to identify consistency errors in the self-managed database, we recommend that you select Synchronous DBCC. This way, the destination database takes more time to open, and the CreateMigrateTask operation applies the parameter setting `CheckDBMode = SyncExecuteDBCheck` when it is called. |

8.  In the message that appears, click **OK**.


Wait until the migration task is completed. You can click **Refresh** to view the latest status of the migration task.

## Import differential or log backup files

After the full backup file of the self-managed database is uploaded to the OSS bucket, you must upload the differential or log backup files.

1.  Log on to the [ApsaraDB RDS console](https://rdsnew.console.aliyun.com/).

2.  In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Backup and Restoration**. On the page that appears, click **Backup Data Upload History**.

5.  Find the destination database and click **Upload Incremental Files**. In the dialog box that appears, configure the required parameters, select the differential or log backup file that you want to upload, and then click **OK**.

    **Note:**

    -   If you have multiple log backup files, you can use the same method to upload these files one by one.
    -   Make sure that the size of the last log backup file is less than or equal to 500 MB. This way, the time required for incremental migration is minimized.
    -   Before you back up the last log file, you must stop writing data to the self-managed database. Otherwise, data may be inconsistent between the self-managed and destination databases after migration.
    ![](../images/p4345.png)


## Open the destination database

After you upload all the backup files to the OSS bucket, the destination database is in the In Recovery or Restoring state. If your RDS instance runs the High-availability Edition, the destination database is in the In Recovery state. If your RDS instance runs the Basic Edition, the destination database is in the Restoring state. In these states, you cannot perform read or write operations on the destination database. Before you can perform read and write operations, you must open the destination database.

1.  Log on to the [ApsaraDB RDS console](https://rdsnew.console.aliyun.com/).

2.  In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Backup and Restoration**. On the page that appears, click **Backup Data Upload History**.

5.  Find the destination database and click **Open Database**.

    ![](../images/p4346.png)

6.  In the dialog box that appears, select a consistency check mode and click **OK**.

    **Note:** The system provides the following consistency check modes:

    -   Asynchronous DBCC: The DBCC CHECKDB statement is executed after the destination database is opened. This reduces the time to open the destination database and minimizes the downtime of your application. This mode is suitable for databases that contain a large volume of data because the execution is time-consuming in this scenario. If your application can tolerate only a short downtime and the execution result of the DBCC CHECKDB statement does not affect your business, we recommend that you select Asynchronous DBCC. This way, the CreateMigrateTask operation applies the parameter setting `CheckDBMode = AsyncExecuteDBCheck` when it is called.
    -   Synchronous DBCC: The DBCC CHECKDB statement is executed when the destination database is opened. If you want to execute the DBCC CHECKDB statement to identify consistency errors in the self-managed database, we recommend that you select Synchronous DBCC. This way, the destination database takes more time to open, and the CreateMigrateTask operation applies the parameter setting `CheckDBMode = SyncExecuteDBCheck` when it is called.

## View the details about the uploaded backup files

If you want to view the details about the uploaded backup files, perform the following operations: Open the **Backup and Restoration** page. Click the **Backup Data Upload History** tab. Find the destination database and click **View File Details**. In the dialog box that appears, view the details about the uploaded backup files.

![](../images/p4348.png)

## Common errors

For more information about common errors that occur during the migration of full backup data, see [Migrate full backup data to ApsaraDB RDS for SQL Server 2012, 2014, 2016, 2017, or 2019](/intl.en-US/RDS SQL Server Database/Data migration/Migrate data from a user-created database to an RDS SQL Server database/Migrate full backup data to ApsaraDB RDS for SQL Server 2012,2014, 2016, 2017, or 2019.mdsection_4rt_0ay_hbh). During the migration of incremental backup data, you may encounter the following errors:

-   The destination database cannot be opened.
    -   Error message: Failed to open database xxx.
    -   Cause: You have enabled some advanced features in the self-managed database, but the features are not supported by your RDS instance. Assume that the self-managed database runs an SQL Server Enterprise Edition and your RDS instance runs an SQL Server Web edition. If you have enabled the data compression and partition features in the self-managed database, the error message is returned when you open the destination database.
    -   Solution:
        -   Disable the advanced features in the self-managed database, back up data again, and migrate the data by using OSS.
        -   Purchase an RDS instance that runs the same SQL Server edition as the self-managed database.
-   The log sequence numbers \(LSNs\) in the backup chain are not consecutive.
    -   Error message: The log in this backup set begins at LSN XXX, which is too recent to apply to the database.RESTORE LOG is terminating abnormally.
    -   Cause: For SQL Server databases, differential and log backup files must be restored in compliance with the LSNs. Otherwise, the error message is returned.
    -   Solution: Restore the differential and log backup files in compliance with the LSNs.
-   Execution of DBCC CHECKDB in asynchronous mode fails.
    -   Error message: asynchronously DBCC checkdb failed: CHECKDB found 0 allocation errors and 2 consistency errors in table 'XXX' \(object ID XXX\).
    -   Cause: After you migrate data to your RDS instance with Asynchronous DBCC selected, the system executes the DBCC CHECKDB statement. Consistency errors are found in the self-managed database.
    -   Solution:
        -   Execute the following statement in the destination database:

            ```
            DBCC CHECKDB (DBName,REPAIR_ALLOW_DATA_LOSS)
            ```

            **Note:** If you use this statement to fix the error, data may be lost.

        -   Execute the following statement in the self-managed database to fix the error and migrate the incremental backup data again:

            ```
            DBCC CHECKDB (DBName,REPAIR_ALLOW_DATA_LOSS)
            ```

-   The full backup file does not meet the requirements.
    -   Error message: Backup set \(xxx\) is a Database FULL backup, we only accept transaction log or differential backup.
    -   Cause: After the full backup file is migrated, you can select only differential or log backup files for migration. If you select the full backup file again, the error message is returned.
    -   Solution: Select a differential or log backup file for migration.
-   The number of self-managed databases that you want to migrate exceeds the upper limit.
    -   Error message: The database \(xxx\) migration failed due to databases count limitation.
    -   Cause: If the number of self-managed databases that you want to migrate exceeds the upper limit, the error message is returned.
    -   Solution: Migrate excess databases to another RDS instance or delete unnecessary databases from the current RDS instance.

## Related operations

|Operation|Description|
|---------|-----------|
|[Create a migration task](/intl.en-US/API Reference/Migrate SQL Server to the cloud/Create a migration task.md)|Creates a migration task to restore backup files from an OSS bucket to an ApsaraDB RDS instance.|
|[Open the database to which backup data is migrated](/intl.en-US/API Reference/Migrate SQL Server to the cloud/Open the database to which backup data is migrated.md)|Opens the database to which backup data is migrated on an ApsaraDB RDS instance.|
|[Query migration tasks](/intl.en-US/API Reference/Migrate SQL Server to the cloud/Query migration tasks.md)|Queries tasks that migrate backup data to an ApsaraDB RDS instance.|
|[t8162.md\#](/intl.en-US/API Reference/Migrate SQL Server to the cloud/Query backup data files of migration task.md)|Queries the details about backup files that a task migrates to an ApsaraDB RDS instance.|

