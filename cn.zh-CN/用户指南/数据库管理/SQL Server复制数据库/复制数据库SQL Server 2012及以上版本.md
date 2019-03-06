# 复制数据库SQL Server 2012及以上版本 {#concept_x3n_3mq_wdb .concept}

**说明：** 本文仅适用于SQL Server 2012及以上版本的实例。关于如何复制SQL Server 2008 R2版本实例的数据库，请参见[复制数据库SQL Server 2008 R2版](intl.zh-CN/用户指南/数据库管理/SQL Server复制数据库/复制数据库SQL Server 2008 R2版.md#)。

您可以使用SQL命令复制数据库，您只需要使用存储过程sp\_rds\_copy\_database指定源数据库和目的数据库即可。复制时间与数据库大小有关。

## 前提条件 {#section_ydq_lmq_wdb .section}

复制数据库前，实例剩余的空间必须大于源数据库的1.3倍。

## 操作步骤 {#section_rcq_mmq_wdb .section}

执行如下命令，即可复制数据库：

```
USE master
GO
--Query database engine edition
SELECT @@Version
GO
--Create database
CREATE DATABASE testdb
GO
EXEC sp_rds_copy_database 'testdb','testdb_copy'
SELECT *
FROM sys.databases
WHERE name IN ('testdb','testdb_copy')
SELECT 
    family_guid,database_guid,* 
FROM sys.database_recovery_status
WHERE 
DB_NAME(database_id) IN ('testdb','testdb_copy')
```

