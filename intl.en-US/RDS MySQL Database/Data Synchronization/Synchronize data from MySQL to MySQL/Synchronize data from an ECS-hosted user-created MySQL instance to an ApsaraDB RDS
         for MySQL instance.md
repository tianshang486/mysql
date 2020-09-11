# Synchronize data from an ECS-hosted user-created MySQL instance to an ApsaraDB RDS for MySQL instance

This topic describes how to synchronize data from an ECS-hosted user-created MySQL instance to an ApsaraDB RDS for MySQL instance by using Alibaba Cloud Data Transmission Service \(DTS\). In this case, the user-created instance is the source instance, and the RDS instance is the destination instance.

## Prerequisites

-   The source instance runs MySQL 5.1, 5.5, 5.6, 5.7, or 8.0.
-   The destination instance is created. For more information, see [Create an ApsaraDB RDS for MySQL instance](https://www.alibabacloud.com/help/doc-detail/26117.htm).

## Precautions

-   DTS uses read and write resources of the source and destination databases during initial full data synchronization. This may increase the database load. If the database performance is unfavorable, the specification is low, or the data volume is large, database services may become unavailable. For example, DTS occupies a large amount of read and write resources in the following cases: a large number of slow SQL queries are performed on the source database, the tables have no primary keys, or a deadlock occurs in the destination database. Before synchronizing data, you must evaluate the performance of the source and destination databases. We recommend that you synchronize data during off-peak hours. For example, you can synchronize data when the CPU usage of the source and destination databases is less than 30%.
-   If you have selected one or more tables \(not a database\) for synchronization, do not use gh-ost or pt-online-schema-change to modify the tables during data synchronization. Otherwise, data synchronization may fail.

    **Note:** To avoid synchronization failure, you can use Data Management \(DMS\) to perform online DDL schema changes during data synchronization. For more information, see [Change the table schema without locking](https://www.alibabacloud.com/help/doc-detail/98373.htm).

-   The destination instance cannot reside in Zone A of the China \(Hong Kong\) region.
-   The destination instance must have an internal endpoint.
-   The source database must have PRIMARY KEY or UNIQUE constraints and all fields must be unique. Otherwise, duplicate data may exist in the destination database.
-   If concurrent INSERT statements are executed on the destination instance during an initial full data synchronization, tables on the destination instance are fragmented. As a result, after the initial full data synchronization is complete, the total size of tables on the destination instance is larger than the total size of tables on the source instance.

## Supported synchronization typologies

-   One-way one-to-one synchronization
-   One-way one-to-many synchronization
-   One-way many-to-one synchronization
-   One-way cascade synchronization
-   Two-way one-to-one synchronization

    **Note:** For more information about two-way synchronization, see [Configure two-way data synchronization between ApsaraDB RDS for MySQL instances]().


## Supported SQL statements

|Operation type|SQL statements|
|--------------|--------------|
|DML|INSERT, UPDATE, DELETE, and REPLACE|
|DDL|-   ALTER TABLE and ALTER VIEW
-   CREATE FUNCTION, CREATE INDEX, CREATE PROCEDURE, CREATE TABLE, and CREATE VIEW
-   DROP INDEX and DROP TABLE
-   RENAME TABLE
-   TRUNCATE TABLE |

## Limits

-   Incompatibility of triggers

    If the object you want to synchronize is a database and the database contains a trigger that updates the synchronized table, the synchronized data may be inconsistent. For example, the source database contains Table A and Table B. If a data record is inserted into Table A, a trigger inserts a data record into Table B. In this case, after an INSERT operation is performed on Table A in the source instance, the data in Table B becomes inconsistent between the source and destination instances.

    To avoid this situation, you must delete the trigger that is synchronized to the destination instance and select Table B as the object to be synchronized. For more information, see [Configure synchronization when triggers exist](https://www.alibabacloud.com/help/doc-detail/26655.htm).

-   Limits on RENAME TABLE operations

    RENAME TABLE operations may cause data inconsistency between the source and destination databases. For example, if only Table A needs to be synchronized and it is renamed Table B, Table B cannot be synchronized to the destination database. To avoid this situation, you can select the database to which Table A and Table B belong as the object when configuring the data synchronization task.


## Preparations

Before you configure a synchronization task, you must create an account and configure binary logging for the source instance. For more information, see [Create an account for a user-created MySQL database and configure binary logging]().

## Procedure

1.  Create a synchronization instance. For more information, see [Purchase a data synchronization instance]().

    **Note:** When you create a synchronization instance, you must select **MySQL** for both the Source Instance and Target Instance parameters. In addition, you must select **One-Way Synchronization** for the Synchronization Topology parameter.

2.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/).
3.  In the left-side navigation pane, click **Data Synchronization**.
4.  At the top of the Synchronization Tasks page, select the region where the destination instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4130359951/p50604.png)

5.  Find the synchronization instance that you created, and click **Configure Synchronization Channel** in the Actions column to configure a synchronization task.
6.  Enter the information of the source and destination instances.

    ![Configure the source and destination instances](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5030359951/p47056.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |N/A|Synchronization Task Name|The name of the synchronization task. DTS automatically generates a task name. We recommend that you specify an informative name for easy identification. You do not need to use a unique task name.|
    |Source Instance Details|Instance Type|The type of the source instance. Select **User-Created Database in ECS Instance**.|
    |Instance Region|The region to which the source instance belongs. The region was specified when you created the synchronization instance. You cannot change the region.|
    |ECS Instance ID|The ID of the ECS instance that hosts the source instance.|
    |Database Type|The database engine that the source instance runs. The database engine was specified when you created the synchronization instance. You cannot change the database engine. In this example, the database engine is **MySQL**.|
    |Port Number|The port that you use to log on to the source instance. The default port is **3306**.|
    |Database Account|The username of the account that you use to log on to the source instance. The account must have the permissions to execute REPLICATION SLAVE, REPLICATION CLIENT, and SELECT statements. The SELECT statement must be authorized on all of the required objects.|
    |Database Password|The password of the account that you use to log on to the source instance.|
    |Destination Instance Details|Instance Type|The type of the destination instance. Select **RDS Instance**.|
    |Instance Region|The region to which the destination instance belongs. The region was specified when you created the synchronization instance. You cannot change the region.|
    |Instance ID|The ID of the destination instance.|
    |Database Account|The username of the account that you use to log on to the destination instance. **Note:** If the destination instance runs **MySQL5.5** or **MySQL5.6**, the **Database Account** and **Database Password** parameters are not displayed. |
    |Database Password|The password of the account that you use to log on to the destination instance.|
    |Encryption|Specifies whether to enable encryption on the destination instance. Select **Non-encrypted** or **SSL-encrypted**. If you want to select **SSL-encrypted**, you must enable SSL encryption for the destination instance before you configure the synchronization task. For more information, see [Configure SSL encryption for an ApsaraDB RDS for MySQL instance](https://www.alibabacloud.com/help/doc-detail/96120.htm). **Note:** The **Encryption** parameter is available only for regions in mainland China and the Hong Kong \(China\) region. |

7.  In the lower-right corner of the page, click **Set Whitelist and Next**.
8.  Configure the synchronization policy and objects.

    ![Configure the synchronization policy and objects](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8030359951/p46145.png)

    |Parameter|Description|
    |:--------|:----------|
    |Processing Mode In Existed Target Table|    -   **Pre-check and Intercept**: checks whether the destination database contains tables that have the same names as tables in the source database. If the destination database does not contain tables that have the same names as tables in the source database, the precheck is passed. Otherwise, an error is returned during precheck and the data synchronization task cannot be started.

**Note:** If tables in the destination database have the same names as tables in the source database, and cannot be deleted or renamed, you can use the object name mapping feature. For more information, see [Specify the name of an object in the destination instance]().

    -   **Ignore**: skips the precheck for identical table names in the source and destination databases.

**Warning:** If you select **Ignore**, data consistency is not guaranteed and your business may be exposed to potential risks.

        -   If the source and destination databases have the same schema, and the primary key of a record in the destination database is the same as that in the source database, the record remains unchanged during initial data synchronization. However, the record is overwritten during incremental data synchronization.
        -   If the source and destination databases have different schemas, initial data synchronization may fail. In this case, only some columns are synchronized or the data synchronization task fails. |
    |Objects to be synchronized|Select objects from the Available section and click the ![Right arrow](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3457359951/p40698.png) icon to move the objects to the Selected section.

 You can select tables and databases as the objects to be synchronized.

 **Note:**

    -   If you select a database as the object to be synchronized, all schema changes in the database are synchronized to the destination database.
    -   After an object is synchronized to the destination database, the name of the object remains unchanged. You can change the name of an object in the destination instance by using the object name mapping feature provided by DTS. For more information about how to use this feature, see [Specify the name of an object in the destination instance](). |

9.  In the lower-right corner of the page, click **Next**.
10. Set the Initial Synchronization parameter.

    ![Advanced settings](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8030359951/p41055.png)

    -   During an initial synchronization, DTS synchronizes the schemas and data of the required objects from the source instance to the destination instance. The schemas and data are the basis for subsequent incremental synchronization.
    -   Initial synchronization is classified into initial schema synchronization and initial full data synchronization. In most cases, you need to select both **Initial Schema Synchronization** and **Initial Full Data Synchronization**.
11. In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   Before you can start the data synchronization task, a precheck is performed. You can start the data synchronization task only after the task passes the precheck.
    -   If the task fails to pass the precheck, click the ![Info icon](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3457359951/p47468.png) icon next to each failed item to view details. Troubleshoot the issues based on the causes and run the precheck again.
12. Close the Precheck dialog box after the following message is displayed: **The precheck is passed.** Then, the data synchronization task starts.
13. Wait until the initial synchronization is complete and the synchronization task switches to the **Synchronizing** state.

    You can view the status of the synchronization task on the Synchronization Tasks page.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5130359951/p41059.png)


