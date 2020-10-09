# Limits of ApsaraDB RDS for SQL Server

This topic describes the limits of ApsaraDB RDS for SQL Server. You must understand the limits to make instances more stable and secure.

ApsaraDB RDS for SQL Server instances are provided with Microsoft SQL Server licenses. You cannot use your own licenses. The following table lists other limits.

|Feature|Cluster Edition|High-availability Edition|Basic Edition|
|2017 EE|2019 SE

2017 SE

2016 SE and 2016 EE

2014 SE

2012 SE and 2012 EE

|2008 R2

|2012 Web and 2016 Web

2012 SE and 2016 SE

2012 EE Basic

2016 EE |
|-------|---------------|-------------------------|-------------|
|-------|---------------------------------------------------------------------|---------|--------------------------------------------------------------------|
|Maximum number of databases \([Maximum number of databases](#section_0va_2q3_edm)\)|300|300|50|400|
|Maximum number of database accounts|Unlimited|Unlimited|500|Unlimited|
|Creation of accounts, logon connections, and databases|Supported|Supported|Supported|Supported|
|Database-level data definition language \(DDL\) trigger|Supported|Supported|Not supported|Supported|
|Database permission authorization|Supported|Supported|Not supported|Supported|
|KILL permission|Supported|Supported|Supported|Supported|
|Linked server|Supported|Supported|Not supported|Not supported|
|Distributed transaction|Supported|Supported|Not supported|Not supported|
|SQL Profiler|Supported|Supported|Supported|Supported|
|Tuning Advisor|Supported|Supported|Not supported|Supported|
|Change Data Capture \(CDC\)|Supported|Not supported|Not supported|Not supported|
|Change tracking|Supported|Supported|Not supported|Supported|
|Windows domain account logon|Not supported|Not supported|Not supported|Not supported|
|Email|
|SQL Server Integration Services \(SSIS\)|
|SQL Server Analysis Services \(SSAS\)|
|SQL Server Reporting Services \(SSRS\)|
|R Services|
|Common Language Runtime \(CLR\)|
|Asynchronous communication|
|Replication|
|Policy management|

**Note:** If you encounter other problems about limits, you can [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

## Maximum number of databases

An ApsaraDB for RDS instance that runs SQL Server 2008 R2 supports up to 50 databases. In the other SQL Server versions, the maximum number of databases varies based on the instance type. You can use the following formulas to calculate the maximum number of databases:

-   Cluster and High-availability Editions

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4149259951/p70676.png)

    The maximum number obtained from the preceding formula cannot exceed 300.

-   Basic Edition

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4149259951/p70678.png)

    The maximum number obtained from the preceding formula cannot exceed 400.


