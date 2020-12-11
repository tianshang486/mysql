# View the resource and engine metrics of an ApsaraDB RDS for MariaDB instance

This topic describes how to view the resource and engine metrics of an ApsaraDB RDS for MariaDB instance in the ApsaraDB RDS console.

## Procedure

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).
2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.
4.  In the left-side navigation pane, click **Monitoring and Alerts**.
5.  On the Monitoring tab, select the **Resource Monitoring** or **Engine Monitoring** type and specify a time range. Then, you can view the metrics that appear. The following table describes the metrics.

    |Monitoring type|Metric|Description|
    |---------------|------|-----------|
    |**Resource Monitoring**|IOPS|The numbers of input/output operations per second \(IOPS\) of the data and log disks.|
    |CPU Utilization and Memory Usage|The CPU utilization and memory usage of the RDS instance.|
    |Disk Space|The disk usage of the RDS instance. Unit: MB.|
    |Total Connections|The number of active connections to the RDS instance and the total number of connections to the RDS instance.|
    |Network Traffic|The volume of inbound traffic to the RDS instance per second and the volume of outbound traffic from the RDS instance per second. Unit: KB.|
    |**Engine Monitoring**|Transactions per Second \(TPS\)/Queries per Second \(QPS\)|The average number of transactions per second \(TPS\) and the average number of SQL statements executed per second.|
    |InnoDB Buffer Pool Read Hit Ratio, Usage Ratio, and Dirty Block Ratio|The read hit ratio, dirty ratio, and usage of the InnoDB buffer pool. Unit: %.|
    |InnoDB Read/Write Volume|The volume of data read from InnoDB per second and the volume of data written to InnoDB per second. Unit: KB.|
    |InnoDB Buffer Pool Read/Write Frequency|The number of reads from InnoDB per second and the number of writes to InnoDB per second.|
    |InnoDB Log Read/Write/fsync|The number of physical writes to log files, number of log write requests, and number of writes that are completed by calling the fsync function to log files by InnoDB per second.|
    |Temporary Tables Automatically Created on Hard Disk when MySQL Statements Are Executed|The number of temporary tables that the RDS instance creates on the hard disk when executing SQL statements.|
    |MySQL\_COMDML|The number of SQL statements that the RDS instance executes per second. ApsaraDB RDS supports the following SQL statements:     -   INSERT
    -   DELETE
    -   INSERT\_SELECT
    -   REPLACE
    -   REPLACE\_SELECT
    -   SELECT
    -   UPDATE |
    |MySQL\_RowDML|The number of operations that InnoDB performs per second, including:     -   The number of physical writes to log files per second.
    -   The number of rows on which InnoDB performs operations per second. This includes the number of rows that are read from InnoDB tables per second, the number of rows that are updated in InnoDB tables per second, the number of rows that are deleted from InnoDB tables per second, and the number of rows that are inserted into InnoDB tables per second. |
    |MyISAM Read/Write Frequency|The number of reads from the buffer pool by MyISAM per second, the number of writes to the buffer pool by MyISAM per second, the number of reads from the hard disk by MyISAM per second, and the number of writes to the hard disk by MyISAM per second.|
    |MyISAM Key Buffer Read/Write/Usage Ratio|The read hit ratio, write hit ratio, and usage of the MyISAM key buffer per second.|


