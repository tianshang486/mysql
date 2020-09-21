# SQL Explorer

This topic describes how to use the SQL Explorer feature of ApsaraDB RDS for MySQL. Compared with the previous SQL Audit feature, SQL Explorer provides more value-added services at lower costs. These services include security audit and performance diagnosis. Upgrading SQL Audit to SQL Explorer does not affect workloads on your RDS instance.

Your RDS instance runs one of the following MySQL versions and RDS editions:

-   MySQL 8.0 on RDS High-availability Edition
-   MySQL 5.7 on RDS High-availability Edition
-   MySQL 5.6
-   MySQL 5.5

SQL Explorer logs all of the data manipulation language \(DML\) and data definition language \(DDL\) operations that are performed on your RDS instance. This is achieved by using network protocol analysis and consumes only a small amount of CPU resources. The Trial Edition of SQL Explorer allows you to store SQL log files for up to one day free of charge. If you want to store SQL log files for more than one day, you must pay additional fees.

## Billing

-   Trial Edition: Starting from August 20th, 2020, the Trial Edition is subject to the new billing policies in all Alibaba Cloud regions.

    The Trial Edition is allowed a 15-day validity period. After the 15-day validity period elapses, the Trial Edition is no longer available. If you want to continue using SQL Explorer, we recommend that you purchase the Paid Edition.

    **Note:** The Trial Edition of SQL Explorer can be enabled only once for each RDS instance.

-   Paid Edition: The Paid Edition allows you to store SQL log files for 30 days, 6 months, 1 year, 3 years, or 5 years. You are charged an hourly fee of USD 0.0018/GB.

## Scenarios

-   Your RDS instance is used for sectors such as finance, security, stocks, governmental affairs, and insurance that have high requirements on data security.
-   You want to analyze the operation of your RDS instance to locate problems or check the execution performance of SQL statements.
-   You may need to restore your data by using logged SQL statements.

## Differences between SQL logs and binary logs

SQL logs and binary logs both include the incremental data of your RDS instance. However, the two types of logs differ in the following aspects:

-   SQL logs are similar to audit logs in MySQL and include information about all of the DML and DDL operations that are performed. The information is obtained by using network protocol analysis. SQL Explorer does not parse actual parameter values. If a large number of SQL statements are executed to query data, some operation records may be lost. As a result, the incremental data obtained from SQL logs may be inaccurate.
-   Binary logs include information about all of the add, delete, and modify operations. You can obtain the accurate incremental data of your RDS instance from binary logs. After binary log files are generated, they are temporarily stored on your RDS instance. The system periodically transfers every binary log file whose size reaches the specified threshold to Alibaba Cloud Object Storage Service \(OSS\). In OSS buckets, these binary log files can be stored for up to seven days. However, if a binary log file is receiving data written to it, it cannot be transferred to OSS. As a result, after a periodic transfer is complete, you may find binary log files that fail to be transferred to OSS. In addition, binary logs are not generated in real time.

## Precautions

-   The time range that is allowed for an online query extends up to 24 hours. This is because SQL Explorer logs a large number of SQL statements to trace all database-related operations. If the time range for an online query exceeds 24 hours, the query takes a long time and may even time out.

    **Note:** If you want to query SQL logs from a time range longer than 24 hours, we recommend that you asynchronously export SQL logs and download the exported SQL log files to your computer.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1540359951/p56771.png)

-   You can specify a combination of conditions for an online query. For example, you can enter test1 test2 in the Keywords field to query SQL logs that contain the keyword test1 or test2.
-   Fuzzy match is not supported for online queries.
-   The length of an SQL statement is limited to 2,000 bytes. If an SQL statement exceeds 2,000 bytes, the excessive part cannot be logged.

## Functions

-   SQL logging

    This function logs all of the operations that are performed on your RDS instance. You can use SQL logs to identify failures, analyze behavior, and audit security.

-   Advanced search

    This function allows you to query data in various dimensions, such as database, thread ID, user, client IP address, execution time, and scanned rows. You can also export and download the query results.

    **Note:**

    -   If you query data in a single dimension, you can specify more than one search condition. The system considers the specified search conditions in OR relationships. For example, if you specify two search conditions, user1 and user2, in the **Users** field, the system returns the SQL statements that are executed by user1 and those that are executed by user2.
    -   If you query data in more than one dimension, the system considers the specified dimensions in AND relationships. For example, if you enter user1 in the **Users** field and select SELECT for the **Operation Type** parameter, the system returns all of the SELECT statements that are executed by user1.
    -   Fuzzy match is not supported.
    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1540359951/p13817.png)

-   SQL analysis

    This function allows you to analyze SQL logs that are generated over a specified time range. Based on the SQL log analysis results, you can identify abnormal SQL statements and locate performance issues.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1540359951/p13818.png)

-   Cost efficiency

    Columnar storage and compression technologies are used to reduce the storage usage for SQL logs. This allows you to save 60% of the overall storage costs.


## Enable SQL Explorer

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **SQL Explorer**.

5.  Click **Activate Now**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1540359951/p13750.png)

6.  Select an SQL log storage duration and click **Activate**.

    **Note:** The system deletes all of the SQL log files that are stored longer than the specified storage duration.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1540359951/p13755.png)


## Change the SQL log storage duration

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **SQL Explorer**.

5.  Click **Service Settings**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2540359951/p13804.png)

6.  Select an SQL log storage duration and click **OK**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1540359951/p13805.png)


## Disable SQL Explorer

**Note:** After you disable SQL Explorer, all of the existing SQL log files are deleted. Before you disable SQL Explorer, we recommend that you export SQL logs and download the exported SQL log files to your computer.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **SQL Explorer**.

5.  Click **Export**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1540359951/p13823.png)

6.  In the message that appears, click **OK**.

7.  After the export is complete, click **View Exported List** and download the exported SQL log files to your computer.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1540359951/p13831.png)

8.  Click **Service Settings**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2540359951/p13804.png)

9.  Turn off the switch next to Activate SQL Explorer and click **OK**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2540359951/p13807.png)


## FAQ

After I enable SQL Explorer, how do I view the size of SQL logs?

After you enable SQL Explorer, you can log on to the ApsaraDB for RDS console and go to the **Basic Information** page for your RDS instance. In the **Usage Statistics** section of the page, you can obtain the size of SQL logs from the Log Size parameter.

![Log Size](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2540359951/p67321.png)

