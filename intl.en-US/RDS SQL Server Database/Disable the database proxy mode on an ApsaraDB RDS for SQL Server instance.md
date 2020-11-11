# Disable the database proxy mode on an ApsaraDB RDS for SQL Server instance

This topic describes how to disable the database proxy mode on an ApsaraDB RDS for SQL Server instance. After you disable the database proxy mode, the RDS instance runs in standard mode. This improves the performance of the RDS instance.

## Precautions

In the database proxy mode, the multi-statement function is enabled by default at the protocol layer. After you disable the database proxy mode, the multi-statement function is also disabled. In this case, if you run multi-statements, the system reports errors. Before you disable the database proxy mode, we recommend that you check and add the connection parameters of your RDS instance. For example, add the allowMultiQueries parameter in the JDBC API.

```
dbc:mysql:///test? allowMultiQueries=true
```

## Access modes

|Database engine version|Access mode|
|-----------------------|-----------|
|SQL Server 2012, SQL Server 2016, and SQL Server 2017|Only the standard mode is supported.|
|SQL Server 2008 R2|Both the standard mode and the database proxy mode are supported.|

## Prerequisites

The database proxy mode is enabled for your RDS instance.

**Note:**

-   If the Database Proxy tab appears, the database proxy mode is enabled. Perform the following steps to disable the database proxy mode.
-   If the Database Proxy tab does not appear, the database proxy mode is disabled. You do not need to perform the operations that are described in this topic.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8359259951/p39637.png)

## Procedure

Precautions

-   You can only disable the database proxy mode. However, you cannot enable the database proxy mode.
-   When you disable the database proxy mode, a transient connection error of about 30 seconds will occur. We recommend that you disable the database proxy mode during off-peak hours. Alternatively, make sure that you configure your application to automatically reconnect to your RDS instance.
-   If your RDS instance runs SQL Server 2008 R2 in a virtual private cloud \(VPC\), the database proxy mode is selected by default. You cannot disable the database proxy mode.
-   If your RDS instance runs SQL Server 2008 R2 in the classic network, the standard mode is selected by default. You cannot disable the standard mode or change the network type to VPC.

Method 1

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.
4.  In the left-side navigation pane, click **Database Connection**.
5.  In the upper-right corner of the Instance Connection tab, click **Switch Access Mode**. In the message that appears, click **OK**.

    ![Database connections](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8359259951/p37541.png)


Method 2

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.
4.  In the left-side navigation pane, click **Database Proxy**.
5.  On the Database Proxy tab, turn off **Database Proxy Status**. In the dialog box that appears, click **Confirm**.

