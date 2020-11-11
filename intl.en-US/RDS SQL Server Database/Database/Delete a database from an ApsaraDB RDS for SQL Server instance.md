# Delete a database from an ApsaraDB RDS for SQL Server instance

This topic describes how to delete a database from an ApsaraDB RDS for SQL Server instance. You can delete a database by using the ApsaraDB for RDS console or an SQL statement.

## Delete a database by using the ApsaraDB for RDS console

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Databases**.

5.  Find the database that you want to delete and in the **Actions** column click **Delete**.

6.  In the message that appears, click **OK**.


## Delete a database by using an SQL statement

1.  Connect to the RDS instance to which the database belongs. For more information, see [Connect to an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Connect to an ApsaraDB RDS for SQL Server instance.md).

2.  Execute the following statement to delete the database:

    ```
    drop database <database name>;
    ```

    **Note:** If the RDS instance runs SQL Server 2012 or later on RDS High-availability Edition, run the following stored procedure. This stored procedure deletes the specified database, removes the associated image, and closes the connection to the database.

    ```
    EXEC sp_rds_drop_database 'database name'
    ```


## Related operations

|Operation|Description|
|---------|-----------|
|[DeleteDatabase](/intl.en-US/API Reference/Database management/Delete database.md)|Deletes a database from an ApsaraDB RDS instance.|

