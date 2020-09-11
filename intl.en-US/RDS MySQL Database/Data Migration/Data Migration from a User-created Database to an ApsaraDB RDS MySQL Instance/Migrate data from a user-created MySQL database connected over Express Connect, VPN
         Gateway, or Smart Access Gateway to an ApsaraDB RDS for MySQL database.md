# Migrate data from a user-created MySQL database connected over Express Connect, VPN Gateway, or Smart Access Gateway to an ApsaraDB RDS for MySQL database

This topic describes how to migrate data from a user-created MySQL database that is connected over Express Connect, VPN Gateway, or Smart Access Gateway to an ApsaraDB RDS for MySQL database by using Data Transmission Service \(DTS\). DTS supports schema migration, full data migration, and incremental data migration. To migrate data from a user-created MySQL database, you can select all of the supported migration types to ensure service continuity.

-   The version of the user-created MySQL database is 5.1, 5.5, 5.6, 5.7, or 8.0.
-   The available storage space of the destination ApsaraDB RDS for MySQL database is larger than the total space of the data in the user-created MySQL database.
-   The on-premises network to which the user-created MySQL database belongs is connected to Alibaba Cloud over Express Connect, VPN Gateway, or Smart Access Gateway.

    **Note:** For more information, see [Connect to local IDCs]().


## Precautions

-   DTS uses read and write resources of the source and destination databases during full data migration. This may increase the database load. If the database performance is unfavorable, the specification is low, or the data volume is large, database services may become unavailable. For example, DTS occupies a large amount of read and write resources in the following cases: a large number of slow SQL queries are performed on the source database, the tables have no primary keys, or a deadlock occurs in the destination database. Before you migrate data, evaluate the performance of the source and destination databases. We recommend that you migrate data during off-peak hours. For example, you can migrate data when the CPU usage of the source and destination databases is less than 30%.
-   The source database must have PRIMARY KEY or UNIQUE constraints and all fields must be unique. Otherwise, duplicate data may exist in the destination database.
-   DTS uses the `ROUND(COLUMN,PRECISION)` function to retrieve values from columns of the float or double data type. If the precision is not specified, DTS sets the precision for the float data type to 38 digits and the precision for the double data type to 308 digits. You must check whether the precision settings meet your business requirements.
-   DTS automatically creates a destination database in the ApsaraDB RDS for MySQL instance. However, if the name of the source database is invalid, you must manually create a database in the ApsaraDB RDS for MySQL instance before you configure the data migration task.

    **Note:** For more information about how to create a database and the database naming conventions, see [Create databases and accounts](https://www.alibabacloud.com/help/doc-detail/96105.htm).

-   DTS automatically resumes a failed data migration task. Before you switch your workloads to the destination database, stop or release the data migration task. Otherwise, the data in the source database will overwrite the data in the destination database after the task is resumed.

## Billing

|Migration type|Instance configurations|Internet traffic|
|--------------|-----------------------|----------------|
|Schema migration and full data migration|Free of charge.|Charged only when data is migrated from Alibaba Cloud over the Internet. For more information, see [Pricing]().|
|Incremental data migration|Charged. For more information, see [Pricing]().|

## Migration types

-   Schema migration

    DTS migrates the schemas of the required objects to the destination instance. DTS supports schema migration for the following types of objects: table, view, trigger, stored procedure, and function.

    **Note:**

    -   During schema migration, DTS changes the value of the SECURITY attribute in views, stored procedures, and functions from DEFINER to INVOKER.
    -   DTS does not migrate user information. Before a user can call views, stored procedures, and functions of the destination database, you must grant the read/write permissions to the user.
-   Full data migration

    DTS migrates historical data of the required objects from the user-created MySQL database to the destination database in the ApsaraDB RDS for MySQL instance.

    **Note:** During full data migration, concurrent INSERT operations cause fragmentation in the tables of the destination instance. After full data migration is complete, the tablespace of the destination instance is larger than that of the source database.

-   Incremental data migration

    After full data migration is complete, DTS retrieves binary log files from the user-created MySQL database. Then, DTS synchronizes incremental data from the user-created MySQL database to the destination ApsaraDB RDS for MySQL instance. Incremental data migration allows you to ensure service continuity when you migrate data from a user-created MySQL database to Alibaba Cloud.


## SQL operations that can be synchronized during incremental data migration

|Operation type|SQL statements|
|--------------|--------------|
|DML|INSERT, UPDATE, DELETE, and REPLACE|
|DDL|-   ALTER TABLE and ALTER VIEW
-   CREATE FUNCTION, CREATE INDEX, CREATE PROCEDURE, CREATE TABLE, and CREATE VIEW
-   DROP INDEX and DROP TABLE
-   RENAME TABLE
-   TRUNCATE TABLE |

## Permissions required for database accounts

|Database|Schema migration|Full data migration|Incremental data migration|
|:-------|:---------------|:------------------|:-------------------------|
|User-created MySQL database|The SELECT permission|The SELECT permission|The REPLICATION SLAVE, REPLICATION CLIENT, SHOW VIEW, and SELECT permissions|
|ApsaraDB RDS for MySQL instance|The read/write permissions|The read/write permissions|The read/write permissions|

For more information about how to create and authorize a database account, see the following topics:

-   [Create an account for a user-created MySQL database and configure binary logging]() for a user-created MySQL database
-   [Create an account for an RDS for MySQL instance](https://www.alibabacloud.com/help/doc-detail/96089.htm) and [Change the permissions of an account for an RDS for MySQL instance](https://www.alibabacloud.com/help/doc-detail/96101.htm)

## Preparations

1.  [Create an account for a user-created MySQL database and configure binary logging]().

2.  [Allow DTS to access the network to which Express Connect, VPN Gateway, or Smart Access Gateway belongs]().


## Procedure

1.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/).

2.  In the left-side navigation pane, click **Data Migration**.

3.  At the top of Migration Tasks the page, select the region where the destination cluster resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9840359951/p50439.png)

