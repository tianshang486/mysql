# Log management {#concept_ujc_hz4_ydb .concept}

This topic describes how to manage logs through the RDS console and SQL statements. You can query error logs and slow query logs for fault analysis. All RDS instances except RDS for MySQL \(Basic Edition\) support log managment.

-   For information about log backup policies and rules, see [Back up RDS data](intl.en-US/User Guide/Backup/Back up RDS data.md#).
-   For information about how to download log backup files, see [Download RDS data and log backup](intl.en-US/User Guide/Backup/Download data and log backup files.md#).
-   For information about how to restore data through log backup files, see:
    -   [Restore MySQL data](intl.en-US/User Guide/Recovery/Restore MySQL data.md#)
    -   [Restore SQL Server Data](intl.en-US/User Guide/Recovery/Restore SQL Server Data.md#)
    -   [Restore PostgreSQL or PPAS data](intl.en-US/User Guide/Recovery/Restore PostgreSQL or PPAS data.md#)
    -   [Restore MariaDB data](intl.en-US/User Guide/Recovery/Restore MariaDB data.md#)
    -   [RDS for MySQL 逻辑备份文件恢复到自建数据库](../../../../intl.en-US/FAQs/Data backup__recovery/(RDS for MySQL) Restore logical backup file to on-premises database.md#)

## Manage logs by using the RDS console {#section_qf4_jz4_ydb .section}

You can use the RDS console to manage logs for instances in the following versions:

-   MySQL 5.5/5.6/5.7/8.0
-   SQL Server 2008 R2
-   PostgreSQL
-   PPAS
-   MariaDB TX

The actual interface may vary with engine types and versions.

The procedure is as follows:

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.
3.  Click the ID of the target instance to enter the Basic Information page.
4.  In the left-side navigation pane, click **Log Management**.
5.  On the Log Management page, select **Error Log**, **Slow Query Log**, **Slow Query Log Summary**, or **Primary/Secondary Instance Switch Log**, select a time range, and click **Query**.

    |Query item|Content|
    |----------|-------|
    |Error Log|Records the SQL statements that are failed to be executed in the past month.|
    |Slow Query Log|     -   Records the SQL statements that lasted for over one second \(for MySQL and MariaDB, you can modify this time threshold by modifying the long\_query\_time parameter in Parameters\) in the past month. Similar SQL statements are displayed once only.
    -   The list does not include slow SQL logs of the past two hours. To query these logs, check the **slow\_log\_view** table in the MySQL database.
 |
    |Slow Query Log Summary|Provides statistics and analysis reports for SQL statements that lasted for over one second \(For MySQL and MariaDB, you can modify this time threshold by modifying the long\_query\_time parameter in Parameters\) in the past month.|
    |Primary/Secondary Instance Switch Log|Available to instances of the MySQL High-Availability edition and MariaDB TX instances.|


## Manage logs by using SQL statements {#section_amm_rz4_ydb .section}

You can use SQL statements to manage logs for instances in the following versions:

-   SQL Server 2012
-   SQL Server 2016
-   SQL Server 2017

Instances in SQL Server 2012 and SQL Server 2016 read error logs only through the `sp_rds_read_error_logs` storage procedure. The method of using `sp_rds_read_error_logs` is similar to that of using `sp_readerrorlog`.

Example 1:

``` {#codeblock_tnb_jry_wf2}
EXEC sys.sp_readerrorlog;
```

Example 2:

``` {#codeblock_xc8_es5_9bx}
EXEC sys.sp_readerrorlog 0,1 ,'error';
```

Instances in SQL Server 2017 read error logs through the `sp_readerrorlog` storage procedure.

Example:

``` {#codeblock_19m_nsb_0t2}
EXEC sp_readerrorlog
```

