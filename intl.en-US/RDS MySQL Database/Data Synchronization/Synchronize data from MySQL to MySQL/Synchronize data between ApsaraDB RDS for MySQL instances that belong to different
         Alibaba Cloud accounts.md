# Synchronize data between ApsaraDB RDS for MySQL instances that belong to different Alibaba Cloud accounts

This topic describes how to synchronize data between ApsaraDB RDS for MySQL instances that belong to different Alibaba Cloud accounts by using Data Transmission Service \(DTS\).

## Prerequisites

-   The source and destination ApsaraDB RDS for MySQL instances for data synchronization are created. For more information, see [Create an RDS instance](https://www.alibabacloud.com/help/doc-detail/26117.htm).
-   The databases in the source and destination RDS instances are MySQL databases.
-   The source and destination ApsaraDB RDS for MySQL instances must have internal endpoints.

## Limits

-   DTS uses read and write resources of the source and destination databases during initial full data synchronization. This may increase the database load. If the database performance is unfavorable, the specification is low, or the data volume is large, database services may become unavailable. For example, DTS occupies a large amount of read and write resources in the following cases: a large number of slow SQL queries are performed on the source database, the tables have no primary keys, or a deadlock occurs in the destination database. Before synchronizing data, you must evaluate the performance of the source and destination databases. We recommend that you synchronize data during off-peak hours. For example, you can synchronize data when the CPU usage of the source and destination databases is less than 30%.
-   If you have selected one or more tables \(not a database\) for synchronization, do not use gh-ost or pt-online-schema-change to modify the tables during data synchronization. Otherwise, data synchronization may fail.

    **Note:** To avoid synchronization failure, you can use Data Management \(DMS\) to perform online DDL schema changes during data synchronization. For more information, see [Change the table schema without locking](https://www.alibabacloud.com/help/doc-detail/98373.htm).

-   You cannot synchronize data between ApsaraDB RDS for MySQL instances that reside in Zone A of the China \(Hong Kong\) region.
-   If the source database does not have primary keys or UNIQUE constraints, and fields are not required to be unique, duplicate data may exist in the destination database.
-   During initial full data synchronization, concurrent INSERT operations cause fragmentation in the tables of the destination instance. After initial full data synchronization, the tablespace of the destination instance is larger than that of the source instance.

## Supported synchronization topologies

-   One-way one-to-one synchronization
-   One-way one-to-many synchronization
-   One-way cascade synchronization
-   One-way many-to-one synchronization

For more information about synchronization topologies, see [Synchronization topologies]().

## SQL operations that can be synchronized

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

Set the Alibaba Cloud account that owns the destination RDS instance as a trusted account. This allows DTS to access the cloud resources of the Alibaba Cloud account that owns the source RDS instance. For more information, see [Configure RAM authorization for cross-account data migration and synchronization]().

**Note:** To authorize the Alibaba Cloud account that owns the destination instance, you must log on to the RAM console with the Alibaba Cloud account that owns the source instance. Then, you can create a data migration task or data synchronization task by using the Alibaba Cloud account that owns the destination instance.

## Procedure

1.  Purchase a data synchronization instance by using the Alibaba Cloud account that owns the destination RDS instance. For more information, see [Purchase a data synchronization instance]().

    **Note:** Select **MySQL** for both the source instance and the destination instance. Select **One-Way Synchronization** as the synchronization topology.

2.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/) with the Alibaba Cloud account that owns the destination RDS instance.
3.  In the left-side navigation pane, click **Data Synchronization**.
4.  At the top of the Synchronization Tasks page, select the region where the destination instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4130359951/p50604.png)

5.  Find the data synchronization instance and click **Configure Synchronization Channel** in the Actions column.
6.  Configure the source and destination instances.

    ![Configure the source and destination instances](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3030359951/p46227.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |N/A|Synchronization Task Name|DTS automatically generates a task name. We recommend that you use an informative name for easy identification. You do not need to use a unique task name.|
    |Source Instance Details|Instance Type|Select **RDS Instance**.|
    |Instance Region|The region of the source instance. The region is the same as the region that you selected when you purchased the data synchronization instance. You cannot change the value of this parameter.|
    |Apsara Stack Tenant Account ID of RDS Instance|Enter the ID of the Alibaba Cloud account that owns the source RDS instance. **Note:** Before you configure this parameter, click RDS Instances of Other Apsara Stack Accounts in the **Source Instance Details** section.

![Select an RDS instance that is owned by a different Alibaba Cloud account](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3030359951/p46232.png) |
    |Role Name|Enter the name of the RAM role that you configured earlier in [Preparations](#section_rdl_qrn_qhb).|
    |RDS Instance ID|Select the ID of the source RDS instance.|
    |Destination Instance Details|Instance Type|Select **RDS Instance**.|
    |Instance Region|The region of the destination instance. The region is the same as the region that you selected when you purchased the data synchronization instance. You cannot change the value of this parameter.|
    |Instance ID|Select the ID of the destination RDS instance.|
    |Database Account|Enter the database account for the destination RDS instance. **Note:** If the database engine of the destination RDS instance is **MySQL 5.5** or **MySQL 5.6**, you do not need to configure the **database account** or **database password**. |
    |Database Password|Enter the password for the database account.|
    |Encryption|Select **Non-encrypted** or **SSL-encrypted**. If you want to select **SSL-encrypted**, you must enable SSL encryption for the RDS instance before configuring the data synchronization task. For more information, see [Configure SSL encryption for an RDS for MySQL instance](https://www.alibabacloud.com/help/doc-detail/96120.htm). **Note:** The **Encryption** parameter is available only in mainland China and Hong Kong\(China\). |

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
10. Configure initial synchronization.

    ![Advanced settings](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8030359951/p41055.png)

    -   During initial synchronization, DTS synchronizes the schemas and data of the required objects from the source instance to the destination instance. The schemas and data are the basis for subsequent incremental synchronization.
    -   Initial synchronization includes initial schema synchronization and initial full data synchronization. You must select both **Initial Schema Synchronization** and **Initial Full Data Synchronization** in most cases.
11. In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   Before you can start the data synchronization task, a precheck is performed. You can start the data synchronization task only after the task passes the precheck.
    -   If the task fails to pass the precheck, click the ![Info icon](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3457359951/p47468.png) icon next to each failed item to view details. Troubleshoot the issues based on the causes and run the precheck again.
12. Close the Precheck dialog box after the following message is displayed: **The precheck is passed.**
13. Wait until the initial synchronization is complete and the data synchronization task is in the **Synchronizing** state.

    You can view the status of the data synchronization task on the Data Synchronization page.

    ![Status of the data synchronization task](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5130359951/p41059.png)


