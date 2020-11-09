# Features of AliSQL

This topic provides an overview of the features that are provided by AliSQL. It also provides a comparison between MySQL versions with AliSQL and other MySQL versions.

## Introduction to AliSQL

AliSQL is an independent MySQL branch that is developed by Alibaba Cloud. AliSQL provides all of the features that are available in the MySQL Community edition. AliSQL also provides some similar features that you can find in the MySQL Enterprise edition. These similar features include enterprise-grade backup and restoration, thread pool, and parallel query. In addition, AliSQL provides Oracle-compatible features, such as Sequence engine. ApsaraDB RDS for MySQL with AliSQL provides all the basic features of MySQL and a wide range of advanced features such as enterprise-grade security, backup and restoration, monitoring, performance optimization, and read-only instance.

## MySQL versions supported

|Category|Feature|Description|MySQL 8.0|MySQL 5.7|MySQL 5.6|
|--------|-------|-----------|---------|---------|---------|
|Functionality|[Thread Pool](/intl.en-US/Proprietary AliSQL/Feature/Thread Pool.md)|The thread pool feature separates threads from sessions. If a large number of sessions are created on your RDS instance, you can run a small number of threads to complete the tasks in active sessions.|Supported|Supported|Supported|
|[Statement outline](/intl.en-US/Proprietary AliSQL/Feature/Statement outline.md)|The statement outline feature allows you to stably run query plans by using optimizer and index hints. You can install the DBMS\_OUTLN package to use this feature.|Supported|Supported|Not supported|
|[Sequence Engine](/intl.en-US/Proprietary AliSQL/Feature/Sequence Engine.md)|The Sequence engine simplifies the generation of sequence values on your RDS instance.|Supported|Not supported|Supported|
|[Returning](/intl.en-US/Proprietary AliSQL/Feature/Returning.md)|This returning feature allows data manipulation language \(DML\) statements to return result sets. You can install the DBMS\_TRANS package to use this feature.|Supported|Not supported|Not supported|
|Performance|[A new version is available.](/intl.en-US/Proprietary AliSQL/Performance/Fast query cache.md)|The fast query cache is a query cache that is developed by Alibaba Cloud based on the native MySQL query cache. The fast query cache uses a new design and a new implementation mechanism to increase the query performance of your RDS instance.|Not supported|Supported|Not supported|
|[Binlog in Redo](/intl.en-US/Proprietary AliSQL/Performance/Binlog in Redo.md)|The Binlog in Redo feature synchronously writes binary logs to the redo log file when a transaction is committed. This reduces operations on disks and improves the performance of your RDS instance.|Supported|Not supported|Not supported|
|[Statement Queue](/intl.en-US/Proprietary AliSQL/Performance/Statement Queue.md)|The statement queue feature allows statements to queue in the same bucket. These statements may be executed on the same resources. For example, these statements are executed on the same row of a table. This feature reduces overheads from possible conflicts.|Supported|Supported|Not supported|
|[Inventory Hint](/intl.en-US/Proprietary AliSQL/Performance/Inventory Hint.md)|The inventory hint feature can work with the returning and statement queue features to rapidly commit and roll back transactions. This allows you to increase the throughput of your application.|Supported|Supported|Supported|
|Stability|[Faster DDL](/intl.en-US/Proprietary AliSQL/Stability/Faster DDL.md)|The faster DDL feature provides an optimized buffer pool management mechanism. This mechanism reduces the impact of data definition language \(DDL\) operations on the performance of your RDS instance. This mechanism also increases the number of concurrent DDL operations that are allowed.|Supported|Supported|Supported|
|[Statement concurrency control](/intl.en-US/Proprietary AliSQL/Stability/Statement concurrency control.md)|The concurrency control \(CCL\) feature allows you to control the concurrency of statements based on syntax rules. You can install the DBMS\_CCL package to use this feature.|Supported|Supported|Not supported|
|[Performance Agent](/intl.en-US/Proprietary AliSQL/Stability/Performance Agent.md)|The performance agent feature is provided as a plug-in of MySQL. You can use this feature to calculate and analyze the performance metrics of your RDS instance.|Supported|Supported|Supported|
|[Purge Large File Asynchronously](/intl.en-US/Proprietary AliSQL/Stability/Purge Large File Asynchronously.md)|The Purge Large File Asynchronously feature allows you to asynchronously delete files from your RDS instance. This ensures the stability of your RDS instance.|Supported|Supported|Supported|
|[Performance Insight](/intl.en-US/Proprietary AliSQL/Stability/Performance Insight.md)|The performance insight feature supports load monitoring, association analysis, and performance optimization at the instance level. You can evaluate loads on your RDS instance and resolve performance issues. This allows you to improve the stability of your RDS instance.|Supported|Supported|Not supported|
|Security|[Data Protect](/intl.en-US/Proprietary AliSQL/Security/Data Protect.md)|The data protection feature controls the permissions on delete operations. This allows you to protect your data from being accidentally deleted.|Supported|Supported|Supported|
|[Recycle bin](/intl.en-US/Proprietary AliSQL/Security/Recycle bin.md)|The recycle bin feature allows you to temporarily store deleted tables. It also allows you to specify a retention period within which you can retrieve the deleted tables. You can install the DBMS\_RECYCLE package to use this feature.|Supported|Not supported|Not supported|

## Features

