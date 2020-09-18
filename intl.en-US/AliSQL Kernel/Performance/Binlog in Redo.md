# Binlog in Redo

The Binlog in Redo function synchronously writes binary logs to the redo log file when a transaction is committed. This reduces operations on disks and improves database performance.

Your RDS instance runs MySQL 8.0 \(with a kernel version of 20200430 or later\).

To ensure data security in crucial MySQL business scenarios, the system stores both binary and redo logs when a transaction is committed. Both the following parameters must be set to 1:

```
sync_binlog = 1;
innodb_flush_log_at_trx_commit = 1;
```

Each time a transaction is committed, the system performs two I/O operations. One is to write the binary logs to disks, and the other is to write the redo logs to disks. Although Group Commit is enabled for binary logs, the system must still wait for the two I/O operations to complete. This affects the efficiency of transaction processing, especially when standard or enhanced SSDs are used. The performance of I/O merging is based on the number of concurrent transactions that are committed at the same time. When the number of concurrent transactions is small, the performance is low. For example, when a small number of write transactions are committed, the system response is slow.

To increase the efficiency of committing transactions, AliSQL provides the Binlog in Redo function. You can enable the function by setting the `persist_binlog_to_redo` parameter to on. When a transaction is committed, the system synchronously writes binary logs to the redo log file and stores only the redo log file to disks. This reduces I/O consumption. The binary log files are then asynchronously stored to disks by using a separate thread at regular intervals. If a restart operation is triggered upon an exception, the system uses the binary logs in the redo log file to complement the binary log files. In this way, the database performance improves and the system response is faster. Also, the number of times that the binary log files are stored is reduced. This significantly relieves the pressure on the file system while increasing performance. This pressure can be resulted from the calls of the fsync functions that are triggered by file updates in real time. The fsync function synchronizes files to disks.

Binlog in Redo does not change the format of binary logs. Replication and third-party tools that are based on binary logs are not affected.

## Parameters

-   persist\_binlog\_to\_redo

    The switch that is used to enable or disable the Binlog in Redo function. This parameter is a global system variable. Valid values: on and off. The parameter change immediately takes effect. You do not need to restart your RDS instance.

    **Note:** If you want to enable Binlog in Redo, you only need to set the `persist_binlog_to_redo` parameter to on. You do not need to modify the settings of other parameters. The setting `sync_binlog = 1` automatically becomes invalid.

-   sync\_binlog\_interval

    The interval at which binary logs are asynchronously stored. This parameter is a global system variable. It takes effect only when the `persist_binlog_to_redo` parameter is set to on. Default value: 50. Unit: milliseconds \(ms\). In normal cases, the default value is recommended. The parameter change immediately takes effect. You do not need to restart your RDS instance.


## Stress testing

-   Test environment
    -   Application server: an Alibaba Cloud ECS instance
    -   RDS instance type: 32 CPU cores, 64 GB of memory, and enhanced SSDs
    -   RDS edition: High-availability Edition with asynchronous data replication
-   Test cases

    Sysbench provides the following test cases:

    -   oltp\_update\_non\_index
    -   oltp\_insert
    -   oltp\_write\_only
-   Test results
    -   oltp\_update\_non\_index

        After Binlog in Redo is enabled, the queries per second \(QPS\) significantly increases and the latency is low when the number of concurrent queries is small.

        ![oltp_update_non_index-QPS](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8630749951/p129994.png)

        ![oltp_update_non_index-laterncy](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8630749951/p129995.png)

    -   oltp\_insert

        After Binlog in Redo is enabled, the QPS significantly increases and the latency is low when the number of concurrent queries is small.

        ![oltp_insert-QPS](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8630749951/p129996.png)

        ![oltp_insert-latency](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8630749951/p129997.png)

    -   oltp\_write\_only

        After Binlog in Redo is enabled, the QPS slightly increases and the latency is low when the number of concurrent queries is small.

        ![oltp_write_only-QPS](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8630749951/p129998.png)

        ![oltp_write_only-latency](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9630749951/p129999.png)

    -   Number of times that the fsync function is called for binary logs

        After Binlog in Redo is enabled, the number of times is significantly reduced.

        ![Binlog Fsync](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9630749951/p130000.png)


## Test conclusion

-   oltp\_update\_non\_index and oltp\_insert test single-statement transactions, and the transactions are committed on a frequent basis. oltp\_write\_only tests multi-statement transactions, and the transactions are committed on a less frequent basis. This type of transaction contains two UPDATE statements, one DELETE statement, and one INSERT statement. Performance improvement in oltp\_update\_non\_index and oltp\_insert is more notable than that in oltp\_write\_only.
-   When the number of concurrent transactions is less than 256, Binlog in Redo significantly improves database performance and reduces latency. In most scenarios, Binlog in Redo provides significant benefits.
-   Binlog in Redo significantly reduces the number of times that the fsync function is called for binary logs. This improves the performance of the file system.

