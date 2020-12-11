# How do I ensure the timeliness of reading data on an ApsaraDB RDS for MySQL instance when the read/write splitting feature is enabled?

ApsaraDB RDS ensures real-time transmission of binary logs between primary and read-only RDS instances. In normal cases, no latency occurs when you read data from a read-only RDS instance. For more information about read-only RDS instances, see [Overview of read-only ApsaraDB RDS for MySQL instances](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md). However, the MySQL database engine has a limit in replication. If the binary logs require a long time to apply, latency occurs in data synchronization. This limit cannot be removed. To minimize the synchronization latency when you apply the binary logs, we recommend that you use a read-only RDS instance whose specifications are higher than or equal to those of the primary RDS instance.

ApsaraDB RDS allows you to set a [latency threshold](). If the latency on a read-only RDS instance exceeds the threshold, ApsaraDB RDS no longer forwards requests to the read-only RDS instance. If the latency on all read-only RDS instances exceeds the threshold, ApsaraDB RDS directly routes all requests to the primary RDS instance. This applies regardless of whether a non-zero read weight is configured for the primary RDS instance.

If you want to perform real-time data queries by using SQL statements after [read/write splitting](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Read/write splitting.md) is enabled, you can use hints to forcibly forward these statements to the primary RDS instance. Write the hints in the `/*FORCE_MASTER*/` format. Example:

```
/*FORCE_MASTER*/ SELECT * FROM table_name;
```

