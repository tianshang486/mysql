# Manage logs

This topic describes how to manage the error logs, slow query logs, and primary/secondary instance switching logs of an ApsaraDB for RDS SQL Server instance through the ApsaraDB for RDS console or by using SQL statements. The logs help you locate faults.

**Note:** For more information about how to archive logs, see [Back up an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance.md) and [Download data and log backup files from an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Backup/Download data and log backup files from an ApsaraDB RDS for SQL Server instance.md).

## View logs through the ApsaraDB for RDS console

Prerequisites

Your RDS instance runs SQL Server 2008 R2.

Procedure

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner of the console, select the region where the target RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the target RDS instance and click its ID.
4.  In the left-side navigation pane, click **Logs**.
5.  On the Logs page that appears, click the Error Log, Slow Query Log Summary, or Primary/Secondary Instance Switching Log tab, select a time range, and click **Search**.

    |Tab|Description|
    |---|-----------|
    |Error Log|Records database running errors that occurred within the last month.|
    |Slow Query Log Summary|Provides statistics and analysis reports on SQL statements that each took more than 1 second to run within the last month. You can change this 1-second threshold by reconfiguring the long\_query\_time parameter.|
    |Primary/Secondary Instance Switching Log|Records switchovers between the primary and secondary instances triggered within the last month.|


## View logs by using SQL statements

Prerequisites

Your RDS instance runs one of the following three SQL Server versions:

-   SQL Server 2012
-   SQL Server 2016
-   SQL Server 2017

Procedure

If your RDS instance runs SQL Server 2012 or SQL Server 2016, execute the `sp_rds_read_error_logs` stored procedure to read error logs. This stored procedure operates in a way similar to the `sp_readerrorlog` stored procedure.

Example 1:

```
EXEC sp_rds_read_error_logs
```

Example 2:

```
EXEC sp_rds_read_error_logs 0,1 ,'error'
```

If your RDS instance runs SQL Server 2017, execute the `sp_readerrorlog` stored procedure to read error logs.

Example:

```
EXEC sp_readerrorlog
```

