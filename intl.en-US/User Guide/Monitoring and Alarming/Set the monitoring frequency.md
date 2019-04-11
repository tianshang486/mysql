# Set the monitoring frequency {#concept_ug4_x5p_wdb .concept}

## Background information {#section_uxl_cvp_wdb .section}

The RDS console provides abundant performance metrics for you to conveniently view and know the running status of instances. You can use the RDS console to set the monitoring frequency, view monitoring data of a specific instance, create monitoring views, and compare instances of the same type under the same account.

**Two monitoring frequencies provided before May 15, 2018**

-   Once per 60 seconds \(monitoring period: 30 days\)
-   Once per 300 seconds \(monitoring period: 30 days\)

**Second-level monitoring frequency introduced since May 15, 2018**

Minute-level monitoring frequencies cannot meet monitoring requirements of some users and maintenance personnel. Therefore, since May 15, 2018, RDS has introduced second-level monitoring frequencies. This facilitates problem locating and improves customer satisfaction.

-   **Once per 5 seconds \(monitoring period: 7 days\), turning to once per minute since the eighth day**
-   The detailed monitoring policies are described in the following table.

    |Instance type|Once per 5 seconds|Once per minute \(60 seconds\)|Once per 5 minutes \(300 seconds\)|
    |-------------|------------------|------------------------------|----------------------------------|
    |Basic Edition|Not supported|Supported for free|Default configuration|
    |High-availability or Finance Edition: Memory < 8 GB|Not supported|Supported for free|Default configuration|
    |High-availability or Finance Edition: Memory \>= 8 GB|Supported \(Not free\)|Default configuration|Supported for free|


## Restrictions {#section_t54_fvp_wdb .section}

-   You can configure second-level monitoring for instances that meet the following conditions:
    -   The instance is located in these regions: China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Beijing\), or China \(Shenzhen\)
    -   The instance is an RDS for MySQL instance.
    -   The instance storage type is local SSD.
    -   The instance memory space is 8 GB or more.
-   All engines \(MySQL, SQL Server, ProstgraSQL, and PPAS\) and database versions support the following monitoring frequencies:
    -   Once per 60 seconds
    -   Once per 300 seconds

## Procedure {#section_vrd_hvp_wdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.
3.  Click the ID of the target instance to enter the Basic Information page.
4.  Click **Monitoring and Alarms** in the left-side navigation pane.

    **Note:** Different types of databases support different metrics. For more information, see **List of monitoring items** at the end of this document.

5.  Click the **Monitoring** tab.
6.  Click **Set Monitoring Frequency**.
7.  Select the monitoring frequency in the Set Monitoring Frequency dialog box and click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7952/15549505043104_en-US.png)

8.  In the displayed Confirm dialog box, click **OK**.
9.  On the Monitoring page, perform the following operations:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7952/15549505043107_en-US.png)

    **Interface description:**

    |No.|Description|
    |---|-----------|
    |1|Select the monitoring type.|
    |2|Select the monitoring period.|
    |3|Set the monitoring frequency.|
    |4|Refresh monitoring results.|
    |5|View monitoring results.|
    |6|Select monitoring items.|


## List of monitoring items {#section_mfg_4vp_wdb .section}

**RDS for MySQL/MariaDB**

|Monitoring items|Description|
|----------------|-----------|
|Disk Space|Disk space usage of the instance, including:-   Overall usage of the disk space
-   Data space usage
-   Log space usage
-   Temporary file space usage
-   System file space usage

Unit: MB

|
|IOPS|Number of I/O request times of an instance per second. Unit: time/second|
|Total Connections|Total number of current connections, including the number of active connections and total connections|
|CPU and Memory Usage|CPU usage and memory usage of an instance \(excluding the memory used by OS\)|
|Network Traffic|Incoming/outgoing traffic of an instance per second. Unit: KB|
|QPS/TPS|Number of SQL statements executed and transactions processed per second|
|InnoDB Buffer Pool|InnoDB buffer pool read hit rate, utilization rate, and percentage of dirty data blocks|
|InnoDB Read/Write Volume|Average InnoDB data read and write times per second. Unit: KB|
|Number of InnoDB Read and Write Times Per Second|Number of read and write times per second of InnoDB|
|InnoDB Log|Number of InnoDB physical writes to a log file, log write requests, and FSYNC writes to a log file per second|
|Temporary Tables|Number of temporary tables created automatically on the hard disk when the database executes SQL statements|
|MyISAM Key Buffer|Average key buffer read hit rate, write hit rate, and usage per seconcd of MyISAM|
|MyISAM Read and Write Times|Number of MyISAM read and write times from/to the buffer pool and from/to the hard disk per second|
|COMDML|Number of statements executed on the database per second. The statements include:-   `Insert`
-   `Delete`
-   `Insert_Select`
-   `Replace`
-   `Replace_Select`
-   `Select`
-   `Update`

|
|ROWDML|Number of operations performed on InnoDB, including:-   Number of physical writes to a log file per second
-   Number of rows read in InnoDB tables per second
-   Number of rows updated, deleted, and inserted in InnoDB tables per second

|

**RDS for SQL Server**

|Monitoring items|Description|
|----------------|-----------|
|Disk Space|Disk space usage of the instance, including:-   Overall usage of the disk space
-   Data space usage
-   Log space usage
-   Temporary file space usage
-   System file space usage

Unit: MB

|
|IOPS|Number of I/O request times of an instance per second. Unit: time/second|
|Connections|Total number of current connections, including the number of active connections and total connections|
|CPU usage|CPU usage \(including CPU used by OS\) of an instance|
|Network traffic|Incoming/outgoing traffic of an instance per second. Unit: KB|
|TPS|Number of transactions processed per second|
|QPS|Number of SQL statements executed per second|
|Cache hit rate|Read hit rate of the buffer pool|
|Average full table scans per second|Average number of full table scan times per second|
|SQL compilations per second|Number of compiled SQL statements per second|
|Page writes of the checking point per second|Number of page write times of the checking point in an instance per second|
|Logons per second|Number of logons per second|
|Lock timeouts per second|Number of lock expiration times per second|
|Deadlocks per second|Number of deadlocks in an instance per second|
|Lock waits per second|Number of lock waiting times per second|

**RDS for PostgreSQL**

|Monitoring item|Description|
|---------------|-----------|
|Disk Space|Usage of the instance disk space. Unit: MB|
|IOPS|Number of I/O request times of the data disk and log disk in an instance per second. Unit: time/second|

**RDS for PPAS**

|Monitoring item|Description|
|---------------|-----------|
|Disk Space|Usage of the instance disk space. Unit: MB|
|IOPS|Number of I/O request times of the data disk and log disk in an instance per second. Unit: time/second|

