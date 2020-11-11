# Connect to an ApsaraDB RDS for SQL Server instance

This topic describes how to connect to an ApsaraDB RDS for SQL Server instance. After you complete the initial configuration, you can connect to your RDS instance from an Elastic Compute Service \(ECS\) instance or your computer.

-   [Create an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)
-   [Configure a whitelist for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Configure a whitelist for an ApsaraDB RDS for SQL Server instance.md)
-   [Create an account for an RDS SQL Server instancy](/intl.en-US/RDS SQL Server Database/Account/Create an account for an RDS SQL Server instancy.md)

## Use DMS to connect to your RDS instance

Data Management \(DMS\) is a graphical data management service that allows you to manage relational databases and NoSQL databases. It provides various functions, such as data management, schema management, user authorization, security audit, trend analysis, data tracking, business intelligence \(BI\) charts, and performance analysis and optimization.

For more information about how to connect to your RDS instance by using DMS, see [Use DMS to log on to an ApsaraDB for RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/Use DMS to log on to an ApsaraDB for RDS instance.md).

## Use a database client to connect to your RDS instance

In this section, the Microsoft SQL Server Management Studio \(SSMS\) client is used as an example. For more information, visit [Microsoft SQL Server Management Studio](https://docs.microsoft.com/zh-cn/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017).

1.  Start the SSMS client on your ECS instance or computer.

2.  Choose **Connect** \> **Database Engine**.

3.  In the Connect to Server dialog box, enter the information that is used to log on to your RDS instance.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8849259951/p2831.png)

    |Parameter|Description|
    |---------|-----------|
    |**Server type**|Select **Database Engine**.|
    |**Server name**|Enter the endpoint and port number of your RDS instance. The endpoint and the port number are separated by a comma \(,\). Example: `rm-bptest.sqlserver.rds.aliyuncs.com,3433`. For more information about how to view the internal and public endpoints and port numbers of your RDS instance, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for SQL Server instance.md). |
    |**Authentication**|Select **SQL Server Authentication**.|
    |**Login**|Enter the username of the account that is authorized to log on to your RDS instance.|
    |**Password**|Enter the password of the account that is authorized to log on to your RDS instance.|

4.  Click **Connect**.


## FAQ

How do I obtain data from ApsaraDB RDS to Function Compute?

You can install third-party dependencies on Function Compute. Then, you can use these built-in dependencies to obtain data from ApsaraDB RDS.For more information, see [Install third-party dependencies](https://www.alibabacloud.com/help/zh/doc-detail/74571.htm).

