# Fast query cache

The fast query cache is a query cache that is developed by the Database Products Business Unit of Alibaba Cloud based on the native MySQL query cache. It uses a new design and implementation mechanism to increase the query performance of your ApsaraDB for RDS instance.

## Prerequisites

Your RDS instance runs MySQL 5.7 \(with a kernel version of 20200331 or later\).

## Background information

A query cache is a cache policy that allows you to expedite queries by saving CPU resources. It stores the text of each qualified statement with the result set that was returned. If an identical statement is received at a later time, the database server directly retrieves the result set from the query cache. This eliminates the need to analyze, optimize, and execute the statement again.

However, the native MySQL query cache has the following drawbacks in terms of design and implementation:

-   It cannot process a large number of concurrent queries at fast speeds. This speed is further reduced if multiple CPU cores are configured.
-   It cannot utilize memory resources properly or reclaim memory resources in a timely manner. This results in a waste of memory resources and low memory usage.
-   If the cache hit ratio is low, query performance does not increase and may even decrease.

Therefore, the native MySQL query cache is not widely used. This technology is no longer provided in the latest version of MySQL 8.0. In contrast, the fast query cache has the following benefits:

-   Optimized concurrency control

    The global locking mechanism that is used in the native MySQL query cache to synchronize the running of threads is removed. The fast query cache uses a new synchronization mechanism. This mechanism allows you to fully utilize the capability of multiple CPU cores and process a large number of concurrent queries at fast speeds.

-   Optimized memory management

    The memory preallocation mechanism used in the native MySQL query cache is removed. The fast query cache uses a dynamic memory allocation mechanism that is more flexible. This mechanism allows you to reclaim invalid memory resources in a timely manner and increase the utilization of memory resources.

-   Optimized caching

    The fast query cache detects cache usage dynamically and adjusts the cache policy in real time. This allows you to ensure stable query performance if the cache hit ratio is low or your RDS instance is used to process both read and write requests.


Unlike the native MySQL query cache, the fast query cache can be used in a wide range of business scenarios to increase query performance.

## Enable the fast query cache

