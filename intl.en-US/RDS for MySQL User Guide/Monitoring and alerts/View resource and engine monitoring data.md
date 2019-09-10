# View resource and engine monitoring data {#concept_sp4_jgl_jgb .concept}

This topic describes how to view the resource and engine monitoring data of an RDS for MySQL instance. ApsaraDB for RDS provides a wide range of performance metrics for you to view in the RDS console.

CloudDBA provides intelligent diagnosis and optimization for monitoring services.

## Procedure {#section_m3j_zlb_3gb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156810193736543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Monitoring and Alerts**.
5.  On the Monitoring tab, select the **Resource Monitoring** or **Engine Monitoring** monitoring type and specify the time range. The following table describes the monitoring metrics.

    |Monitoring Type|Metric|Description|
    |---------------|------|-----------|
    |**Resource Monitoring**|Disk Space \(MB\)|The disk space usage of the instance, including:     -   Instance Size
    -   Data Usage
    -   Log Size
    -   Temporary File Size
    -   Other System File Size
 Unit: MByte.

 |
    |IOPS \(Input/Output Operations per Second\)|The number of I/O requests per second for the instance. Unit: Number/second.|
    |Total Connections|The total number of connections to the instance, including the number of active connections and the total number of connections.|
    |CPU and Memory Usage \(%\)|The CPU and memory usage of the instance \(excluding the CPU and memory usage for the operating system\).|
    |Network Traffic \(KB\)|The input and output traffic of the instance per second. Unit: KB.|
    |**Engine Monitoring**|TPS \(Transactions per Second\)/QPS \(Queries per Second\)|The average number of transactions per second and the average number of SQL statements executed per second.|
    |InnoDB Buffer Pool Read Hit Ratio, Usage Ratio, and Dirty Block Ratio \(%\)|The read hit ratio, usage, and proportion of dirty blocks for the InnoDB buffer pool.|
    |InnoDB Read/Write Volume \(KB\)|The amount of data that is read and written by InnoDB per second. Unit: KB.|
    |InnoDB Buffer Pool Read/Write Frequency|The number of read and write operations that are performed by InnoDB per second.|
    |InnoDB Log Read/Write/fsync|The average frequency of physical writes to log files per second by InnoDB, the log write request frequency, and the average frequency of fsync \(\) writes to log files.|
    |Number of Temporary Tables Created Automatically on the Hard Disk when MySQL Statements Are Being Executed|The number of temporary tables that are automatically created on the hard disk when the instance runs SQL statements.|
    |MySQL\_COMDML|The number of SQL statements that are executed by the instance per second, including:     -   Insert
    -   Delete
    -   Insert\_Select
    -   Replace
    -   Replace\_Select
    -   Select
    -   Update
 |
    |MySQL\_RowDML|The number of operations that are performed by InnoDB per second, including:     -   The average number of physical writes to log files per second
    -   The number of rows that are read/updated/deleted/inserted from InnoDB tables per second.
 |
    |MyISAM Read/Write Frequency|The number of read/write operations that are performed by MyISAM on the buffer pool per second and the number of read/write operations that are performed by MyISAM on the hard disk per second.|
    |MyISAM Key Buffer Read/Write/Usage Ratio \(%\)|The read hit ratio, write hit ratio, and usage of the MyISAM key buffer per second.|


