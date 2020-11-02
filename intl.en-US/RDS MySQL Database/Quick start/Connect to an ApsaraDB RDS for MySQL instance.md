# Connect to an ApsaraDB RDS for MySQL instance

After you complete the initial configuration of your ApsaraDB RDS for MySQL instance, you can connect to it from an Elastic Compute Service \(ECS\) instance or your computer.

After you create an RDS instance, you must configure IP address whitelists and create accounts. Then, you can use Alibaba Cloud Data Management \(DMS\) or a database client to connect to the RDS instance. You can also configure the endpoints, ports, and account information in your application.

For more information about how to connect to an RDS instance that runs other database engines, see the following topics:

-   [Connect to an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Connect to an ApsaraDB RDS for SQL Server instance.md)
-   [Connect to an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Connect to an ApsaraDB RDS for PostgreSQL instance.md)
-   [Connect to an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Quick start/Connect to an ApsaraDB RDS for PPAS instance.md)
-   [Connect to an ApsaraDB RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Quick start/Connect to an ApsaraDB RDS for MariaDB instance.md)

## Use DMS to connect to an RDS instance

DMS is a graphical data management service that allows you to manage relational databases and NoSQL databases. It provides various functions, such as data management, schema management, user authorization, security audit, trend analysis, data tracking, business intelligence \(BI\) charts, and performance analysis and optimization.

You can click **SQL Query** in the Actions column of a specific database on the **Databases** page to log on to the RDS instance. This allows you to manage the database after the logon.

![SQL Query](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3249404061/p174701.png)

For more information, see [t41864.md\#](/intl.en-US/RDS MySQL Database/Database connection/Use DMS to log on to an ApsaraDB for RDS instance.md).

## Use a client to connect to an RDS instance

ApsaraDB RDS for MySQL is fully compatible with open source MySQL. You can connect to an RDS instance from a database client by using a similar method that you use to connect to an open source MySQL database. In the following example, the [HeidiSQL](https://www.heidisql.com/) client is used.

1.  Start the HeidiSQL client.
2.  In the lower-left corner of the Session manager dialog box, click **New**.
3.  Enter information about the RDS instance that you want to connect. The following table describes the parameters.

    ![Connection settings](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2250359951/p54911.png)

    |Parameter|Description|
    |---------|-----------|
    |**Network type**|Select the network type of the RDS instance. For this example, select **MariaDB or MySQL \(TCP/IP\)**.|
    |**Hostname / IP**|Enter the internal or public endpoint of the RDS instance.     -   If the HeidiSQL client is deployed on an ECS instance that resides in the same region and has the same network type as the RDS instance, enter the internal endpoint. For example, if the ECS and RDS instances both reside in virtual private clouds \(VPCs\) of the China \(Hangzhou\) region, you can use the internal endpoint to establish a secure connection.
    -   In other scenarios, enter the public endpoint.
For more information about how to view the internal and public endpoints and the port numbers of the RDS instance, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md). |
    |**User**|Enter the username of the account that you use to connect to the RDS instance.|
    |**Password**|Enter the password of the account.|
    |**Port**|Enter the port number of the RDS instance. If you want to connect to the RDS instance over an internal network, enter the internal port number of the RDS instance. If you want to connect to the RDS instance over the Internet, enter the public port number of the RDS instance. For more information, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md).|

4.  Click **Open**.

    If the connection information is correct, the RDS instance is connected.

    ![Connection established](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2250359951/p2610.png)


## Use the CLI to connect to an RDS instance

If your server is equipped with the MySQL command line interface \(CLI\), you can connect to the RDS instance by running the following command in the CLI:

```
mysql -h<Hostname> -P<Port number> -u<Username> -p<Password> -D<Instance name>
```

|Parameter|Description|Example|
|---------|-----------|-------|
|-h|Enter the internal or public endpoint of the RDS instance. For more information about how to view the internal and public endpoints and the port numbers of the RDS instance, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md).

|`rm-bpxxxxxxxxxxxxxx.mysql.rds.aliyuncs.com`|
|-P|Enter the port number of the RDS instance. -   If you want to connect to the RDS instance over an internal network, enter the internal port number of the instance.
-   If you want to connect to the RDS instance over the Internet, enter the public port number of the instance.

**Note:**

-   The default port number is 3306.
-   You can retain the default port number.

|`3306`|
|-u|Enter the username of the account that you use to connect to the RDS instance.|`root`|
|-p|Enter the password of the account. **Note:** This parameter is optional.

-   If you do not specify this parameter, you are prompted for the password when you connect to the RDS instance.
-   If you specify this parameter, no space character is allowed between `-p` and the password.

|`password233`|
|-D|Enter the name of the instance that you want to connect. **Note:**

-   This parameter is optional.
-   You can enter only the instance name and exclude `-D`.

|`mysql`|

![Connection example in the CLI](../images/p52311.png "Connection example in the CLI")

## FAQ

How do I obtain data from ApsaraDB RDS to Function Compute?

You can install third-party dependencies on Function Compute. Then, you can use these built-in dependencies to obtain data from ApsaraDB RDS.For more information, see [Install third-party dependencies](https://www.alibabacloud.com/help/zh/doc-detail/74571.htm).

