# Connect to an ApsaraDB RDS for PostgreSQL instance

This topic describes how to connect to an ApsaraDB RDS for PostgreSQL instance. After you complete the initial configurations, you can connect to your RDS instance from an Elastic Compute Service \(ECS\) instance or your computer.

You can connect to an RDS instance by using Data Management \(DMS\) or a client such as pgAdmin 4.

## Background information

You can log on to DMS from the ApsaraDB RDS console and then connect to an RDS instance.

[DMS](https://dms-intl.console.aliyun.com/#/dms/login) offers an integrated solution for data, schema, and server management, user authorization, security audit, trend analysis, data tracking, business intelligence \(BI\) charts, and performance analysis and optimization. In DMS, you can manage relational databases such as MySQL, SQL Server, and PostgreSQL databases. You can also manage NoSQL databases such as MongoDB and Redis databases.

You can also use a client to connect to an RDS instance. ApsaraDB RDS for PostgreSQL is fully compatible with open source PostgreSQL. You can connect to an ApsaraDB RDS for PostgreSQL instance in the similar way that you connect to an open source PostgreSQL instance. This topic uses the pgAdmin 4 client as an example. You can also adopt this method when you use other clients. When you connect to an RDS instance by using a client, you must select the internal or public endpoint of the RDS instance based on your network environment:

-   If the client runs on an ECS instance that resides in the same region and has the same network type as the RDS instance, use the internal endpoint. For example, if the ECS and RDS instances both reside in virtual private clouds \(VPCs\) of the China \(Hangzhou\) region, use the internal endpoint to establish a secure connection.
-   In other situations, use the public endpoint.

## Use DMS to connect to an RDS instance

Log on the ApsaraDB RDS console, find the RDS instance to which you want to connect, and go to the Databases page. On the **Databases** page, find the database that you want to manage, and click **SQL Query** in the Actions column. On the logon page of DMS, enter the logon information as prompted to connect to the RDS instance.

![SQL Query](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3249404061/p174701.png)

For more information, see [Use DMS to log on to an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Database connections/Use DMS to log on to an ApsaraDB RDS for PostgreSQL instance.md).

## Use the pgAdmin 4 client to connect to an RDS instance

1.  Add the IP address of the pgAdmin client to an IP address whitelist of the RDS instance. For more information, see [Configure a whitelist for an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Configure a whitelist for an ApsaraDB RDS for PostgreSQL instance.md).
2.  Start the [pgAdmin 4 client](https://www.pgadmin.org/download/).

    **Note:** If the pgAdmin client runs a later version and you log on the pgAdmin client for the first time, you must specify a master password that is used to protect the saved passwords and other credentials.

3.  Right-click **Servers** and choose **Create** \> **Server**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4150359951/p2963.png)

4.  On the **General** tab of the Create - Server dialog box, enter the name of the server where the pgAdmin client runs.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4150359951/p2964.png)

5.  Click the **Connection** tab and enter the information that is used to connect to the RDS instance.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4150359951/p2965.png)

    |Parameter|Description|
    |---------|-----------|
    |**Hostname/address**|Enter the endpoint of the RDS instance. If you want to connect to the RDS instance over an internal network, enter the internal endpoint of the RDS instance. If you want to connect to the RDS instance over the Internet, enter the public endpoint of the RDS instance. For more information, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Database connections/View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for PostgreSQL instance.md).|
    |**Port**|Enter the port number that is associated with the endpoint.|
    |**Username**|Enter the username of the account that you use to log on to the RDS instance.|
    |**Password**|Enter the password of the account that you use to log on to the RDS instance.|

6.  Click **Save**.
7.  If the information that you entered is correct, the following page appears, which indicates that the connection to RDS instance is successful.

    **Note:** The postgres database is the default system database of the RDS instance. Do not perform operations on this database.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4150359951/p2967.png)


## FAQ

How do I obtain data from ApsaraDB RDS to Function Compute?

You can install third-party dependencies on Function Compute. Then, you can use these built-in dependencies to obtain data from ApsaraDB RDS.For more information, see [Install third-party dependencies](https://www.alibabacloud.com/help/zh/doc-detail/74571.htm).

