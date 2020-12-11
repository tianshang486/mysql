# View the logs of an ApsaraDB RDS for SQL Server instance

This topic describes how to view the logs of an ApsaraDB RDS for SQL Server instance by using the ApsaraDB RDS console or SQL statements. These logs include error logs and primary/secondary switchover logs. You can use these logs to troubleshoot issues on your RDS instance.

**Note:** For more information about archived logs, see [Back up an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance.md) and [Download data and log backup files from an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Backup/Download data and log backup files from an ApsaraDB RDS for SQL Server instance.md).

## View logs by using the ApsaraDB RDS console

Before you perform the following steps, make sure that your RDS instance runs SQL Server 2008 R2.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Logs**.

5.  On the **Logs** page, click the Error Logs or Primary/Secondary Switching Logs tab, select a time range, and then click **Search**.

    |Tab|Description|
    |---|-----------|
    |Error Logs|Provides database running errors that occurred over the last month.|
    |Primary/Secondary Switching Logs|Provides information about primary/secondary switchovers that occurred over the last month.|


## View logs by using SQL statements

Before you perform the following operations, make sure that your RDS instance runs an SQL Server version other than SQL Server 2008 R2:

-   If your RDS instance runs SQL Server 2016 or an earlier version, run the `sp_rds_read_error_logs` stored procedure to read error logs. The method that is used to run this stored procedure is similar to the method that is used to run the `sp_readerrorlog` stored procedure.
    -   Example 1:

        ```
        EXEC sp_rds_read_error_logs
        ```

    -   Example 2:

        ```
        EXEC sp_rds_read_error_logs 0,1 ,'error'
        ```

-   If your RDS instance runs SQL Server 2017, run the `sp_readerrorlog` stored procedure to read error logs.

    Example:

    ```
    EXEC sp_readerrorlog
    ```


