# Migrate full backup data to RDS for SQL Server 2008 R2 {#concept_swt_smw_ydb .concept}

Instances of the SQL Server 2008 R2 version support easy data migration to the cloud database. You only have to back up all the data by using the official backup function of Microsoft your on-premises database, upload the backup file to the [Object Storage Service \(OSS\)](https://www.alibabacloud.com/help/doc-detail/31817.htm) of Alibaba Cloud, and then move the full amount of data to the specified RDS database through the RDS console. This feature takes advantage of Microsoft’s official backup and recovery program, realizes 100% compatibility, and is combined with the powerful capabilities of OSS. All these functions make it a highly efficient feature for data migration to the cloud database.

## Prerequisite {#section_z4d_hnw_ydb .section}

A target database has been created in RDS. For more information, see [Create databases and accounts for an RDS for SQL Server 2008 R2 instance](../../../../intl.en-US/Quick Start for SQL Server/Initial configuration/Creating accounts and databases/Create databases and accounts for an RDS for SQL Server 2008 R2 instance.md#).

**Note:** The name of the target database in RDS can be the same as that of the local database to be migrated.

## Billing details {#section_q1w_3nw_ydb .section}

When you migrate data to the cloud, no additional fees are charged for RDS but you must pay for OSS, as shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7997/15656791174362_en-US.png)

Figure description:

-   Uploading local data backup files to OSS is free of charge.
-   OSS storage can be changed if you store backup files on OSS. For more information, see [Pricing](https://www.alibabacloud.com/product/oss?spm=a3c0i.7990255.247275.8.7a40749en97oY9#pricing).
-   If you migrate backup files from OSS to RDS through an intranet, no extra fees are charged. If it is through the Internet, OSS charges for the Internet outbound traffic. For more information, see [Pricing](https://www.alibabacloud.com/product/oss?spm=a3c0i.7990255.247275.8.7a40749en97oY9#pricing).

    **Note:** The RDS instance and OSS bucket can connect to each other through an intranet only when they are located in the same region. Therefore, make sure that the backup files are uploaded to the bucket that is located in the same region as the target RDS instance.


## Procedure {#section_fm1_34w_ydb .section}

1.  Prepare the local database by completing the following steps:
    1.  Start the Microsoft SQL Server Management Studio \(SSMS\) client.
    2.  Log on to the database to be migrated.
    3.  Run the following commands to check the recover mode of the local database:

        ``` {#codeblock_n8m_hkx_75s}
        use master;
        go
        select name, case recovery_model
        when 1 then FULL
        when 2 then BULD_LOGGED
        when 3 then SIMPLE end model from sys.databases
        where name not in (master,tempdb,model,msdb);
        go
        ```

        Check the model value of the local database:

        -   If the model value is not FULL, go to Step iv.
        -   If the model value is FULL, go to Step v.
    4.  Run the following commands to set the recover mode of the source database to FULL 

        ``` {#codeblock_9n8_bzu_pws}
        ALTER DATABASE [dbname] SET RECOVERY FULL;
        go
        ALTER DATABASE [dbname] SET AUTO_CLOSE OFF;
        go
        ```

        **Note:** Setting the recover mode to FULL increases the number of SQL Server logs. Therefore, make sure there is sufficient disk space for the logs.

    5.  Run the following commands to back up the source database. This example uses filename.bak as the backup file name.

        ``` {#codeblock_cp6_4lm_wcf}
        use master;
        go
        BACKUP DATABASE [testdbdb] to disk =d:\backup\filename.bak WITH COMPRESSION,INIT;
        go
        ```

    6.  Run the following commands to verify integrity of the backup file.

        ``` {#codeblock_09w_lt1_zwh}
         USE master
         GO
         RESTORE FILELISTONLY 
           FROM DISK = ND:\Backup\filename.bak;
        ```

        Returned result description:

        -   If a result set is returned, the backup file is valid.
        -   If an error is returned, the backup file is invalid. In this case, back up the database again.
    7.  Run the following commands to recover the recover mode of the source database:

        ``` {#codeblock_hrk_6sk_wj3}
        ALTER DATABASE [dbname] SET RECOVERY SIMPLE;
        go
        ```

        **Note:** If you do not perform Step iv \(that is, the original recover mode of the database is FULL\), skip this step.

2.  Upload the local backup file to OSS and retrieve the file URL by completing the following steps:
    1.  Upload the backup file to OSS:
        -   For the procedure of uploading a file smaller than 5 GB, see [Upload an object](https://www.alibabacloud.com/help/doc-detail/31886.htm).
        -   For the procedure of uploading multiple files or a file larger than 5 GB, see [Multipart upload](https://www.alibabacloud.com/help/doc-detail/31850.htm). To perform this step on GUIs, see [ossbrowser](https://www.alibabacloud.com/help/doc-detail/61872.htm).
    2.  In the left-side navigation pane of the [OSS console](https://oss.console.aliyun.com/), select the bucket where the backup file belongs.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7997/15656791174363_en-US.png)

    3.  Select **Files**.
    4.  Click the name of the target backup file.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7997/15656791184364_en-US.png)

    5.  In the **Validity Period \(Seconds\)** field, change the validity period of the link. We recommend that you set the validity period to 28,800 seconds, namely, 8 hours.

        **Note:** When you migrate the backup file from OSS to RDS, the URL of the backup file is required. If the link validity period for the URL expires, the data migration fails. Therefore, we recommend that you set the validity period to the maximum value, which is 28,800s.

    6.  Click **Copy File URL**. The default URL is the Internet connection address of the file.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7997/15656791184365_en-US.png)

    7.  If you want to migrate data through the intranet, change the endpoint in the backup file URL to the intranet endpoint. The intranet endpoint varies with the network type and region. For more information, see [Access domain name and data center](https://www.alibabacloud.com/help/doc-detail/31837.htm).

        For example, if the backup file URL is `http://rdstest-yanhua.oss-cn-shanghai.aliyuncs.com/testmigraterds_20170906143807_FULL.bak?Expires=1514189963&OSSAccessKeyId=TMP.AQGVf994YTPfArSpw78uix2rdGBi-dPe_FzQSLwOLP7MVlR-XXXX`, change the Internet endpoint `oss-cn-shanghai.aliyuncs.com` in the URL to the intranet endpoint `oss-cn-shanghai-internal.aliyuncs.com`.

3.  Migrate the backup file from OSS to RDS by completing the following steps:
    1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
    2.  Select the region where the target instance is located.
    3.  Click the ID of the target instance to go to the Basic Information page.
    4.  In the left-side navigation pane, click **Databases** to go to the Databases page.
    5.  Find the target database and in the **Actions** column click **Migrate Backup Files from OSS**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7997/15656791184366_en-US.png)

    6.  In the Import Guide dialog box, read the prompt and click **Next** to go to the **Upload the backup files to** step.
    7.  Read the prompt and click **Next** to go to the **Import data** step.
    8.  In the **OSS URL of the Backup File** field, enter the backup file URL in OSS.

        **Note:** Currently, RDS supports only one cloud migration solution, that is, **One-time full backup file migration**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7997/15656791184367_en-US.png)

    9.  Click **OK**.
    10. In the left-side navigation pane, click **Data Migration to Cloud** to go to the page listing the tasks of migrating backup files from OSS to RDS.
    11. Find the target migration task. If **Tasks Status** is **Success**, the data is successfully migrated to the RDS database. If the migration task status does not change to **Success** after a long time, click View File Details**View File Details** next to the migration task to view the failure causes. After resolving the problems, perform the required steps to migrate the backup file again.

