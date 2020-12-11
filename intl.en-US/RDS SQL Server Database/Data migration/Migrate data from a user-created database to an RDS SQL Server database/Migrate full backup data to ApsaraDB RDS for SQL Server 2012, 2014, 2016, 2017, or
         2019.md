# Migrate full backup data to ApsaraDB RDS for SQL Server 2012, 2014, 2016, 2017, or 2019

This topic describes how to migrate full backup data of a self-managed SQL Server database to an ApsaraDB RDS for SQL Server instance by using an Object Storage Service \(OSS\) bucket and a full backup file.

-   Your RDS instance runs one of the following SQL Server versions and RDS editions:

    -   SQL Server 2017 EE on RDS Cluster Edition
    -   SQL Server 2012 SE, 2012 EE, 2014 SE, 2016 SE, 2016 EE, 2017 SE, and 2019 SE on RDS High-availability Edition
    -   SQL Server 2012 EE Basic, 2012 Web, and 2016 Web on RDS Basic Edition
    **Note:** For more information about how to migrate full backup data to an RDS instance that runs SQL Server 2008 R2 on RDS High-availability Edition, see [Migrate full backup data to ApsaraDB RDS for SQL Server 2008 R2](/intl.en-US/RDS SQL Server Database/Data migration/Migrate data from a user-created database to an RDS SQL Server database/Migrate full backup data to ApsaraDB RDS for SQL Server 2008 R2.md).

-   The remaining storage space of your RDS instance is sufficient. If the space is insufficient, you must increase it before migration.
-   The destination database on your RDS instance has a different name from the self-managed database.
-   A privileged account is created for your RDS instance. For more information, see [Create accounts and databases for an ApsaraDB for RDS instance running SQL Server 2012, 2016, 2017 SE, or 2019](/intl.en-US/RDS SQL Server Database/Quick start/Creating accounts and databases/Create accounts and databases for an ApsaraDB for RDS instance running SQL Server
         2012, 2016, 2017 SE, or 2019.md).
-   The OSS bucket used to store the full backup file resides in the same region as your RDS instance. For more information about how to create an OSS Bucket, see [Create buckets](/intl.en-US/Quick Start/Create buckets.md).
-   The DBCC CHECKDB statement is executed, and the execution result indicates that no allocation errors or consistency errors occur.

    **Note:** If no allocation errors or consistency errors occur, the following execution result is returned:

    ```
    ...
    CHECKDB found 0 allocation errors and 0 consistency errors in database 'xxx'.
    DBCC execution completed. If DBCC printed error messages, contact your system administrator.
    ```


## Precautions

-   This solution allows you to migrate the full backup file of only one self-managed database at a time. If you want to migrate the full backup files of multiple or all self-managed databases at a time, we recommend that you use the instance-level migration solution. For more information, see [Migrate data from an on-premises SQL Server instance to an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Data migration/Migrate data from a user-created database to an RDS SQL Server database/Migrate data from an on-premises SQL Server instance to an ApsaraDB RDS for SQL Server instance.md).
-   If the SQL Server version of the self-managed database is later than that of your RDS instance, you cannot migrate the full backup file of the self-managed database to your RDS instance. For example, if the self-managed database runs SQL Server 2016 and your RDS instance runs SQL Server 2012, you cannot migrate the full backup file of the self-managed database to your RDS instance.
-   Differential or log backup files are not supported.
-   The names of full backup files cannot contain special characters, such as at signs \(@\) and vertical bars \(\|\). If the file names contain special characters, the migration fails.
-   After the service account of your RDS instance is granted the access permission on the OSS bucket, the system creates a role named **AliyunRDSImportRole** in RAM. Do not modify or delete this role. If you have modified or deleted this role, you cannot download the full backup file when you migrate data to your RDS instance. In this case, you must re-authorize the service account of your RDS instance.
-   Before the migration is complete, do not delete backup files from the OSS bucket. If you delete the backup files before the migration is complete, the migration fails.
-   The names of backup files can be suffixed only with bak, diff, trn, or log. If you do not use the script in this topic to generate a backup file, you must name the backup file with one of the following suffixes:
    -   bak: indicates a full backup file.
    -   diff: indicates a differential backup file.
    -   trn and log: indicate a log backup file.

## Back up the self-managed database

**Note:** Before you perform the full backup, stop writing data to the self-managed database. The data written during the backup process is not backed up.

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

After the self-managed database is backed up, you must upload the full backup file to your OSS bucket. The following methods are available for uploading:

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
    |**Database Name**|Enter the name of the destination database on your RDS instance. The destination database stores the data that is migrated from the self-managed database. The name can be different from the name of the self-managed database.**Note:** The name of the destination database must meet the requirements of open source SQL Server. |
    |**OSS Bucket**|Select the OSS bucket that stores the backup files.|
    |**OSS Subfolder Name**|Enter the name of the OSS bucket folder that stores the backup files.|
    |**OSS File**|Click the search icon to search for a backup file by using the prefix-based fuzzy match. The system displays the name, size, and update time of the backup file. Select the backup file that you want to upload to the OSS bucket.|
    |**Cloud Migration Method**|    -   Immediate Access \(Full Backup\): Select this option if only a full backup file is available. For this example, select **Immediate Access \(Full Backup\)**. This way, the CreateMigrateTask operation applies the parameter settings `BackupMode = FULL` and `IsOnlineDB = True` when it is called.
    -   Access Pending \(Incremental Backup\): Select this operation if log and differential backup files are also available. If you select this option, the CreateMigrateTask operation applies the parameter settings `BackupMode = UPDF` and `IsOnlineDB = False` when it is called. |
    |**Consistency Check Mode**|    -   Asynchronous DBCC: The DBCC CHECKDB statement is executed after the destination database is opened. This reduces the time to open the destination database and minimizes the downtime of your application. This mode is suitable for databases that contain a large volume of data because the execution is time-consuming in this scenario. If your application can tolerate only a short downtime and the execution result of the DBCC CHECKDB statement does not affect your business, we recommend that you select Asynchronous DBCC. This way, the CreateMigrateTask operation applies the parameter setting `CheckDBMode = AsyncExecuteDBCheck` when it is called.
    -   Synchronous DBCC: The DBCC CHECKDB statement is executed when the destination database is opened. If you want to execute the DBCC CHECKDB statement to identify consistency errors in the self-managed database, we recommend that you select Synchronous DBCC. This way, the destination database takes more time to open, and the CreateMigrateTask operation applies the parameter setting `CheckDBMode = SyncExecuteDBCheck` when it is called. |

