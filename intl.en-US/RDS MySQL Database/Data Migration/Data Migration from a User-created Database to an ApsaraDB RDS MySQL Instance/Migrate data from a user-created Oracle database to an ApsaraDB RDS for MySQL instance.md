# Migrate data from a user-created Oracle database to an ApsaraDB RDS for MySQL instance

This topic describes how to migrate data from a user-created Oracle database to an ApsaraDB RDS for MySQL instance by using Data Transmission Service \(DTS\). DTS supports schema migration, full data migration, and incremental data migration. When you migrate data from a user-created Oracle database, you can select all of the supported migration types to ensure service continuity.

## Prerequisites

-   An Oracle database of version 9i, 10g, 11g, 12c, 18c, or 19c is created.
-   Supplemental logging, including SUPPLEMENTAL\_LOG\_DATA\_PK and SUPPLEMENTAL\_LOG\_DATA\_UI, is enabled for the user-created Oracle database. For more information, see [Supplemental Logging](https://docs.oracle.com/database/121/SUTIL/GUID-D857AF96-AC24-4CA1-B620-8EA3DF30D72E.htm#SUTIL1582).
-   The user-created Oracle database is running in ARCHIVELOG mode. Archived log files are accessible and a suitable retention period is set for archived log files. For more information, see [Managing Archived Redo Log Files](https://docs.oracle.com/database/121/ADMIN/archredo.htm#ADMIN008).
-   The available storage space of the destination ApsaraDB RDS for MySQL instance is larger than the total size of the data in the user-created Oracle database.

## Precautions

-   DTS uses read and write resources of the source and destination databases during full data migration. This may increase the load of the database server. If the database performance is unfavorable, the specification is low, or the data volume is large, database services may become unavailable. For example, DTS occupies a large amount of read and write resources in the following cases: a large number of slow SQL queries are performed on the source database, the tables have no primary keys, or a deadlock occurs in the destination database. Before you migrate data, evaluate the impact of data migration on the performance of the source and destination databases. We recommend that you migrate data during off-peak hours. For example, you can migrate data when the CPU utilization of the source and destination databases is less than 30%.
-   The tables to be migrated in the source database must have PRIMARY KEY or UNIQUE constraints and all fields must be unique. Otherwise, the destination database may contain duplicate data records.
-   Table names in the ApsaraDB RDS for MySQL instance are case-insensitive. If a table name in the user-created Oracle database contains uppercase letters, ApsaraDB RDS for MySQL converts all uppercase letters to lowercase letters before creating the table.

    If the source Oracle database contains identical table names that differ only in capitalization, these table names are identified as duplicate. During schema migration, the following message is returned: "The object already exists". To avoid name conflicts in the destination database, you can change the names of the migrated objects by using the object name mapping feature. For more information, see [Object name mapping](/intl.en-US/Data Migration/Migration task management/Object name mapping.md).

-   DTS automatically creates a destination database in the ApsaraDB RDS for MySQL instance. However, if the name of the source database is invalid, you must manually create a database in the ApsaraDB RDS for MySQL instance before you configure the data migration task. For more information about the naming conventions of ApsaraDB RDS for MySQL databases and how to create a database, see [Create a database on an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database/Create a database on an ApsaraDB RDS for MySQL instance.md).

## Billing

|Migration type|Instance configuration fee|Internet traffic fee|
|--------------|--------------------------|--------------------|
|Schema migration and full data migration|Free of charge|Charged only when data is migrated from Alibaba Cloud over the Internet. For more information, see [Pricing]().|
|Incremental data migration|Charged. For more information, see [Pricing]().|

## Migration types

-   Schema migration

    DTS supports schema migration for tables and indexes. DTS does not support schema migration for the following types of objects: view, synonym, trigger, stored procedure, function, package, and user-defined type. DTS has the following limits on schema migration for tables and indexes:

    -   Schema migration of nested tables is not supported. Clustered tables and index-organized tables \(IOTs\) are converted into common tables in the destination database.
    -   Schema migration of function-based indexes, domain indexes, bitmap indexes, and reverse indexes is not supported.
-   Full data migration

    DTS migrates historical data of the required objects from the user-created Oracle database to the destination ApsaraDB RDS for MySQL instance.

-   Incremental data migration

    DTS retrieves redo log files from the user-created Oracle database. Then, DTS synchronizes incremental data from the user-created Oracle database to the destination database in the ApsaraDB RDS for MySQL instance. Incremental data migration allows you to ensure service continuity when you migrate data from the user-created Oracle database to the destination database.


## SQL operations that can be synchronized during incremental data migration

-   INSERT, DELETE, and UPDATE
-   CREATE TABLE

    **Note:** If a CREATE TABLE operation creates a table that contains functions, DTS does not synchronize the CREATE TABLE operation.

-   ALTER TABLE, ADD COLUMN, DROP COLUMN, RENAME COLUMN, and ADD INDEX
-   DROP TABLE
-   RENAME TABLE, TRUNCATE TABLE, and CREATE INDEX

## Data type conversion

For more information, see [Data type mappings between heterogeneous databases](/intl.en-US/Data Migration/Data type mappings between heterogeneous databases.md).

## Before you begin

Log on to the source Oracle database, create an account for data collection, and grant permissions to the account.

**Note:** If you have created a database account and the account has the permissions that are listed in the following table, skip this step.

|Database|Schema migration|Full data migration|Incremental data migration|
|:-------|:---------------|:------------------|:-------------------------|
|User-created Oracle database|The owner permission on schemas|The owner permission on schemas|DBA|
|ApsaraDB RDS for MySQL instance|The write permission on the destination database|The write permission on the destination database|The write permission on the destination database|

For more information about how to create and authorize a database account, see the following topics:

-   User-created Oracle database: [CREATE USER](https://docs.oracle.com/cd/B19306_01/server.102/b14200/statements_8003.htm) and [GRANT](https://docs.oracle.com/cd/B19306_01/server.102/b14200/statements_9013.htm)
-   ApsaraDB RDS for MySQL instance: [Create an account](https://www.alibabacloud.com/help/zh/doc-detail/96089.htm) and [Modify account permissions](https://www.alibabacloud.com/help/zh/doc-detail/96101.htm)

**Note:** If you need to migrate incremental data from an Oracle database but the DBA permission cannot be granted to the database account, you can grant fine-grained permissions to the account. The following sample statements show you how to grant specific permissions to an Oracle database account.

## Procedure

1.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**.
3.  At the top of the Migration Tasks page, select the region where the destination RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9840359951/p50439.png)

4.  In the upper-right corner of the page, click **Create Migration Task**.
5.  Configure the source and destination databases.

    ![Configure the source and destination databases](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6720359951/p47598.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |N/A|Task Name|DTS automatically generates a task name. We recommend that you specify an informative name for easy identification. You do not need to use a unique task name.|
    |Source Database|Instance Type|Select an instance type based on the deployment of the source database. In this example, select **User-Created Database with Public IP Address**. **Note:** If you select other instance types, you must prepare the environment that is required for the source database. For more information, see [Preparation overview](). |
    |Instance Region|If the instance type is set to **User-Created Database with Public IP Address**, you do not need to specify the **instance region**. **Note:** If a whitelist is configured for the user-created Oracle database, you must add the CIDR blocks of DTS servers to the whitelist of the database. You can click **Get IP Address Segment of DTS** next to **Instance Region** to obtain the CIDR blocks of DTS servers. |
    |Database Type|Select **Oracle**.|
    |Hostname or IP Address|Enter the endpoint that is used to connect to the user-created Oracle database. In this example, enter the public IP address.|
    |Port Number|Enter the service port number of the user-created Oracle database. The default port number is **1521**.|
    |Instance Type|    -   **Non-RAC Instance**: If you select this option, you must specify the **SID** parameter.
    -   **RAC Instance**: If you select this option, you must specify the **Service Name** parameter. |
    |Database Account|Enter the account of the user-created Oracle database. For more information about the permissions that are required for the account, see [Before you begin](#section_jk0_mfq_ydu).|
    |Database Password|Enter the password of the source database account. **Note:** After you specify the source database parameters, click **Test Connectivity** next to **Database Password** to verify whether the specified parameters are valid. If the specified parameters are valid, the **Passed** message appears. If the **Failed** message appears, click **Check** next to **Failed**. Modify the source database parameters based on the check results. |
    |Destination Database|Instance Type|Select **RDS Instance**.|
    |Instance Region|Select the region where the destination RDS instance resides.|
    |RDS Instance ID|Select the ID of the destination RDS instance.|
    |Database Account|Enter the database account of the destination RDS instance. For more information about the permissions that are required for the account, see [Before you begin](#section_jk0_mfq_ydu).|
    |Database Password|Enter the password of the destination database account. **Note:** After you specify the destination database parameters, click **Test Connectivity** next to **Database Password** to verify whether the parameters are valid. If the specified parameters are valid, the **Passed** message appears. If the **Failed** message appears, click **Check** next to **Failed**. Modify the destination database parameters based on the check results. |

6.  In the lower-right corner of the page, click **Set Whitelist and Next**.

    **Note:** DTS adds the CIDR blocks of DTS servers to the whitelist of the destination RDS instance. This ensures that DTS servers can connect to the destination RDS instance.

7.  Select the migration types and the objects to be migrated.

    ![Select the migration types and the objects to be migrated](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6720359951/p47602.png)

    |Setting|Description|
    |:------|:----------|
    |Select the migration types|    -   To perform only full data migration, select **Schema Migration** and **Full Data Migration**.
    -   To ensure service continuity during data migration, select **Schema Migration**, **Full Data Migration**, and **Incremental Data Migration**.
**Note:** If **Incremental Data Migration** is not selected, do not write data to the source database during full data migration. This ensures data consistency between the source and destination databases. |
    |Select the objects to be migrated|Select objects from the Available section and click the ![Right arrow](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3457359951/p40698.png) icon to move the objects to the Selected section.

**Note:**

    -   You can select columns, tables, or databases as the objects to be migrated.
    -   After an object is migrated to the destination RDS instance, the name of the object remains the same as that in the user-created Oracle database. You can use the object name mapping feature to change the names of the objects that are migrated to the destination RDS instance. For more information, see [Object name mapping](/intl.en-US/Data Migration/Migration task management/Object name mapping.md). |

8.  In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   Before you can start the data migration task, a precheck is performed. You can start the data migration task only after the task passes the precheck.
    -   If the task fails to pass the precheck, click the ![Info icon](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3457359951/p47468.png) icon next to each failed item to view details. Troubleshoot the issues based on the causes and run the precheck again.
9.  After the task passes the precheck, click **Next**.
10. In the Confirm Settings dialog box, specify the **Channel Specification** and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.
11. Click **Buy and Start** to start the migration task.
    -   Full data migration

        Do not manually stop a task during full data migration. Otherwise, data migrated to the destination database will be incomplete. Wait until the migration task automatically stops.

    -   Incremental data migration

        An incremental data migration task does not automatically stop. You must manually stop the migration task.

        **Note:** Select an appropriate time to manually stop the migration task. For example, you can stop the migration task during off-peak hours or before you switch your workloads to the destination instance.

        1.  Wait until **Incremental Data Migration** and **The migration task is not delayed** appear in the progress bar of the migration task. Then, stop writing data to the source database for a few minutes. The delay time of **incremental data migration** may be displayed in the progress bar.
        2.  After the status of **incremental data migration** changes to **The migration task is not delayed**, manually stop the migration task.

            ![The migration task is not delayed](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2940359951/p47604.png)

12. Switch your workloads to the destination RDS instance.

## What to do next

The database accounts that are used for data migration have the read and write permissions. After the data migration is complete, you must delete the accounts of both the user-created Oracle database and the ApsaraDB RDS for MySQL instance to ensure database security.

## More information

DTS supports reverse data transmission when you migrate data from a user-created Oracle database to an ApsaraDB RDS for MySQL instance. You can use this feature to synchronize data changes from the ApsaraDB RDS for MySQL instance to the user-created Oracle database. To do this, submit a ticket.