|Category|Feature|MySQL Community edition|MySQL Enterprise edition|MySQL 5.7 and MySQL 8.0 with AliSQL|ApsaraDB RDS for MySQL|
|--------|-------|-----------------------|------------------------|-----------------------------------|----------------------|
|Enterprise-grade value-added services|[24/7 support](https://www.alibabacloud.com/zh/services/list)|Not supported|Supported|Supported|Supported|
|[Emergency troubleshooting](https://www.alibabacloud.com/zh/services/list)|Not supported|Supported|Supported|Supported|
|[Expert support](https://www.alibabacloud.com/zh/services/list)|Not supported|Supported|Supported|Supported|
|MySQL Features|[MySQL Database Server](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)|Supported|Supported|Supported|Supported|
|MySQL Document Store|Supported|Supported|Supported for MySQL 8.0|Supported for MySQL 8.0|
|MySQL Connectors|Supported|Supported|Supported for versions released to the public|Supported for versions released to the public|
|MySQL Replication|Supported|Supported|Supported|Supported|
|MySQL Router|Supported|Supported|MaxScale supported for MySQL 8.0|Single-tenant database proxies supported|
|MySQL Partitioning|Supported|Supported|Supported|Supported|
|[Storage Engine](/intl.en-US/Proprietary AliSQL/X-Engine/X-Engine overview.md)|InnoDB

MyISAM

NDB

|InnoDB

MyISAM

NDB

|InnoDB

X-Engine

|InnoDB

X-Engine |
|Oracle Compatibility|[Sequence Engine](/intl.en-US/Proprietary AliSQL/Feature/Sequence Engine.md)|Not supported|Not supported|Supported for MySQL 8.0|Supported for MySQL 8.0|
|MySQL Enterprise Monitor|[Enterprise Dashboard](/intl.en-US/RDS MySQL Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for MySQL instance.md)|Not supported|Supported|Under development|Enhanced Monitor|
|[Query Analyzer](/intl.en-US/RDS MySQL Database/Audit/SQL Explorer.md)|Not supported|Supported|Under development|Performance Insight|
|[Replication Monitor](/intl.en-US/RDS MySQL Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for MySQL instance.md)|Not supported|Supported|Under development|Supported|
|[Enhanced OS Metrics](/intl.en-US/RDS MySQL Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for MySQL instance.md)|Not supported|Not supported|Not supported|Enhanced Monitor|
|MySQL Enterprise Backup|[Hot backup for InnoDB](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md)|Not supported|Supported|Supported|Supported|
|[Full, Incremental, Partial, Optimistic Backups](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md)|Not supported|Supported|Supported|Database- and table-level backup supported|
|[Full, Partial, Selective, Hot Selective restore](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md)|Not supported|Supported|Supported|Database- and table-level restoration supported|
|[Point-In-Time-Recovery](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance.md)|Not supported|Supported|Supported|Supported|
|[Cross-Region Backup](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance across regions.md)|Not supported|Not supported|Not supported|Cross-region backup supported|
|[Recycle bin](/intl.en-US/Proprietary AliSQL/Security/Recycle bin.md)|Not supported|Not supported|Supported for MySQL 8.0|Supported for MySQL 8.0|
|[Flashback](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance.md)|Not supported|Not supported|Supported|Supported|
|MySQL Enterprise Security|[Enterprise TDE](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md)|Local key replacement supported|Supported|BYOK-based TDE and key rotation supported|BYOK-based TDE and key rotation supported|
|[Enterprise Disk Data Encryption at Rest](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md)|Not supported|Not supported|Not supported|BYOK-based disk encryption supported|
|[Enterprise Encryption](/intl.en-US/RDS MySQL Database/Data security/Configure SSL encryption on an ApsaraDB RDS for MySQL instance.md)|SSL|Supported|SSL|SSL|
|[Enterprise Audit](/intl.en-US/RDS MySQL Database/Audit/SQL Explorer.md)|Not supported|Supported|SQL Explorer supported|SQL Explorer supported|
|SM4 encryption algorithm|Not supported|Not supported|Supported|Supported|
|MySQL Enterprise Scalability|[Thread Pool](/intl.en-US/Proprietary AliSQL/Feature/Thread Pool.md)|Not supported|Supported|Supported for MySQL 8.0|Supported for MySQL 8.0|
|[Enterprise Readonly Request Extention](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md)|Not supported|Not supported|Supported|Read-only instances supported|
|MySQL Enterprise Reliability|[SQL Outline](/intl.en-US/Proprietary AliSQL/Feature/Statement outline.md)|Not supported|Not supported|Supported|Supported|
|[Hot Massive Update](/intl.en-US/Proprietary AliSQL/Performance/Inventory Hint.md)|Not supported|Not supported|Supported|Supported|
|[Hot SQL Limit](/intl.en-US/Proprietary AliSQL/Stability/Statement concurrency control.md)|Not supported|Not supported|Supported|Supported|
|[Hot SQL Firewall](/intl.en-US/Product Introduction/Why choose ApsaraDB for RDS/High security.md)|Not supported|Not supported|Supported|Supported|
|MySQL Enterprise High-Availability|[Enterprise Automatic Failover Switch](/intl.en-US/Product Introduction/Why choose ApsaraDB for RDS/High availability and disaster tolerance.md)|Not supported|Not supported|Third-party high-availability mechanism required|Supported for the RDS High-availability Edition|
|[Multi-Source Replication](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md)|Supported|Supported|Supported|Highly available read-only instances supported|

