# Benefits of X-Engine

This topic describes the benefits of X-Engine. X-Engine provides the same performance as InnoDB at 50% lower costs for storage.

## Background information

X-Engine is a storage engine that is developed by Alibaba Cloud to reduce the disk usage and overall database costs of ApsaraDB RDS for MySQL. X-Engine stores data in a tiered storage architecture and uses the Zstandard algorithm to compress data at a high compression ratio. You can understand the advantages of X-Engine over InnoDB and TokuDB by comparing their storage costs and performance.

**Note:** The major technological innovations of X-Engine have been released at three top academic conferences: ACM SIGMOD 2019 and VLDB2020 in the database field and the USENIX Conference on File and Storage Technologies \(FAST\) 2020 in the storage field.

## Test environment

The RDS instance used for testing is created with the rds.mysql.s3.large instance type and a storage capacity of 2 TB. This instance type supports four CPU cores and 8 GB of memory.

## 50% lower storage costs than InnoDB

![Disk usage comparison between X-Engine and InnoDB](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0630749951/p100884.png)

This figure compares disk usage between X-Engine and InnoDB.

Both X-Engine and InnoDB use their default configurations and the default schema that is provided by Sysbench. Each table contains 10 million data records, and the total number of tables increases from 32 to 736. As the data volume increases, the disk usage of X-Engine increases at a lower speed compared with InnoDB. The disk usage of X-Engine is up to 42% less than that of InnoDB. In addition, X-Engine requires less disk space to store large-sized individual data records. For example, after an image database is migrated to X-Engine, it occupies only 14% of the disk space that is required in InnoDB.

InnoDB does not compress data in most of its business scenarios. If data compression is enabled, the disk usage of InnoDB decreases by about 33%, but the query performance also decreases. For example, the performance for updates based on primary keys decreases by about 90%. This interrupts your business. X-Engine can compress data to reduce storage costs and maintain stable performance. The following tests are run by using Sysbench.

Run the following commands to test the performance:

```
# For an ApsaraDB RDS for MySQL instance that runs InnoDB
sysbench/usr/share/sysbench/oltp_update_index.lua\
    --mysql-host=[The endpoint of the RDS instance]\
    --mysql-user=sbtest\
    --mysql-password=sbtest\
    --mysql-db=sbtest\
    --threads=32\
    --tables=[32-736]\
    --table_size=10000000\
    --mysql-storage_engine=INNODB\
    prepare

# For an ApsaraDB RDS for MySQL instance that runs X-Engine
sysbench/usr/share/sysbench/oltp_update_index.lua\
    --mysql-host=[The endpoint of the RDS instance]\
    --mysql-user=sbtest\
    --mysql-password=sbtest\
    --mysql-db=sbtest\
    --threads=32\
    --tables=[32-736]\
    --table_size=10000000\
    --mysql-storage_engine=XENGINE\
    prepare
```

## Lower storage costs than TokuDB

TokuDB no longer offers low cost storage options. Also, Percona no longer offers support, maintenance, and updates for TokuDB. However, X-Engine offers lower storage costs than TokuDB. We recommend that you change the storage engine of your ApsaraDB RDS for MySQL instance from TokuDB to X-Engine.

TokuDB uses a fractal tree structure. This structure consists of more leaf nodes than the B+-tree structure that is used by InnoDB. These leaf nodes are populated with data records and stored as data blocks. Therefore, TokuDB supports a higher data compression ratio than InnoDB. However, the fractal tree structure does not support tiered storage. The tiered storage architecture of X-Engine not only consists of blocks that are populated with data records but also offers optimized storage. This reduces the storage costs of X-Engine.

![Comparison of disk usage between X-Engine and TokuDB](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0630749951/p100943.png)

This figure compares disk usage between X-Engine and TokuDB.

A total of 32 tables are created on the RDS instance used for testing. Each table contains 100 million data records. These data records occupy 411 GB of disk space in TokuDB and 400 GB of disk space in X-Engine. This proves the improvements and advantages of X-Engine over TokuDB in terms of storage costs.

Run the following commands to test the performance:

