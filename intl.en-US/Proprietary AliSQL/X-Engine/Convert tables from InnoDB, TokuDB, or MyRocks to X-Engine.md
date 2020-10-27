# Convert tables from InnoDB, TokuDB, or MyRocks to X-Engine

ApsaraDB RDS for MySQL 8.0 supports X-Engine. X-Engine provides better data compression capabilities and reduces disk space costs. This topic describes how to convert tables from InnoDB, TokuDB, or MyRocks to X-Engine.

X-Engine is an online transaction processing \(OLTP\) database storage engine that is developed by Alibaba Cloud to suit the needs of PolarDB. X-Engine now is widely used in a number of business systems of Alibaba Group to reduce costs. These include the transaction history database and DingTalk chat history database. In addition, X-Engine is a crucial database technology that empowers Alibaba Group to withstand bursts of traffic that may surge by hundreds of times than usual during Double 11, a shopping festival in China.

For more information, see the following topics:

-   [Usage notes](/intl.en-US/Proprietary AliSQL/X-Engine/Usage notes.md)
-   [Best practices of X-Engine](/intl.en-US/RDS MySQL Database/MySQL/Best practices of X-Engine.md)

**Note:** When you create an RDS instance that is designed to run MySQL 8.0, we recommend that you specify X-Engine as the default storage engine. After the RDS instance is created, you can also specify X-Engine for the RDS instance by setting the engine parameter to xengine.

![Default storage engine](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8530749951/p94602.png)

## Precautions

-   If the tables that you want to convert uses InnoDB, make sure that the remaining disk space of your RDS instance is twice the data volume of the tables. After the conversion to X-Engine, the disk space that is occupied by the tables decreases to 10% to 50% of the original disk space that is occupied by the tables before the conversion.
-   If you use Solution 1 in this topic to perform the conversion, you must reconfigure parameters and restart your RDS instance. Stop your database service before you perform the conversion.
-   If you use Solution 2 in this topic to migrate all data from your RDS instance to a new RDS instance, you must update the endpoints on your application. We recommend that you perform the migration during off-peak hours.
-   Before the conversion, make sure that X-Engine is compatible with SQL.
-   After the conversion, change the value of the **default\_storage\_engine** parameter to **xengine**. This ensures that all of the tables that are created later use X-Engine.

## Solution recommendations

-   If your RDS instance runs MySQL 8.0 \(with a minor engine version of 20200229 or later\), we recommend that you use [Solution 1](#section_rw9_h1f_cmq). This way, you do not need to configure various tools.

    **Note:** If the minor engine version of your RDS instance does not meet your business requirements, you can update the minor engine version on the Basic Information page in the ApsaraDB RDS console. In the Configuration Information section of the Basic Information page, check whether the Upgrade Kernel Version button exists. If the button exists, you can click the button to view and update the minor engine version. If the button does not exist, you are using the latest minor engine version. For more information, see [Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance.md).

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6040359951/p61646.png)

-   If your RDS instance runs MySQL 5.6 or 5.7, we recommend that you use [Solution 2](#section_4wc_kda_hjy).

## Solution 1

This solution allows you to enable X-Engine by using a parameter template. Then, you can use data definition language \(DDL\) statements to convert tables to X-Engine. This solution is easy and fast, but requires a restart of your RDS instance. In addition, data manipulation language \(DML\) operations may be blocked, and the conversion of large-sized tables is time-consuming.

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).

2.  In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Parameters**.

5.  In the upper-left corner of the Editable Parameters tab, click **Apply Template**. In the dialog box that appears, select **MySQL\_8.0\_X-Engine\_High-availability\_Default Parameter Template** from the Apply Template drop-down list and click **OK**.

    **Note:** This operation triggers a restart of your RDS instance. After the restart, 95% of the memory resources are allocated to X-Engine. Do not use X-Engine and InnoDB at the same time.

    ![Convert a table to a new storage engine](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8530749951/p94612.png)

6.  Log on to your RDS instance by using Data Management \(DMS\). For more information, see [Use DMS to log on to an ApsaraDB RDS instance](/intl.en-US/RDS MySQL Database/Database connection/Use DMS to log on to an ApsaraDB for RDS instance.md).

7.  In the top navigation bar, choose **SQL Operations** \> **SQL Window**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8530749951/p74996.png)

8.  Run the following command to convert a table:

    ```
    alter table <The name of the database where the table resides>. <The name of the table> engine xengine;
    ```

    Example:

    ```
    alter table test.sbtest1 engine xengine;
    ```


## Solution 2

This solution allows you to synchronize the data of tables in real time from your RDS instance to a new RDS instance by using Data Transmission Service \(DTS\). After the data synchronization is complete, you can switch over your workloads to the new RDS instance.

**Note:** The new RDS instance inherits the storage engine of your RDS instance by default. You must export the SQL statements that are used to create tables. In addition, you must change the storage engine to X-Engine in these SQL statements. Then, you can migrate the data to the new X-Engine tables.

1.  Perform the following steps to export all the schemas of your RDS instance:

    1.  Log on to your RDS instance by using DMS. For more information, see [Use DMS to log on to an ApsaraDB RDS instance](/intl.en-US/RDS MySQL Database/Database connection/Use DMS to log on to an ApsaraDB for RDS instance.md).

    2.  In the top navigation bar, choose **Data Operation** \> **Export**.

        ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9530749951/p75002.png)

    3.  Choose **New** \> **Export Database**.

    4.  Configure the parameters and click **OK**. In the message that appears, click **Yes**.

        **Note:** The message appears because **Extended Options** is selected in the **Advanced Options** dialog box. You can ignore the message.

        ![Export schemas](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9530749951/p75005.png)

2.  Decompress the schemas and change InnoDB or TokuDB to X-Engine.

    ![Modify schemas](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9530749951/p75015.png)

3.  Purchase a new RDS instance that runs MySQL 8.0 and has the same specifications as your RDS instance. Make sure that you select the X-Engine parameter template.

    **Note:** When you create the new RDS instance, you can use the default X-Engine parameter template to specify X-Engine as the default storage engine. For more information, see [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md).

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6530749951/p75281.png)

4.  Perform the following steps to import the schemas into the new RDS instance.

    1.  Log on to the new RDS instance by using DMS. For more information, see [Use DMS to log on to an ApsaraDB RDS instance](/intl.en-US/RDS MySQL Database/Database connection/Use DMS to log on to an ApsaraDB for RDS instance.md).

    2.  In the top navigation bar, choose **Data Operation** \> **Import**.

        ![Import](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9530749951/p75022.png)

    3.  On the page that appears, click **New Task**.

    4.  In the dialog box that appears, configure the parameters and click **Start**.

        ![Import scripts](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9530749951/p75028.png)

        **Note:** After the schemas are imported, you can run the following command to verify that a table uses X-Engine:`show create table <The name of the table>;`.

5.  Synchronize data from your RDS instance to the new RDS instance. For more information, see [Configure two-way data synchronization between ApsaraDB RDS for MySQL instances]().

    **Warning:** In the Advanced Settings step, do not select **Initial Schema Synchronization**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9530749951/p75041.png)


After the synchronization is complete, you can check whether the data synchronization is successful. Then, you can test the compatibility between X-Engine and SQL. If X-Engine is compatible with SQL, you can convert tables to X-Engine.

