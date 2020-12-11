# Query data from the remote backup files of an ApsaraDB RDS for MySQL instance

In most cases, when you query data from the remote backup files of an ApsaraDB RDS for MySQL instance, Alibaba Cloud needs to restore the data of the remote backup files to a new RDS instance. This includes several processes: initialize the new RDS instance, copy the remote backup files to the new RDS instance, and restore data from the remote backup files to the new RDS instance. These processes are complex and time-consuming. This topic describes how to query data in real time from remote backup files without the need to restore these files.

-   An RDS instance is created. This instance is known as the source RDS instance. For more information, see [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md).
-   Data Lake Analytics \(DLA\) is activated. For more information, see [Activate Data Lake Analytics]().
-   Database Backup \(DBS\) is activated, and a backup schedule is created. For more information, see [Create a backup schedule](~~65909~~).

    **Note:**

    -   The backup schedule must reside in a region that is different from the region of the source RDS instance. In addition, the region of the backup schedule must support DLA.
    -   The Database Type parameter must be set to MySQL for the backup schedule.
    -   The Backup Method parameter must be set to Logical Backup for the backup schedule.

## Scenario

Most of the traditional remote backup solutions compress the backup files that are generated on the source RDS instance, and then store the backup files to a different region. This brings challenges to the management of these backup files. In addition, the need to query historical backup files decreases as more time elapses. The storage of these historical backup files causes a waste of storage resources. The remote backup solution in this topic allows you to query data from remote backup files at high speeds and low costs.

-   DBS supports automatic management of remote backup files. It stores backup files to OSS buckets of various storage classes, such as Infrequent Access \(IA\) and Archive, based on how often the backup files are queried.

    **Note:** For more information about OSS storage classes, see [Overview](/intl.en-US/Developer Guide/Storage classes/Overview.md).

-   DLA supports real-time queries from full backup files. This relieves the need to restore data and reduces costs.

## Technical architecture

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0984884061/p58448.png)

## Precautions

-   DLA supports real-time queries only from the backup files that DBS generates for ApsaraDB RDS for MySQL instances.
-   DLA supports real-time queries only from full backup files. It does not support real-time queries from incremental backup files.
-   DLA must reside in the same region as the OSS buckets that store backup files.
-   DLA supports real-time queries only from logical backup files.

## Procedure

1.  Configure a backup schedule that is used to back up databases from the source RDS instance on DBS.

    1.  Log on to the [DBS console](https://dbs.console.aliyun.com/#/home/).
    2.  In the left-side navigation pane, click **Backup Schedules**.
    3.  In the top navigation bar, select the region where the backup schedule resides.
    4.  Find the backup schedule and in the Actions column click **Configure Backup Schedule**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0675564061/p58470.png)

    5.  Configure the Schedule Name parameter and the other parameters in the **Backup Source Information** and **Backup Destination Information** sections.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0675564061/p58472.png)

        |Category|Parameter|Description|
        |--------|---------|-----------|
        |Schedule Name|-|        -   DBS generates a name for each backup schedule. You do not need to specify a unique name.
        -   You can modify the name of the backup schedule based on your business requirements. We recommend that you specify an informative name that helps identify the backup schedule. |
        |Backup Source Information|Backup Mode|The type of backup that you want to perform. Default value: Logical Backup.|
        |Database Location|The location of the databases that you want to back up. Select **RDS Instance**.|
        |RDS Instance ID|The ID of the source RDS instance. **Note:** The source RDS instance and the backup schedule reside in different regions. Therefore, you can specify the **RDS Instance ID** parameter only after you specify the **Instance Region** parameter. |
        |Instance Region|The region where the source RDS instance resides.|
        |Database Account|The username of the account that is authorized to manage the specified databases on the source RDS instance.|
        |Password|The password of the account that is authorized to manage the specified databases on the source RDS instance.|
        |SSL Encryption|The type of connection that you want to establish. Select **Non-encrypted** or **SSL-encrypted**. **Note:** Before you configure the backup schedule, you must enable SSL encryption for the source RDS instance. This applies if you want to select the SSL-encrypted option. For more information, see [Configure SSL encryption on an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure SSL encryption on an ApsaraDB RDS for MySQL instance.md). |
        |Backup Destination Information|Backup Storage Type|        -   DBS generates an OSS bucket name for each backup schedule.
        -   You can modify the OSS bucket name based on your business requirements. We recommend that you specify an informative name that helps identify the OSS bucket. |
        |Storage Encryption|The type of storage that you want to use. Select **Non-encrypted**, **Encrypted**, or KMS Encrypted. **Note:** If you select the Encrypted or KMS Encrypted option, DBS encrypts the backup files by using AES 256. |

    6.  Click **Test Connection**. When Test Passed appears, click **Next**.

        **Note:** After you click Test Connection, DBS creates an IP address whitelist on the source RDS instance. The IP address whitelist contains the Classless Inter-Domain Routing \(CIDR\) block of the DBS server.

    7.  Select databases and tables from the **Available** section, move them to the **Selected** section, and then click **Next**.
    8.  Configure the backup time and click **Next**. In this step, you can set the Full-scale Backup Frequency parameter to **Periodic Backup** or **Single Backup**.
    9.  Configure the lifecycle and click **Precheck**.

        **Note:** For more information about how to configure the parameters in the Configure Backup Time and Edit Lifecycle steps, see [Configure a backup schedule](~~59609~~).

    10. After the backup task passes the precheck, click **Start Task**.
    11. Wait until the backup is complete.
