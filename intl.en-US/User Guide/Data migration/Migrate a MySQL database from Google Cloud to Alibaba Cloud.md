# Migrate a MySQL database from Google Cloud to Alibaba Cloud {#concept_ilq_dfl_5fb .concept}

This topic describes how to migrate a MySQL database from Google Cloud to Alibaba Cloud and the corresponding precautions.

## Prerequisites {#section_vw2_ycl_5fb .section}

-   You have [created an Alibaba Cloud RDS MySQL instance](../../../../../intl.en-US/Quick Start for MySQL/Create an instance.md).
-   You have [created an account with read/write privileges](../../../../../intl.en-US/Quick Start for MySQL/Initial configuration/Create accounts and databases.md).

## Limits {#section_ang_jbk_5fb .section}

-   Structure migration does not support migration of events.
-   For MySQL databases, DTS reads floating-point values \(FLOAT and DOUBLE data types\) with `round(column,precision)`. If the column definition does not specify the precision, the precision is 38 for FLOAT values and 308 for DOUBLE values.
-   If the object name mapping function is used for an object, migration of objects relying on the object may fail.
-   For incremental migration, you need to enable binlog for the source MySQL instance.
-   For incremental migration, binlog\_format of the source database must be set to ROW.

    **Note:** You can modify parameters of Google Cloud databases by choosing**Instance details** \> **Configuration** \> **Edit configuration** \> **Add database flags**.

-   For incremental migration, if the source database version is MySQL 5.6 or later, binlog\_row\_image must be set to FULL.
-   For incremental migration, if the source instance has binlog file ID disorder caused by cross-host migration, the incremental migration may have data loss.

## Precautions {#section_ypx_pbk_5fb .section}

DTS automatically attempts to recover abnormal tasks of the past seven days. This may cause the new data in the target instance to be overwritten by the source database data. Therefore, you must revoke the write permission of the DTS account that is used to access the target instance by running the `revoke` command.

## Procedure {#section_uwt_sck_5fb .section}

1.  Log on to your database instance on Google Cloud. On the Instance details page, view Public IP address.

    **Note:** If an Internal IP address is not enabled, perform related settings by going to **Configuration** \> **Edit configuration** \> **Set connectivity**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64127/155410891233416_en-US.png)

2.  Choose **Configuration** \> **Edit configuration** \> **Set connectivity** \> **Add network**, and then add the IP address of the [region of the source database instance](#table_j3v_42k_5fb) obtained from DTS.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64127/155410891233417_en-US.png)

3.  Log on to the [DTS Console](https://dts.console.aliyun.com/).
4.  In the left-side navigation pane, click **Data Migration**. In the right pane, click **Create Migration Task** in the upper-right corner.
5.  Enter information about the source and target databases. The following table describes the parameters.

    |Database type|Parameter|Description|
    |-------------|---------|-----------|
    |Source database \(on Google Cloud\)|Instance Type|Type of the instance in the source database. Select On-premises Databases.|
    |Instance Region|If you have configured access control for your instance, you need to allow the specified Internet IP segment of the region to access the instance before configuring a migration task.**Note:** You can click **Get DTS IP** to view and copy the IP segment of the region.

|
    |Database Engine|Source database type. Select MySQL .|
    |Host Name or IP Address|Public IP address of the database|
    |Port|Default port 3306|
    |Database account|Default superuser account root|
    |Database Password|Password of the root account|
    |Target database \(on Alibaba Cloud\)|Instance Type|Type of the instance in the target database. Select RDS Instance.|
    |Instance Region|Region of the target instance|
    |RDS Instance ID|ID of the instance in the selected region. Select the ID of the target instance.|
    |Database account|An account with read and write permissions under the target instance|
    |Database Password|Account password|
    |Connection method|Select **Non-encrypted connection** or **SSL secure connection**. The latter greatly increases CPU consumption.|

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64127/155410891233418_en-US.png)

6.  Click **Test the Connection** and confirm that the test results for both the source and target databases are Test passed.
7.  Click **Authorize Whitelist and Enter into Next Step** .
8.  Select the migration type. In the Migration objects area, select the target database and click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64127/155410891333419_en-US.png) to add the database to the Selected objects area.

    **Note:** To maintain data consistency before and after migration, we recommend that you migrate the structure, full data, and incremental data.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64127/155410891333420_en-US.png)

9.  Click **Pre-check and Start** and wait until the pre-check ends.

    **Note:** If the check fails, you can rectify faults according to error items and restart the task.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64127/155410891333421_en-US.png)

10. Click **Next**. In the **Confirm Purchase Configuration** dialog box, read and confirm you agree to the **Service Terms of Data Transmission \(Pay-As-You-Go\)** and click **Buy and Start Now**.

    **Note:** Currently, structure migration and full migration are free of charge, while incremental migration is charged by the hour according to link specifications.

11. Wait until the migration task is completed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64127/155410891333422_en-US.png)


