# Functional modules of AliPG

This topic describes the functional modules that are provided by AliPG.

## Overview

|Category|Functional module|Description|
|--------|-----------------|-----------|
|Account permission|[rds\_superuser](/intl.en-US/RDS PostgreSQL Database/Account/Create an account for an ApsaraDB RDS for PostgreSQL instance.md)|The rds\_superuser role is a type of intermediate account between standard accounts and superuser accounts. The accounts that are assigned the rds\_superuser role are called privileged accounts. To ensure security on the cloud, AliPG does not provide superuser accounts. However, AliPG provides the rds\_superuser role. The rds\_superuser role does not have the sensitive security permissions that are owned by superuser accounts. The rds\_superuser role has the permissions to create and delete plug-ins, create and delete standard and privileged accounts, access and manage all of the tables that are created by standard accounts, and close connections.|
|Spatio-temporal database engine|[Ganos](/intl.en-US/Spatio-temporal Database/Overview.md)|Ganos is a spatio-temporal database engine that is developed by Alibaba Cloud. Ganos provides a series of data types, functions, and stored procedures to efficiently store, index, query, analyze, and compute spatio-temporal data.|
|External data reads and writes|[oss\_fdw](/intl.en-US/AliPG Kernel/Run cross-database queries/Read and write external data files by using oss_fdw.md)|The oss\_fdw plug-in supports data migration and hot-cold data separation. You can load data from Alibaba Cloud Object Storage Service \(OSS\) buckets to RDS instances. You can also write data from RDS instances to OSS buckets.|
|Concurrency control \(CCL\)|pg\_concurrency\_control|The pg\_concurrency\_control plug-in controls the concurrency of transactions, SQL queries, stored procedures, and data manipulation language \(DML\) operations and allows you to customize large queries. This expedites the execution of highly concurrent workloads.|
|Failover slot|[Failover Slot](/intl.en-US/AliPG Kernel/Failover slot.md)|In the PostgreSQL Community edition, logical slots cannot be automatically switched over to the new primary RDS instance in the event of a primary/secondary switchover. As a result, logical subscriptions are disconnected. In AliPG, the failover slot feature allows ApsaraDB for RDS to synchronize all logical slots from the primary RDS instance to the secondary RDS instance. This prevents the disconnection of logical subscriptions.|
|Bitmap function extension|varbitx|The varbitx plug-in of the PostgreSQL Community edition supports only simple BIT-type operation functions. In AliPG, the varbitx plug-in is extended to support more BIT-type operations in more scenarios. These scenarios include real-time user profile recommendation, access control advertising, and ticketing.|
|Vector search|[PASE](/intl.en-US/AliPG Kernel/Query vertical industry-specific data/Use the PASE plug-in.md)|PASE is a high-performance vector search index plug-in that is developed for AliPG. The PASE plug-in uses the following two well-developed, stable, and efficient approximate nearest neighbor \(ANN\) search algorithms: IVFFlat and Hierarchical Navigable Small World \(HNSW\). These algorithms are used to query vectors from PostgreSQL databases at high speeds. The PASE plug-in does not support the extraction or output of feature vectors. You must retrieve the feature vectors of the entities that you want to query. The PASE plug-in only implements a similarity search among a large amount of vectors that are identified based on retrieved feature vectors.|
|Log query|[log\_fdw](/intl.en-US/AliPG Kernel/Run cross-database queries/Use the log_fdw plug-in.md)|The log\_fdw plug-in queries logs from external tables.|
|Security|Security hardening|A security hardening module is built-in to improve custom views, enhance the security of the functions that you call, prevent security traps, and avoid the security vulnerabilities that are detected in the PostgreSQL Community edition.|

## References

[Plug-ins supported](/intl.en-US/AliPG Kernel/Plug-ins supported.md)

