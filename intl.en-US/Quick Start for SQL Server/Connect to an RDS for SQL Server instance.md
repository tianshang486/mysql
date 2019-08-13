# Connect to an RDS for SQL Server instance {#concept_y5f_rj1_wdb .concept}

After you [create an instance](intl.en-US/Quick Start for SQL Server/Create an RDS for SQL Server instance.md), [configure a whitelist](intl.en-US/Quick Start for SQL Server/Initial configuration/Configure a whitelist.md), and create a database and an account, you can use Data Management Sevice \(DMS\) or other database clients to connect to the RDS instance.

## Use DMS to connect to an instance {#section_1py_oh4_6e2 .section}

DMS is a graphical data management service provided by Alibaba Cloud. It can be used to manage non-relational databases and relational databases, and supports data and schema management, user authorization, security audit, data trends, data tracking, BI charts, and performance and optimization.

For more information, see [Use DMS to log on to an RDS instance](../../../../intl.en-US/User Guide/Connection management/Use DMS to log on to an RDS instance.md#).

## Use a client to connect to an instance {#section_8rv_40f_pri .section}

This topic describes how to use the Microsoft SQL Server Management Studio \(SSMS\) client to connect to an RDS instance.

1.  Start the SSMS client in an ECS instance or your computer.
2.  Choose **Connect** \> **Database Engine**.
3.  In the displayed Connect to Server dialog box, enter the logon information.

    ![连接到服务器](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7840/15656778722831_en-US.png)

    |Parameter|Description|
    |---------|-----------|
    |**Server type**|Select **Database Engine**.|
    |**Server name**|Enter the connection address and the port number of the RDS instance. Separate the address and the port number with a comma \(,\), such as `rm-bptest.sqlserver.rds.aliyuncs.com,3433`. The following procedure shows how to view the internal and public addresses and the port number of the RDS instance:

     1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
    2.  In the upper-left corner of the page, select the region where the instance is located.
    3.  Click the ID of the instance.
    4.  Find the internal IP address and port number, or the public IP address and port number of the instance in the **Basic Information** section, as shown in the following figure.

![基本信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7839/15656778722776_en-US.png)

 |
    |**Authentication**|Select **SQL Server Authentication**.|
    |**Login**|Enter the account name of the RDS instance.|
    |**Password**|Enter the password of the account of the RDS instance.|

4.  Click **Connect**.

