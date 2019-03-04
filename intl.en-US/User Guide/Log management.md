# Log management {#concept_ujc_hz4_ydb .concept}

All instance versions except MySQL 5.7 support log management. You can use the RDS console or SQL statements to query error logs and slow SQL log details for fault analysis. However, you can manage logs of instances in SQL Server 2012 and later versions only through SQL statements. This document describes how to manage logs through the RDS console and SQL statements.

## Use the RDS console to manage logs {#section_qf4_jz4_ydb .section}

You can use the RDS console to manage logs of MySQL 5.5/5.6, SQL Server 2008 R2, PostgreSQL, and PPAS instances. The actual interface may vary with engine types and versions.

## Procedure {#section_vqv_kz4_ydb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.
3.  Click the ID of the target instance to enter the Basic Information page.
4.  Click **Log Management** in the left-side navigation pane.
5.  On the Log Management page, select **Error Log**, **Slow SQL Log Details**, **Slow SQL Log Summary**, or **Switch Logs**, select a time range, and click **Query**.

    |Query item|Content|
    |----------|-------|
    |Error Log|Records the SQL statements that are failed to be executed in the past month.|
    |Slow SQL Log Details|     -   Records the SQL statements that lasted for over one second \(For MySQL, you can modify this time threshold by modifying the long\_query\_time parameter in Parameters\) in the past month. Similar SQL statements are displayed once only.
    -   The list does not include slow SQL logs of the past two hours. To query these logs, check the **slow\_log\_view** table in the MySQL database.
 |
    |Slow SQL Log Summary|Provides statistics and analysis reports for SQL statements that lasted for over one second \(For MySQL, you can modify this time threshold by modifying the long\_query\_time parameter in Parameters\) in the past month. |


## Use SQL statements to manage logs {#section_amm_rz4_ydb .section}

Instances in SQL Server 2012 and later versions read error logs only through the `sp_rds_read_error_logs` storage procedure. The method of using it is similar to that of using `sp_readerrorlog`.

Example 1:

```
EXEC sp_rds_read_error_logs
```

Example 2:

```
EXEC sp_rds_read_error_logs 0,1 ,'error'
```

