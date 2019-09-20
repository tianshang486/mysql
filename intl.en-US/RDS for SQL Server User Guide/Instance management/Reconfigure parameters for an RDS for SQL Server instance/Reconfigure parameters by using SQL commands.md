# Reconfigure parameters by using SQL commands {#concept_wm4_44n_wdb .concept}

This topic describes how to reconfigure parameters for an RDS for SQL Server instance by using SQL commands.

**Note:** This topic is applicable to RDS for SQL Server 2012 and later versions. For information about how to reconfigure parameters for an RDS instance that uses the SQL Server 2008 R2 engine, see [Reconfigure parameters the in the RDS console](intl.en-US/RDS for SQL Server User Guide/Instance management/Reconfigure parameters for an RDS for SQL Server instance/Reconfigure parameters the in the RDS console.md#).

## Parameters supported {#section_bdv_z4b_1fb .section}

-   fill factor \(%\)
-   max worker threads
-   cost threshold for parallelism
-   max degree of parallelism
-   min server memory \(MB\)
-   max server memory \(MB\)
-   blocked process threshold \(s\)

## Reconfigure parameters {#section_qrs_y4b_1fb .section}

Use sp\_rds\_configure to specify the target configuration item. If the reconfigured parameter requires the RDS instance to restart, the system displays a message to suggest you.

For example, you can run the following command to reconfigure a parameter:

``` {#codeblock_9cw_6fo_24t}
USE master
GO
--database engine edtion
SELECT SERVERPROPERTY('edition')
GO
--create database
CREATE DATABASE testdb
GO
SELECT * 
FROM sys.configurations
WHERE NAME = 'max degree of parallelism'
EXEC sp_rds_configure 'max degree of parallelism',0
WAITFOR DELAY '00:00:10'
SELECT * 
FROM sys.configurations
WHERE NAME = 'max degree of parallelism'
```

