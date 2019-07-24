# 下载的RDS备份如何恢复到新的RDS实例 {#concept_1322637 .concept}

本文介绍如何将RDS for MySQL和RDS for SQL Server的备份文件恢复到新的RDS实例。

## 应用场景 {#section_nha_rgy_wp3 .section}

如果您之前下载了RDS备份作为存档，并且释放了原实例，现在因为业务原因需要将数据恢复到新的RDS实例，您可以参考本文介绍的方法进行恢复。

**说明：** 

-   RDS for PostgreSQL/PPAS暂不支持使用物理备份文件恢复到RDS实例，需要您在释放原实例前使用客户端进行逻辑备份，需要恢复时再使用pg\_dump功能恢复到新的RDS实例，详情请参见[使用 psql 命令迁移自建PostgreSQL 数据库数据](../../../../cn.zh-CN/RDS for PostgreSQL 用户指南/数据迁移/使用 psql 命令迁移自建PostgreSQL 数据库数据.md#)。
-   RDS for MariaDB暂不支持下载备份文件。

## MySQL恢复方法 {#section_b41_ud3_gdd .section}

您可以通过如下步骤将数据恢复到新的RDS实例：

1.  将RDS备份恢复到本地数据库。详情请参见[RDS for MySQL 物理备份文件恢复到自建数据库](cn.zh-CN/常见问题/备份__恢复__迁移/RDS for MySQL 物理备份文件恢复到自建数据库.md#)或[RDS for MySQL 逻辑备份文件恢复到自建数据库](cn.zh-CN/常见问题/备份__恢复__迁移/RDS for MySQL 逻辑备份文件恢复到自建数据库.md#)。
2.  通过数据传输服务DTS将本地数据库迁移到新的RDS实例上。详情请参见[从自建MySQL迁移至RDS for MySQL](https://help.aliyun.com/document_detail/126875.htm)。

## SQL Server恢复方法 {#section_te0_6to_mdn .section}

您可以通过OSS上云的方式将数据恢复到新的RDS实例，详情请参见[全量备份数据上云SQL Server 2012/2016/2017版本](../../../../cn.zh-CN/RDS for SQL Server 用户指南/数据迁移/全量备份数据上云SQL Server 2012__2016__2017版本.md#)或[全量备份数据上云SQL Server 2008 R2版](../../../../cn.zh-CN/RDS for SQL Server 用户指南/数据迁移/全量备份数据上云SQL Server 2008 R2版.md#)。