8.  In the message that appears, click **OK**.


Wait until the migration task is completed. You can click **Refresh** to view the latest status of the migration task. If the migration fails, fix the error based on the message displayed in the Task Description column. For more information, see [Common errors](#section_4rt_0ay_hbh).

## View the migration task

If you want to view the details about the migration task, perform the following operations: Open the **Backup and Restoration** page. Click the **Backup Data Upload History** tab. The system shows the migration tasks from the last week.

## Common errors

Each record of a migration task contains a task description, which helps you identify the error cause and fix the error. The following list describes common errors:

-   A database with the same name as the self-managed database exists on your RDS instance.
    -   Error message: The database \(xxx\) is already exist on RDS, please backup and drop it, then try again.
    -   Cause: For data security purposes, ApsaraDB RDS for SQL Server forbids the migration if the self-managed database is named the same as an existing database on your RDS instance.
    -   Solution: If you want to overwrite an existing database on your RDS instance, back up the existing database, delete it from your RDS instance, and then migrate the backup data to your RDS instance.
-   A differential backup file is used.
    -   Error message: Backup set \(xxx.bak\) is a Database Differential backup, we only accept a FULL Backup.
    -   Cause: The file that you upload is a differential backup file. It is not a full backup file. The migration solution for full backup data supports only full backup files.
-   A log backup file is used.
    -   Error message: Backup set \(xxx.trn\) is a Transaction Log backup, we only accept a FULL Backup.
    -   Cause: The file that you upload is a log backup file. It is not a full backup file. The migration solution for full backup data supports only full backup files.
-   The backup file fails the verification.
    -   Error message: Failed to verify xxx.bak, backup file was corrupted or newer edition than RDS.
    -   Cause: The backup file is damaged, or the self-managed database runs a higher SQL Server version than your RDS instance. For example, if the self-managed database runs SQL Server 2016 and your RDS instance runs SQL Server 2012, the error message is returned.
    -   Solution: If the backup file is damaged, perform a full backup on the self-managed database again. If the database engine version is not satisfied, select an RDS instance that runs the same as or a higher version than the self-managed database.
-   Execution of DBCC CHECKDB fails.
    -   Error message: DBCC checkdb failed.
    -   Cause: Allocation errors or consistency errors occur in the self-managed database.
    -   Solution: Execute the following statement in the self-managed database:

        **Note:** If you use this statement to fix the error, data may be lost.

        ```
        DBCC CHECKDB (DBName, REPAIR_ALLOW_DATA_LOSS) WITH NO_INFOMSGS, ALL_ERRORMSGS
        ```

-   The remaining storage space of your RDS instance is insufficient. \(1\)
    -   Error message: Not Enough Disk Space for restoring, space left \(xxx MB\) < needed \(xxx MB\).
    -   Cause: The remaining storage space of your RDS instance is insufficient to restore the backup file.
    -   Solution: Increase the storage space of your RDS instance.
-   The remaining storage space of your RDS instance is insufficient. \(2\)
    -   Error message: Not Enough Disk Space, space left xxx MB < bak file xxx MB.
    -   Cause: The remaining storage space of your RDS instance is smaller than the size of the backup file.
    -   Solution: Increase the storage space of your RDS instance.
-   No privileged account exists.
    -   Error message: Your RDS doesn't have any init account yet, please create one and grant permissions on RDS console to this migrated database \(XXX\).
    -   Cause: No privileged account is created for your RDS instance, and the database permissions are not granted to any account. However, the backup file has been restored to your RDS instance, and the migration task is successful.
    -   Solution: Create the privileged account for your RDS instance. For more information, see [Create accounts and databases for an ApsaraDB for RDS instance running SQL Server 2012, 2016, 2017 SE, or 2019](/intl.en-US/RDS SQL Server Database/Quick start/Creating accounts and databases/Create accounts and databases for an ApsaraDB for RDS instance running SQL Server
         2012, 2016, 2017 SE, or 2019.md).

## Related operations

|Operation|Description|
|---------|-----------|
|[Create a migration task](/intl.en-US/API Reference/Migrate SQL Server to the cloud/Create a migration task.md)|Creates a migration task to restore backup files from an OSS bucket to an ApsaraDB RDS instance.|
|[Open the database to which backup data is migrated](/intl.en-US/API Reference/Migrate SQL Server to the cloud/Open the database to which backup data is migrated.md)|Opens the database to which backup data is migrated on an ApsaraDB RDS instance.|
|[Query migration tasks](/intl.en-US/API Reference/Migrate SQL Server to the cloud/Query migration tasks.md)|Queries tasks that migrate backup data to an ApsaraDB RDS instance.|
|[t8162.md\#](/intl.en-US/API Reference/Migrate SQL Server to the cloud/Query backup data files of migration task.md)|Queries the details about backup files that a task migrates to an ApsaraDB RDS instance.|

