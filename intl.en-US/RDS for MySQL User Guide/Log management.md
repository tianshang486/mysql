# Log management {#concept_ujc_hz4_ydb .concept}

This topic describes how to manage logs through the RDS console and SQL statements. You can query error logs and slow query logs for fault analysis. All RDS for MySQL instances except those in the Basic Edition support log management.

-   For information about log backup policies and rules, see [Back up the data of an RDS for MySQL instance](intl.en-US/RDS for MySQL User Guide/Database backup/Back up the data of an RDS for MySQL instance.md#).
-   For information about how to download log backup files, see [Download the data backup files and log backup files of an RDS for MySQL instance](intl.en-US/RDS for MySQL User Guide/Database backup/Download the data backup files and log backup files of an RDS for MySQL instance.md#).
-   For information about how to restore data through log backup files, see:
    -   [Restore the data of an RDS for MySQL instance](intl.en-US/RDS for MySQL User Guide/Database restoration/Restore the data of an RDS for MySQL instance.md#)
    -   [\(RDS for MySQL\) Restore logical backup file to on-premises database](../intl.en-US/FAQs/Data backup__recovery/(RDS for MySQL) Restore logical backup file to on-premises database.md#)
    -   [Restore data from physical backup files of ApsaraDB for MySQL to an on-premises user-created database](../intl.en-US/FAQs/Data backup__recovery/Restore data from physical backup files of ApsaraDB for MySQL to an on-premises user-created database.md#)

## View logs {#section_wvj_cdo_pja .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156747629036543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Log Management**.
5.  On the Log Management page, select **Error Log**, **Slow Query Log**, **Slow Query Log Summary**, or **Primary/Secondary Instance Switch Log**, select a time range, and click **Search**.

    |Query item|Content|
    |----------|-------|
    |Error Log|Records the SQL statements that are failed to be executed in the last one month.|
    |Slow Query Log|Records the SQL statements that lasted for over 1 second \(you can reconfigure the long\_query\_time parameter to change this time threshold according to [Reconfigure parameters](intl.en-US/RDS for MySQL User Guide/Instance management/Reconfigure parameters.md#)\) in the last one month. Similar SQL statements are displayed once only. **Note:** The slow query logs are updated in the console once every minute. You can view the mysql.slow\_log table to obtain real-time slow query logs.

 |
    |Slow Query Log Summary|Provides statistics and analysis reports for SQL statements that lasted for over 1 second \(you can reconfigure the long\_query\_time parameter to change this time threshold according to [Reconfigure parameters](intl.en-US/RDS for MySQL User Guide/Instance management/Reconfigure parameters.md#)\) in the last one month.|
    |Primary/Secondary Instance Switch Log|Available to RDS instances in the MySQL High-availability Edition.|

    **Note:** For each RDS instance in the China \(Zhangjiakou\) region, the system retains only the error logs, slow query logs, and slow query log summary generated within the last nine days.


