# Connect to an ApsaraDB RDS for MariaDB instance

This topic describes how to connect to an ApsaraDB RDS for MariaDB instance. After you complete the initial configurations, you can connect to your RDS instance from an Elastic Compute Service \(ECS\) instance or your computer.

## Prerequisites

The following operations are completed:

-   [Creates an ApsaraDB RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Quick start/Creates an ApsaraDB RDS for MariaDB instance.md)
-   [Configure a whitelist for an ApsaraDB RDS for MariaDB TX instance](/intl.en-US/RDS MariaDB TX Database/Quick start/Configure a whitelist for an ApsaraDB RDS for MariaDB TX instance.md)
-   [Create a database and account on an ApsaraDB RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Quick start/Create a database and account on an ApsaraDB RDS for MariaDB instance.md)

## Use DMS to connect to an RDS instance

DMS is a graphical data management service that allows you to manage relational databases and NoSQL databases. It provides various functions, such as data management, schema management, user authorization, security audit, trend analysis, data tracking, business intelligence \(BI\) charts, and performance analysis and optimization.

Log on the ApsaraDB RDS console, find the RDS instance to which you want to connect, and go to the Databases page. On the **Databases** page, find the database that you want to manage, and click **SQL Query** in the Actions column. On the logon page of DMS, enter the logon information as prompted to connect to the RDS instance.

![SQL Query](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3249404061/p174701.png)

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


## FAQ

How do I obtain data from ApsaraDB RDS to Function Compute?

You can install third-party dependencies on Function Compute. Then, you can use these built-in dependencies to obtain data from ApsaraDB RDS.For more information, see [Install third-party dependencies](https://www.alibabacloud.com/help/zh/doc-detail/74571.htm).

