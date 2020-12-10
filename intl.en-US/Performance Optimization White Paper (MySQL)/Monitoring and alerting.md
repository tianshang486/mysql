# Monitoring and alerting

ApsaraDB RDS provides a number of metrics that you can use to monitor the performance of your ApsaraDB RDS instance. ApsaraDB RDS also allows you to configure alert rules for these metrics. If the value of a metric meets the specified alert conditions, an alert is triggered. ApsaraDB RDS sends the alert to all the contacts in the associated alert group.

Monitoring and alerting are two important modules of the ApsaraDB RDS architecture. These modules are crucial to daily operations and maintenance \(O&M\). You can use these modules to obtain the running status of your RDS instance in a timely manner. You can also use these modules to identify and handle the potential risks that may affect your workloads.

You can view the resource monitoring, engine monitoring, and deployment monitoring data of your RDS instance in the ApsaraDB RDS console. For more information, see [View the resource and engine metrics of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for MySQL instance.md).

The following table describes the metrics that are supported by ApsaraDB RDS for MySQL.

|Monitoring type|Metric|Description|
|---------------|------|-----------|
|**Resource Monitoring**|Disk Space|The disk usage of the RDS instance, including: -   Instance size
-   Data usage
-   Log size
-   Temporary file size
-   Other system file size

Unit: MB. |
|IOPS|The number of input/output operations per second \(IOPS\) of the RDS instance.|
|Total Connections|The number of active connections to the RDS instance and the total number of connections to the RDS instance.|
|CPU Utilization and Memory Usage|The CPU utilization and memory usage of the RDS instance. This excludes the CPU utilization and memory usage for the operating system. Unit: %.|
|Network Traffic|The volume of inbound traffic to the RDS instance per second and the volume of outbound traffic from the RDS instance per second. Unit: KB.|
|**Engine Monitoring**|TPS/QPS|The average number of transactions per second \(TPS\) and the average number of SQL statements executed per second.|
|InnoDB Buffer Pool Read Hit Ratio, Usage Ratio, and Dirty Block Ratio|The read hit ratio, dirty ratio, and usage of the InnoDB buffer pool. Unit: %.|
|InnoDB Read/Write Volume|The volume of data read from InnoDB per second and the volume of data written to InnoDB per second. Unit: KB.|
|InnoDB Buffer Pool Read/Write Frequency|The number of reads from InnoDB per second and the number of writes to InnoDB per second.|
|InnoDB Log Read/Write/fsync|The number of physical writes to log files, number of log write requests, and number of writes that are completed by calling the fsync function to log files by InnoDB per second.|
|Temporary Tables Automatically Created on Hard Disk when MySQL Statements Are Executed|The number of temporary tables that the RDS instance creates on the hard disk when executing SQL statements.|
|MySQL\_COMDML|The number of SQL statements that the RDS instance executes per second. ApsaraDB for RDS supports the following SQL statements: -   INSERT
-   DELETE
-   INSERT\_SELECT
-   REPLACE
-   REPLACE\_SELECT
-   SELECT
-   UPDATE |
|MySQL\_RowDML|The number of operations that InnoDB performs per second, including: -   The number of physical writes to log files per second.
-   The number of rows on which InnoDB performs operations per second. This includes the number of rows that are read from InnoDB tables per second, the number of rows that are updated in InnoDB tables per second, the number of rows that are deleted from InnoDB tables per second, and the number of rows that are inserted into InnoDB tables per second. |
|MyISAM Read/Write Frequency|The number of reads from the buffer pool by MyISAM per second, the number of writes to the buffer pool by MyISAM per second, the number of reads from the hard disk by MyISAM per second, and the number of writes to the hard disk by MyISAM per second.|
|MyISAM Key Buffer Read/Write/Usage Ratio|The read hit ratio, write hit ratio, and usage of the MyISAM key buffer per second.|
|Running Threads|The number of active threads and the number of connected threads.|
|**Deploy Monitoring**|Replication Thread Status of Secondary Instances|The status of the threads that replicate data to the secondary RDS instance.-   I/O thread: The value 1 indicates that the thread is normal, and the value 0 indicates that the thread is lost.
-   SQL thread: The value 1 indicates that the thread is normal, and the value 0 indicates that the thread is lost. |
|Replication Latency of Secondary Instances|The latency of data replication to the secondary RDS instance. Unit: seconds.|

You can configure alert rules for the metricsin the [Cloud Monitor console](https://cms-intl.console.aliyun.com). For more information, see the following topics:

-   [Create an alert contact or alert group](/intl.en-US/Alarm service/Alert contacts/Create an alert contact or alert group.md)
-   [Create a threshold-triggered alert rule](/intl.en-US/Alarm service/Alarm rules/Create a threshold-triggered alert rule.md)