2.  Configure the root account, endpoint, and OSS access permissions on DLA.

    -   For more information about how to configure an endpoint, see [Create endpoints](~~107696~~).
    -   To configure OSS access permissions, perform the following steps:

        **Note:** If OSS access permissions have been configured, you can skip these steps.

        1.  Log on to the [DLA console](https://datalakeanalytics.console.aliyun.com/overview).
        2.  In the left-side navigation pane, choose **Data Lake Management** \> **Metadata management**.
        3.  Click **Create Schema**.
        4.  In the OSS section, click **Create By Wizard**.
        5.  On the Cloud Resource Access Authorization page, click **Confirm Authorization Policy**.
3.  Create a schema on DBS.

    1.  Log on to the [DBS console](https://dbs.console.aliyun.com/#/home/).
    2.  In the left-side navigation pane, click **Backup Schedules**.
    3.  Find the backup schedule that you want to use. Then, click the ID of the backup schedule in the **Schedule ID/Name** column or click **Manage** in the Actions column.
    4.  In the left-side navigation pane, choose **Backup Tasks** \> **Full Data**.
    5.  Find the backup set that you want to use, and click **Query Backup Set** in the Actions column. In the Query Backup Data message, click **OK**.

        **Note:** After you click **OK**, DLA creates a schema for the backup set.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1675564061/p58495.png)

4.  Query full backup data from DBS.

    1.  Log on to the [DLA console](https://datalakeanalytics.console.aliyun.com/overview).
    2.  In the left-side navigation pane, choose **Serverless SQL** \> **SQL access point**.
    3.  On the **SQL access point** page, click **Log on in DMS**.
    4.  In the Login instance dialog box, enter the information that is used to log on to the source RDS instance and click **Login**.

        **Note:** DMS automatically specifies the **Database type**, **Instance Area**, and **Connection string address**. You must confirm the parameter settings and enter the username and password of the specified account.

    5.  Execute the following SQL statements on both DLA and the source RDS instance to check whether the data volume on DLA is consistent with the data volume on the source RDS instance:

        ```
        select 'bill' as tableName ,count(id) as countNumber from `bill`
        union ALL
        select 'dim_code_desc' as tableName ,count(id) as countNumber from `dim_code_desc` ;
        ```

        ![](../images/p58506.png "Data volume on the source RDS instance")

        ![](../images/p58507.png "Data volume on DLA")

    6.  Execute the following SQL statement on DLA to run a multi-table join query:

        ```
        select  t.* from dim_code_desc   as t1,  BILL t
        where   t1.id= t.id
        and t1.code_id like '9%';
        ```

        ![](../images/p58508.png "Multi-table join query on DLA")

        Run a multi-table join query on the source RDS instance. Then, compare the query results that you obtain from DLA and the source RDS instance.

        ![](../images/p58509.png "Multi-table join query on the source RDS instance")

        Verify that the query result on DLA is consistent with that on the source RDS instance.

        If you use a traditional remote backup solution, Alibaba Cloud needs to clone an RDS instance by using the full backup data of the source RDS instance and configure an IP address whitelist. In this case, a query requires about 1 hour, and the query process is more complicated. The remote backup solution in this topic relieves the need to restore data. In addition, this solution allows you to check for and recover a small volume of data that is accidentally deleted.


