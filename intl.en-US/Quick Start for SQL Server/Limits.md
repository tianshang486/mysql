# Limits {#concept_nrk_ntz_vdb .concept}

To guarantee instance stability and security, RDS for SQL Server has certain limits.

|Function|Cluster \(AlawayOn\) Edition|High-Availibility Edition|Basic Edition|
| 2017 Enterprise

 | 2016 Standard/Enterprise

 2012 Standard, Enterprise

 | 2008 R2 Enterprise

 | 2016 Web

 2012 Web/Enterprise

 |
|--------|----------------------------|-------------------------|-------------|
|-------------------|--------------------------------------------------------|----------------------|----------------------------------|
|Maximum number of databases \(Note\)|50|50|50|100|
|Maximum number of database accounts|Unlimited|Unlimited|500|Unlimited|
|Create user, LOGIN, or database|Supported|Supported|Supported|Supported|
|Database-level DDL trigger|Supported|Supported|Not supported|Supported|
|Database permission authorization|Supported|Supported|Not supported|Supported|
|KILL permission|Supported|Supported|Supported|Supported|
|LinkServer|Supported|Supported|Not supported|Not supported|
|Distributed transaction|Supported|Supported|Not supported|Not supported|
|SQL Profiler|Supported|Supported|Supported|Supported|
|Tuning Advisor|Supported|Supported|Not supported|Supported|
|Change Data Capture \(CDC\)|Supported|Supported|Not supported|Supported|
|Chage Tracking|Supported|Supported|Supported|Supported|
|Windows domain account login|Not supported|Not supported|Not supported|Not supported|
|Email|
|SQL Server Integration Services \(SSIS\)|
|SQL Server Analysis Services \(SSAS\)|
|SQL Server Reporting Services \(SSRS\)|
|R Services|
|Common Language Runtime \(CLR\)|
|Asynchronous communication|
|Replication|
|Policy management|

**Note:** 

-   RDS for SQL Server instances already have Microsoft SQL Server licenses and do not support your own licenses.

-   For SQL Server 2012/2016/2017, you can [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to apply for increasing the higher maximum number of databases.