For better query performance, you can reduce the memory space for the InnoDB buffer pool. However, we recommend that you increase the memory space for the fast query cache. The fast query cache is in the test invitation phase. If you are interested, [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

## Compare the performance of the native MySQL query cache and the fast query cache

For the following example, compare the queries per second \(QPS\) with different query cache configurations under the same conditions in various test cases. These query cache configurations are QC-OFF \(no query cache is enabled\), MySQL-QC \(the native MySQL query cache is enabled\), and RDS-QC \(the fast query cache is enabled\).

-   Test environment: a dedicated RDS instance with 4 CPU cores and 8 GB of memory
-   Test tool: SysBench
-   Test data volume: 250 MB \(25 tables in total, 40,000 records per table\)

-   Test case 1: Test the QPS for read-only queries with a cache hit ratio higher than 99%.

    The oltp\_point\_select script is used. Execute only primary key-based POINT SELECT statements. In addition, set the query cache size to 512 MB. This size is greater than the test data volume. It allows the cache hit ratio to reach more than 99%. In this test case, focus on how much the QPS increases based on the number of concurrent queries.

    |Number of concurrent queries|QC-OFF|MySQL-QC \(QPS increase compared with QC-OFF\)|RDS-QC \(QPS increase compared with QC-OFF\)|
    |----------------------------|------|----------------------------------------------|--------------------------------------------|
    |1|7,947|8,771 \(10.38%\)|9,196 \(15.72%\)|
    |8|61,685|65,686 \(6.49%\)|74,603 \(20.94%\)|
    |16|102,800|73,027 \(-28.96%\)|141,856 \(37.99%\)|
    |32|102,222|60,567 \(-40.75%\)|199,209 \(94.88%\)|
    |64|110,230|60,216 \(-45.37%\)|218,456 \(98.18%\)|
    |128|111,274|62,844 \(-43.52%\)|223,885 \(101.20%\)|
    |256|109,978|63,832 \(-41.96%\)|218,692 \(98.85%\)|
    |512|107,379|64,866 \(-39.59%\)|211,062 \(96.56%\)|
    |1,024|102,610|62,291 \(-39.29%\)|198,787 \(93.73%\)|

    ![QPS for read-only queries with a cache hit ratio higher than 99%](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6630749951/p96444.png)

    **Note:** Based on the test result, as the number of concurrent queries increases, the QPS of the native MySQL query cache sharply decreases. However, the QPS of the fast query cache remains stable and can even increase by up to 100%.

-   Test case 2: Test the QPS for read-only queries with a cache hit ratio higher than 80%.

    The oltp\_read\_only script is used. Run queries including range queries that each return more than one record. In addition, set the query cache size to 512 MB. This size ensures sufficient memory capacity and allows the cache hit ratio to reach more than 80%. In this test case, focus on how much the QPS increases based on the number of concurrent queries.

    |Number of concurrent queries|QC-OFF|MySQL-QC \(QPS increase compared with QC-OFF\)|RDS-QC \(QPS increase compared with QC-OFF\)|
    |----------------------------|------|----------------------------------------------|--------------------------------------------|
    |1|4,944|6,467 \(30.82%\)|6,860 \(38.77%\)|
    |8|28,195|28,651 \(1.62%\)|42,720 \(51.52%\)|
    |16|35,292|31,099 \(-11.88%\)|63,227 \(79.15%\)|
    |32|34,067|27,610 \(-18.95%\)|63,133 \(85.32%\)|
    |64|35,706|27,518 \(-22.93%\)|70,556 \(97.61%\)|
    |128|36,303|27,733 \(-23.61%\)|74,146 \(104.24%\)|
    |256|36,386|27,738 \(-23.77%\)|75,550 \(107.64%\)|
    |512|36,083|27,398 \(-24.07%\)|74,317 \(105.96%\)|
    |1,024|35,077|26,861 \(-23.42%\)|71,205 \(103.00%\)|

    ![QPS for read-only queries with a cache hit ratio higher than 80%](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7630749951/p96455.png)

    **Note:** Based on the test result, as the number of concurrent queries increases, the QPS of the native MySQL query cache significantly decreases. However, the QPS of the fast query cache can increase by up to 100%.

-   Test case 3: Test the QPS for read-only queries with a cache hit ratio of about 10%

    The oltp\_read\_only script is used. Run queries including range queries that each return more than one record. In addition, set the query cache size to 16 MB. This size results in insufficient memory capacity and deletion of cached data and allows the cache hit ratio to drop to about 10%. In this test case, focus on how much the QPS decreases based on the number of concurrent queries.

    |Number of concurrent queries|QC-OFF|MySQL-QC \(QPS increase compared with QC-OFF\)|RDS-QC \(QPS increase compared with QC-OFF\)|
    |----------------------------|------|----------------------------------------------|--------------------------------------------|
    |1|4,944|4,727 \(-4.38%\)|4,917 \(-0.54%\)|
    |8|28,195|22,542 \(-20.05%\)|27,897 \(-1.06%\)|
    |16|35,292|24,064 \(-31.81%\)|34,625 \(-1.89%\)|
    |32|34,067|21,330 \(-37.39%\)|33,592 \(-1.39%\)|
    |64|35,706|19,791 \(-44.57%\)|35,571 \(-0.38%\)|
    |128|36,303|19,519 \(-46.23%\)|36,055 \(-0.68%\)|
    |256|36,386|19,168 \(-47.32%\)|36,243 \(-0.39%\)|
    |512|36,083|18,420 \(-48.95%\)|35,679 \(-1.12%\)|
    |1,024|35,077|20,168 \(-42.50%\)|34,595 \(-1.37%\)|

    ![QPS for read-only queries with a cache hit ratio of about 10%](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7630749951/p96458.png)

    **Note:** Based on the test result, as the number of concurrent queries increases, the QPS of the native MySQL query cache significantly decreases by up to 50%. However, the fast query cache allows you to ensure that the QPS decrease is within 2%.

-   Test case 4: Test the QPS for read/write queries.

    The oltp\_read\_write script is used. Run transactions that each perform updates on tables. These frequent updates result in deletion of data from the query cache, and consequently the query cache is considered invalid. In this test case, focus on how much the QPS decreases based on the number of concurrent queries.

    |Number of concurrent queries|QC-OFF|RDS-QC \(QPS increase compared with QC-OFF\)|
    |----------------------------|------|--------------------------------------------|
    |1|4,188|4,199 \(0.27%\)|
    |8|21,587|21,263 \(-1.50%\)|
    |16|26,224|25,956 \(-1.02%\)|
    |32|27,887|27,741 \(-0.52%\)|
    |64|29,852|29,426 \(-1.43%\)|
    |128|30,024|29,724 \(-1.00%\)|
    |256|29,835|29,615 \(-0.74%\)|
    |512|29,525|29,683 \(0.54%\)|
    |1,024|29,905|29,512 \(-1.31%\)|

    ![QPS for read/write queries](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7630749951/p96466.png)

    **Note:** Based on the test result, as the number of concurrent queries increases, the fast query cache allows you to ensure that the QPS decrease is within 2%.


## Practice guidelines

Assume that you can determine the size of the data sets that need to be cached. For example, you enable a query cache on a specified table by using the SQL\_CACHE option. In this situation, you can evaluate the QPS by using the preceding test cases. A few more tips on using the fast query cache are as follows:

-   Enable the fast query cache in various scenarios
    -   The fast query cache aims to increase the QPS for read queries. We recommend that you enable the fast query cache if your RDS instance processes a large number of read queries but a small number of write queries. Otherwise, we recommend that you enable the fast query cache only for tables that are frequently read but to which data is infrequently written. You can enable the fast query cache for a specified table by using the SQL\_CACHE option. If your RDS instance processes a small number of read queries but a large number of write queries, the data of your RDS instance is frequently updated. In this situation, if you enable the fast query cache, the QPS may decrease by up to 2%.
    -   The QPS increase produced by the fast query cache varies based on the cache hit ratio. Before you enable the fast query cache for your RDS instance, we recommend that you obtain the hit ratio of the InnoDB buffer pool. If the hit ratio is lower than 80%, we recommend that you do not enable the fast query cache. The hit ratio of the InnoDB buffer pool is calculated by using the following formula: Hit ratio = \(1 - The value of the Innodb\_buffer\_pool\_reads parameter/The value of the Innodb\_buffer\_pool\_read\_requests parameter\) x 100%. You can also obtain the read/write ratio of each table from the TABLE\_STATISTICS table. If a table has a high read/write ratio, enable the fast query cache for the table by using the SQL\_CACHE option. For more information about how to query the TABLE\_STATISTICS table, see [Performance Insight](/intl.en-US/AliSQL Kernel/Performance Insight.md).
-   Manage the fast query cache by using the query\_cache\_type parameter

    The fast query cache is managed by using the same method as the native MySQL query cache. You can manage the fast query cache by using the **query\_cache\_type** parameter.

    |Parameter|Value|Description|
    |---------|-----|-----------|
    |**query\_cache\_type**|OFF|Disables the fast query cache. This is the default value.|
    |ON|Enables the fast query cache. However, you can use the SQL\_NO\_CACHE option to specify that your RDS instance does not retrieve result sets from the fast query cache.|
    |DEMAND|Disables the fast query cache. However, you can enable the fast query cache later by using the SQL\_CACHE option.|

    You can set the **query\_cache\_type** parameter for a specific session based on your business scenario.

    -   If your RDS instance processes a small number of read queries but a large number of write queries, the data of your RDS instance is frequently updated. In this situation, set the **query\_cache\_type** parameter to OFF for your RDS instance.
    -   If your RDS instance features a small volume of data, fixed query types, and high hit ratio, set the **query\_cache\_type** parameter to ON for your RDS instance.
    -   If your RDS instance features a large data volume, changing query types, and unstable hit ratio, set the **query\_cache\_type** parameter to DEMAND for your RDS instance. You can enable the fast query cache only for a specific statement by using the SQL\_CACHE option.
-   Specify a proper query cache size by using the query\_cache\_size parameter

    The query\_cache\_size parameter determines SQL statement execution efficiency. If you want to cache the results of queries that each return more than one record, you may need to specify a query cache size that is many times larger than the data volume. If you do not run range queries, you can evaluate the relationship between the data volume and the query\_cache\_size parameter as follows:

    -   Test environment: a dedicated RDS instance with 4 CPU cores and 8 GB of memory \(The size of the InnoDB buffer pool is set to 6 GB by using the innodb\_buffer\_pool\_size parameter.\)
    -   Test tool: SysBench
    -   Test data volume: 10 GB \(100 tables in total, 400,000 records per table\)
    Test case: Specify different cache sizes by using the query\_cache\_size parameter and execute the oltp\_point\_select script for each cache size. Make sure that 64 threads run concurrently to query data. In this case, hot data accounts for 20%. This way, you can obtain the impacts of different cache sizes on the QPS. The actual result set is 2.5 GB in size.

    |query\_cache\_size \(MB\)|QC-OFF|RDS-QC hit ratio|RDS-QC \(QPS increase compared with QC-OFF\)|
    |-------------------------|------|----------------|--------------------------------------------|
    |128|104,473|45%|110,483 \(5.75%\)|
    |256|104,473|72%|128,297 \(22.80%\)|
    |512|104,473|82%|137,153 \(31.28%\)|
    |1024|104,473|84%|133,624 \(27.90%\)|
    |2048|104,473|87%|125,766 \(20.38%\)|

    When you set the query\_cache\_size parameter, note the following information:

    -   If you can determine the result set size, set the query\_cache\_size parameter to a value that is `20% of the result set size`.
    -   If you cannot determine the result set size, set the query\_cache\_size parameter to a value that is `20% of the value of the innodb_buffer_pool_size parameter`.
    -   The memory capacity of your RDS instance is limited. We recommend that you properly adjust the values of the query\_cache\_size and innodb\_buffer\_pool\_size parameters at the same time. This allows you to refrain from exhausting the memory capacity that is allowed.

