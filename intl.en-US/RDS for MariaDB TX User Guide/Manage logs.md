# Manage logs {#concept_ujc_hz4_ydb .concept}

This topic describes how to manage the logs of an RDS for MariaDB instance in the RDS console.

-   For information about log backup policies and rules, see [Automatically back up the data of an RDS for MariaDB instance](intl.en-US/RDS for MariaDB TX User Guide/Data backup/Automatically back up the data of an RDS for MariaDB instance.md#).
-   For information about how to download log backup files, see [Download the log backup files of an RDS for MariaDB instance](intl.en-US/RDS for MariaDB TX User Guide/Data backup/Download the log backup files of an RDS for MariaDB instance.md#).
-   For information about how to restore data through log backup files, see [Restore the data of an RDS for MariaDB instance](intl.en-US/RDS for MariaDB TX User Guide/Data restoration/Restore the data of an RDS for MariaDB instance.md#).

## View logs {#section_a5g_2zv_1gb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156896039436543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Log Management**.
5.  On the Log Management page, select **Error Log**, **Slow Query Log**, **Slow Query Log Summary**, or **Primary/Secondary Instance Switch Log**, select a time range, and click **Search**.

    |Query item|Description|
    |----------|-----------|
    |Error Log|Records the SQL statements that are failed to be executed within the last one month.|
    |Slow Query Log|Records the SQL statements that lasted for more than 1 second within the last one month. \(You can reconfigure the long\_query\_time parameter to change this time threshold according to [Reconfigure parameters for an RDS for MariaDB instance](intl.en-US/RDS for MariaDB TX User Guide/Instance management/Reconfigure parameters for an RDS for MariaDB instance.md#).\) Similar SQL statements are displayed once only.|
    |Slow Query Log Summary|Provides statistics and analysis reports for SQL statements that lasted for more than 1 second within the last one month. \(You can reconfigure the long\_query\_time parameter to change this time threshold according to [Reconfigure parameters for an RDS for MariaDB instance](intl.en-US/RDS for MariaDB TX User Guide/Instance management/Reconfigure parameters for an RDS for MariaDB instance.md#).\)|
    |Primary/Secondary Instance Switch Log|Records logs related to the switchovers between the master and slave instances within the last one month.|