```
# For an ApsaraDB RDS for MySQL instance that runs TokuDB
sysbench/usr/share/sysbench/oltp_update_index.lua\
    --mysql-host=[The endpoint of the RDS instance]\
    --mysql-user=sbtest\
    --mysql-password=sbtest\
    --mysql-db=sbtest\
    --threads=32\
    --tables=[32-736]\
    --table_size=1000000000\
    --mysql-storage_engine=TokuDB\
    prepare

# For an ApsaraDB RDS for MySQL instance that runs X-Engine
sysbench/usr/share/sysbench/oltp_update_index.lua\
    --mysql-host=[The endpoint of the RDS instance]\
    --mysql-user=sbtest\
    --mysql-password=sbtest\
    --mysql-db=sbtest\
    --threads=32\
    --tables=[32-736]\
    --table_size=1000000000\
    --mysql-storage_engine=XENGINE\
    prepare
```

## Tiered storage and tiered access to increase QPS

X-Engine reduces the disk usage for cold data to lower the overall storage costs and maintains a stable rate of queries per second \(QPS\) for hot data. The following content describes how X-Engine increases the QPS and reduces storage costs:

-   The tiered storage architecture of X-Engine allows you to store hot and cold data at different tiers and compress cold data by default.
-   X-Engine applies technologies such as prefix encoding to every data record. This reduces storage costs.
-   In most of the actual business scenarios, data is skewed because the volume of hot data is smaller than that of cold data. The tiered access architecture of X-Engine allows you to increase the QPS.

![Performance of point queries](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0630749951/p100915.png)

This figure shows the performance of X-Engine for processing point queries on skewed data.

This test uses the popular method of Zipf distribution to control the degree of data skew. If the degree of data skew \(namely, the Zipf factor\) is high, more point queries hit hot data in the cache instead of cold data on disks. This decreases the access latency and increases the QPS. In addition, the compression of cold data only has a small impact on the QPS.

The tiered storage and tiered access architectures of X-Engine reduces the probability that SQL statements for hot data hit cold data. These architectures increase the QPS by 2.7 times than when all data is evenly accessed.

Run the following commands to test the performance:

```
sysbench/usr/share/sysbench/oltp_point_select.lua\
    --mysql-host=[The endpoint of the RDS instance]\
    --mysql-user=sbtest\
    --mysql-password=sbtest\
    --time=3600\
    --mysql-db=sbtest\
    --tables=32\
    --threads=512\
    --table_size=10000000\
    --rand-type=zipfian\
    --rand-zipfian-exp=[0-1]\
    --report-interval=1\
    run
```

## Equally matched performance of X-Engine and InnoDB for cold data queries

X-Engine and InnoDB offer an equally matched QPS and transactions per second \(TPS\) for processing queries to a large volume of cold data, especially archived and historical data.

![Performance for processing queries to cold data](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0630749951/p100960.png)

This figure compares cold data query performance between InnoDB and X-Engine.

In most of the online transactional processing \(OLTP\) scenarios, X-Engine and InnoDB offer equally matched performance for processing frequent updates \(oltp\_update\_index and oltp\_write\_only\) and point queries \(oltp\_point\_select\).

However, when X-Engine queries data for a specific time range or checks the uniqueness of a single data record, it performs a scan or access to multiple storage tiers. As a result, X-Engine processes range queries \(oltp\_read\_only\) and inserts \(OLTP\_insert\) at a slightly lower speed than InnoDB.

X-Engine processes data reads and writes \(oltp\_read\_write\) at the same speed as InnoDB.

Run the following commands to test the performance:

```
# oltp_read_only is used as an example.
sysbench/usr/share/sysbench/oltp_read_only.lua\
    --mysql-host=[The endpoint of the RDS instance]\
    --mysql-user=sbtest\
    --mysql-password=sbtest\
    --mysql-db=sbtest\
    --time=3600\
    --tables=32\
    --threads=512\
    --table_size=10000000\
    --rand-type=uniform\
    --report-interval=1\
    run
```

## Summary

X-Engine is a storage engine that is tailored to the cost-effectiveness requirements of ApsaraDB RDS for MySQL. It offers performance that is comparable to InnoDB but at lower storage costs. X-Engine has been used in a number of core business of Alibaba Group. These include DingTalk chat history databases, Taobao image databases, and Taobao transaction history databases. For more information, see [X-Engine overview](/intl.en-US/Proprietary AliSQL/X-Engine/X-Engine overview.md).

## Get started with X-Engine

-   If you are new to ApsaraDB RDS for MySQL, select X-Engine as the storage engine when you create an RDS instance. For more information, see [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md).
-   You can also change the storage engine of your RDS instance to X-Engine. For more information, see [Convert the storage engine from InnoDB, TokuDB, or MyRocks to X-Engine](/intl.en-US/Proprietary AliSQL/X-Engine/Convert the storage engine from InnoDB, TokuDB, or MyRocks to X-Engine.md).

