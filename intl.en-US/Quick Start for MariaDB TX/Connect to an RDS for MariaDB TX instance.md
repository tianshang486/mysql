# Connect to an RDS for MariaDB TX instance {#concept_n1v_qpf_vdb .concept}

You can connect to an RDS for MariaDB TX instance through any MySQL client. This topic uses [MySQL-Front](http://www.mysqlfront.de/) as an example.

## Prerequisites {#section_4gc_x3s_xyo .section}

You have [created an RDS for MariaDB TX instance](intl.en-US/Quick Start for MariaDB TX/Create an RDS for MariaDB TX instance.md#), [configured a whitelist](intl.en-US/Quick Start for MariaDB TX/Initial configuration/Configure a whitelist.md#), and [Created accounts](intl.en-US/Quick Start for MariaDB TX/Initial configuration/Create accounts and databases.md#).

## Use a database client to connect to an RDS instance {#section_pys_6c4_okj .section}

ApsaraDB RDS for MySQL is fully compatible with MySQL. You can connect to an RDS instance from any general-purpose database client in the similar way you connect to a MySQL database. This section describes how to use [HeidiSQL](https://www.heidisql.com/) to connect to an RDS instance.

1.  Start HeidiSQL.
2.  In the lower-left area of the Session manager dialog box, click **New**.
3.  Enter the information of the RDS instance to be connected. The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Network type**|The method of connecting to the RDS instance. Select **MariaDB or MySQL \(TCP/IP\)**.|
    |**Hostname/IP**|Enter the private or public IP address of the RDS instance.     -   If your database client is deployed in an ECS instance that is in the same region and has the same network type as the RDS instance, you can use the private IP address of the RDS instance. For example, if the ECS and RDS instances are both in a VPC located in the China \(Hangzhou\) region, then you can use the private IP address of the RDS instance to create a secure, efficient connection.
    -   In the other situations, use the public IP address of the the RDS instance.
 You can obtain the private and public IP addresses of the RDS instance by completing the following steps:

    1.  Log on to the [RDS console](https://rds.console.aliyun.com).
    2.  In the upper-left corner of the page, select the region where the RDS instance is located.
    3.  Find the RDS instance and click its ID.
    4.  On the displayed **Basic Information** page, find the private and public IP addresses and their corresponding port numbers.

![基本信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/15653398282609_en-US.png)

 |
    |**User**|The username of the account that you use to access the RDS instance.|
    |**Password**|The password of the account that you use to access the RDS instance.|
    |**Port**|The port for the RDS instance to establish a connection. If you use the private IP address of the RDS instance to establish a connection, enter the private port number. If you use the public IP address of the RDS instance to establish a connection, enter the public port number.|

    ![HeidiSQL客户端设置连接信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/156533982854911_en-US.png)

4.  Click **Open**.

    If the entered information is correct, the RDS instance can be connected.

    ![HeidiSQL客户端实例连接成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/15653398292610_en-US.png)


