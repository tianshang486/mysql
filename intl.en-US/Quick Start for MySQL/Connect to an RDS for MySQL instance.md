# Connect to an RDS for MySQL instance {#concept_n1v_qpf_vdb .concept}

This topic describes how to connect to an RDS for MySQL instance. After completing the initial configurations, you can use Data Management Service \(DMS\), a database client, or the CLI to connect to ApsaraDB RDS for MySQL.

## Background information {#section_ixn_v5c_dhb .section}

After you [create an instance](intl.en-US/Quick Start for MySQL/Create an RDS for MySQL instance.md), [configure a whitelist](intl.en-US/Quick Start for MySQL/Initial configuration/Configure a whitelist for an RDS for MySQL instance.md#), and [create an account](intl.en-US/Quick Start for MySQL/Initial configuration/Create accounts and databases for an RDS for MySQL instance.md), you can use DMS, a database client, or CLI to connect to your RDS instance. You can also set the IP address, port, and account information in applications to connect.

## Use DMS to connect to an RDS instance {#section_pgl_xm5_vdb .section}

DMS is a graphical data management service provided by Alibaba Cloud. It can be used to manage non-relational databases and relational databases, and supports data and schema management, user authorization, security audit, data trends, data tracking, BI charts, and performance and optimization.

For more information, see [Use DMS to log on to an RDS instance](../../../../intl.en-US/User Guide/Connection management/Use DMS to log on to an RDS instance.md#).

## Use a database client to connect to an RDS instance {#section_qib_br0_czb .section}

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

![基本信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/15689433542609_en-US.png)

 |
    |**User**|The username of the account that you use to access the RDS instance.|
    |**Password**|The password of the account that you use to access the RDS instance.|
    |**Port**|The port for the RDS instance to establish a connection. If you use the private IP address of the RDS instance to establish a connection, enter the private port number. If you use the public IP address of the RDS instance to establish a connection, enter the public port number.|

    ![HeidiSQL客户端设置连接信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/156894335454911_en-US.png)

4.  Click **Open**.

    If the entered information is correct, the RDS instance can be connected.

    ![HeidiSQL客户端实例连接成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/15689433542610_en-US.png)


## Use the CLI to connect to an RDS instance {#section_jch_n19_l3p .section}

If MySQL is installed on your server, you can use the CLI to connect to an RDS instance as follows:

``` {#codeblock_5vk_9q6_1ks}
mysql -h<Host name> -P<Port number> -u<Username> -p<Password> -D<RDS instance name>
```

|Field|Description|Example|
|-----|-----------|-------|
|-h|The private or public IP address of the RDS instance. For more information, see [Configure endpoints](../../../../intl.en-US/User Guide/Connection management/Configure endpoints.md#).|`rm-bpxxxxxxxxxxxxxx.mysql.rds.aliyuncs.com`|
|-P|The port for the RDS instance to establish a connection. -   If you use the private IP address of the RDS instance to establish a connection, enter the private port number.
-   If you use the public IP address of the RDS instance to establish a connection, enter the public port number.

 **Note:** 

-   The default port number is 3306.
-   If the port used by the RDS instance to establish a connection is Port 3306, you can retain the default value.

 |`3306`|
|-u|The username of the account that you use to access the RDS instance.|`root`|
|-p|The password of the account that you use to access the RDS instance. **Note:** This field is optional.

-   If you do not enter the password in this field, the system prompts you to enter the password during subsequent operations.
-   If you enter the password in this field, note that no spaces are allowed between `-p` and the entered password.

 |`password233`|
|-D|The name of the RDS instance you want to access. **Note:** 

-   This field is optional.
-   You can enter only the RDS instance name with `-D` removed.

 |`mysql`|

![MySQL实例命令行连接示例](images/52311_en-US.png "Example of connecting to an RDS instance through CLI")