4.  In the upper-right corner of the page, click **Create Migration Task**.

5.  Configure the information about the source and destination databases for the data migration task.

    ![Configure source and destination databases](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9720359951/p63500.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |N/A|Task Name|DTS automatically generates a task name. We recommend that you use an informative name for easy identification. You do not need to use a unique task name.|
    |Source Database|Instance Type|Select **User-Created Database Connected Over Express Connect, VPN Gateway, or Smart Access Gateway**.|
    |Instance Region|Select the region to which the VPC that is connected to Express Connect, VPN Gateway, or Smart Access Gateway belongs.|
    |Peer VPC|Select the VPC that is connected to Express Connect, VPN Gateway, or Smart Access Gateway.|
    |Database Type|Select **MySQL**.|
    |IP Address|Enter the endpoint that is used to connect to the user-created MySQL database.|
    |Port Number|Enter the service port number of the user-created MySQL database. The default port number is **3306**.|
    |Database Account|Enter the account for the user-created MySQL database. For more information about permissions required for the account, see [Permissions required for database accounts](#section_31k_oq1_w0z).|
    |Database Password|Enter the password for the database account. **Note:** After the source database parameters are specified, click **Test Connectivity** next to the **Database Password** parameter to verify whether the specified parameters are correct. If the source database parameters are correct, the **Test Passed** message is displayed, If the **Test Failed** message is displayed, click **Diagnose** in the **Test Failed** message. Modify the source database parameters as prompted. |
    |Destination Database|Instance Type|Select **RDS Instance**.|
    |Instance Region|Select the region where the destination RDS instance resides.|
    |RDS Instance ID|Select the ID of the destination RDS instance.|
    |Database Account|Enter the database account of the destination RDS instance. For more information about permissions required for the account, see [Permissions required for database accounts](#section_31k_oq1_w0z).|
    |Database Password|Enter the password for the database account. **Note:** After the destination database parameters are specified, click **Test Connectivity** next to the **Database Password** parameter to verify whether the specified parameters are correct. If the destination database parameters are correct, the **Test Passed** message is displayed. If the **Test Failed** message is displayed, click **Diagnose** in the **Test Failed** message. Modify the destination database parameters as prompted. |
    |Encryption|Select **Non-encrypted** or **SSL-encrypted**. If you want to select **SSL-encrypted**, you must enable SSL encryption for the RDS instance before configuring the data migration task. For more information, see [Configure SSL encryption for an RDS for MySQL instance](https://www.alibabacloud.com/help/doc-detail/96120.htm). **Note:** The **Encryption** parameter is available only in mainland China and Hong Kong\(China\). |

6.  In the lower-right corner of the page, click **Set Whitelist and Next**.

    **Note:** The CIDR blocks of DTS servers are automatically added to the whitelist of the destination ApsaraDB RDS for MySQL instance. This ensures that DTS servers can connect to the destination RDS instance.

7.  Configure migration types and objects.

    ![Configure Migration Types and Objects](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1920359951/p56880.png)

    |Item|Description|
    |:---|:----------|
    |Migration types|    -   To perform only full data migration, select **Schema Migration** and **Full Data Migration**.
    -   If you want to migrate data without business disruptions, select **Schema Migration**, **Full Data Migration**, and **Incremental Data Migration**.
 **Note:** If **Incremental Data Migration** is not selected, do not write data into the source database during full data migration. This ensures data consistency between the source and destination databases. |
    |Objects to be migrated|Select the objects to be migrated in the Available section and click ![>](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3457359951/p40698.png) icon to move them to the Selected section.

 **Note:**

    -   Objects to be migrated can be databases, tables, or columns.
    -   By default, the selected objects are not renamed after the migration. If you want to rename the objects that are migrated to the destination instance, you can use the object name mapping feature provided by DTS. For more information about how to use this feature, see [Object name mapping]().
    -   If you use the object name mapping feature for an object, objects that depend on the object may fail to be migrated. |

8.  Click **Precheck** on the lower right of the page.

    **Note:**

    -   A precheck is performed for a data migration task. A data migration task can be started only if it passes the precheck.
    -   If the precheck fails, click ![Note](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3457359951/p47468.png) icon corresponding to each failed item to view the details. Fix the problems as instructed and run the precheck again.
9.  After the precheck is passed, click **Next**.

10. On the Confirm Settings dialog box that appears, specify **Channel Specification** and select the **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.

11. Click **Buy and Start** to start the data migration task.

    -   Schema migration and full data migration

        Do not manually stop a migration task. Otherwise, data migrated to the destination database will be incomplete. Wait until the data migration task stops when it is complete.

    -   Schema migration, full data migration, and incremental data migration

        An incremental data migration task does not automatically end. You must manually end the migration task.

        **Note:** Select an appropriate time point to manually end the migration task. For example, you can end the migration task during off-peak hours or before you switch your workloads to the destination cluster.

        1.  When the task progress bar switches to **Incremental Data Migration** and the message **The migration task is not delayed** appears, stop writing new data to the source database for a few minutes. Then, the progress bar will show the latency of the **incremental data migration**.
        2.  When the status of **incremental data migration** changes to **The migration task is not delayed**, manually stop the migration task.

            ![Stop the incremental migration task](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2940359951/p47604.png)

12. Switch your workloads to the ApsaraDB RDS for MySQL instance.


