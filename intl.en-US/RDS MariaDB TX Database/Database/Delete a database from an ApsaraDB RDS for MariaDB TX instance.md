# Delete a database from an ApsaraDB RDS for MariaDB TX instance

This topic describes how to delete a database from an ApsaraDB RDS for MariaDB TX instance. You can delete a database by using the ApsaraDB RDS console or an SQL statement.

## Delete a database by using the ApsaraDB RDS console

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Databases**.

5.  Find the database and in the **Actions** column click **Delete**.

6.  In the message that appears, click **OK**.


## Delete a database by using an SQL statement

1.  Connect to your RDS instance by using a client. Note that you cannot connect to an ApsaraDB RDS for MariaDB TX instance by using Data Management \(DMS\). For more information, see [Connect to an RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Quick start/Connect to an RDS for MariaDB instance.md).

2.  Execute the following statement to delete the database:

    ```
    drop database <database name>;
    ```


## Related operations

|Operation|Description|
|---------|-----------|
|[DeleteDatabase](/intl.en-US/API Reference/Database management/Delete database.md)|Deletes a database from an ApsaraDB for RDS instance.|

