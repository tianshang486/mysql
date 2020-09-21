# Connect to an ApsaraDB RDS for MySQL instance

After you complete the initial configuration of your ApsaraDB RDS for MySQL instance, you can connect to it from an Elastic Compute Service \(ECS\) instance or an on-premises client.

For more information about how to connect to an RDS instance that runs other database engines, see the following topics:

-   [Connect to an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Connect to an ApsaraDB RDS for SQL Server instance.md)
-   [Connect to an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Connect to an ApsaraDB RDS for PostgreSQL instance.md)
-   [Connect to an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Quick start/Connect to an ApsaraDB RDS for PPAS instance.md)
-   [Connect to an ApsaraDB RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Quick start/Connect to an RDS for MariaDB instance.md)

## Background information

After you create an RDS instance, configure a whitelist, and create an account, you can use Data Management \(DMS\) or a database client to connect to the RDS instance. You can also configure the endpoints, ports, and account information in your application.

## Use DMS to connect to an RDS instance

DMS is a graphical user interface \(GUI\) provided by Alibaba Cloud for you to manage databases. It can be used to manage relational and non-relational databases. It offers various functions, such as data and schema management, user authorization, security audit, data trends, data tracking, BI charts, and performance and optimization.

For more information, see [t41864.md\#](/intl.en-US/RDS MySQL Database/Database connection/Use DMS to log on to an ApsaraDB for RDS instance.md).

## Use a client to connect to an RDS instance

ApsaraDB RDS for MySQL is fully compatible with open source MySQL. You can connect to an ApsaraDB RDS for MySQL instance from a database client by using a similar method that you use to connect to an open source MySQL database. In the following example, the [HeidiSQL](https://www.heidisql.com/) client is used.

1.  Start the HeidiSQL client.
2.  In the lower-left corner of the Session manager dialog box, click **New**.
3.  Enter information about the RDS instance that you want to connect. The following table describes the required parameters.

    ![Connection settings](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2250359951/p54911.png)

    |Parameter|Description|
    |---------|-----------|
    |**Network type**|Select the network type of the RDS instance that you want to connect. For this example, select **MariaDB or MySQL \(TCP/IP\)**.|
    |**Hostname / IP**|Enter the internal or public endpoint of the RDS instance.     -   If your client is deployed on an ECS instance that is in the same region and has the same network type as the RDS instance, use the internal endpoint. For example, if your ECS and RDS instances are both in a VPC located in the China \(Hangzhou\) region, you can use the internal endpoint of the RDS instance to create a secure connection.
    -   In other scenarios, use the public endpoint.
 For more information about how to view the internal and public endpoints and the port numbers of the RDS instance, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md). |
    |**User**|Enter the username of the account that you use to connect to the RDS instance.|
    |**Password**|Enter the password of the account.|
    |**Port**|Enter the port number of the RDS instance. If you connect to the instance over an internal network, enter the internal port number of the instance. If you connect to the instance over the Internet, enter the public port number of the instance.|

4.  Click **Open**.

    If the connection information is correct, the RDS instance is connected.

    ![Connection success](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2250359951/p2610.png)


## Use the CLI to connect to an RDS instance

If your server is equipped with the mysql command line interface \(CLI\), you can connect to the RDS instance by running the following command in the CLI:

```
mysql -h<Hostname> -P<Port> -u<Username> -p<Password> -D<Database>
```

|Parameter|Description|Example|
|---------|-----------|-------|
|-h|Enter the internal or public endpoint of the RDS instance. For more information about how to view the internal and public endpoints and the port numbers of the RDS instance, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md).

|`rm-bpxxxxxxxxxxxxxx.mysql.rds.aliyuncs.com`|
|-P|Enter the port number of the RDS instance. -   If you connect to the instance over an internal network, enter the internal port number of the instance.
-   If you connect to the instance over the Internet, enter the public port number of the instance.

 **Note:**

-   The default port is 3306.
-   If you use the default port, this parameter can be left empty.

|`3306`|
|-u|Enter the username of the account that you use to connect to the RDS instance.|`root`|
|-p|Enter the password of the account. **Note:** This parameter is optional.

-   If you do not specify this parameter, you must enter the password later.
-   When you specify this parameter, no space is allowed between `-p` and the password.

|`password233`|
|-D|The name of the database to be connected. **Note:**

-   This parameter is optional.
-   You can enter only the database name and exclude `-D`.

|`mysql`|

![Connection example in the CLI](../images/p52311.png "Connection example in the CLI")

## FAQ

Q: How do I obtain the data of an ApsaraDB for RDS instance from Function Compute?

A: You can install third-party dependencies for your functions in Function Compute and use built-in components to obtain the data. For more information, see [Install third-party dependencies for functions](https://www.alibabacloud.com/help/zh/doc-detail/74571.htm).

