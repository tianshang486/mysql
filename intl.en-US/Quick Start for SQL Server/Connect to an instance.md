# Connect to an instance {#concept_y5f_rj1_wdb .concept}

After completing the initial configurations, you can connect to the RDS for SQLServer instance through a SQL Server client or your application by configuring the connection address, port number, and account information. The SQL Server client and your application can be deployed on ECS or a local computer.

If you are connecting from ECS to RDS through the intranet address, make sure that:

-   The ECS and RDS instances are both in the classic network or in the same VPC.
-   You have added the ECS intranet address to the RDS whitelist.

## Use a client to connect to RDS for SQL Server { .section}

The following introduces the connection procedure by taking the Microsoft SQL Server Management Studio \(SSMS\) client as an example.

1.  On your ECS instance or local computer, start Microsoft SQL Server Management Studio.
2.  In the Connect to Server dialog box, enter connection information.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7840/15571570222831_en-US.png)

    |Parameter|Description|
    |---------|-----------|
    |**Server type**|Select **Database Engine**.|
    |**Server name**|Enter the connection address and port number and separate them with a comma. For example, **rm-bptest.sqlserver.rds.aliyuncs.com,3433** You can view the intranet or Internet address and port number as follows:

     1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
    2.  At the upper-left corner, select the region where the RDS instance is located.
    3.  Click the instance ID.

The **Basic Infomation** area shows the addresses and port numbers.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7839/15571570222776_en-US.png)

 |
    |**Authentication**|Select **SQL Server Authentication**.|
    |**Login**|Name of an RDS instance account.|
    |**Password**|Password of the preceding account.|

3.  Click **Connect** to connect to the RDS instance.

