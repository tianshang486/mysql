# SQL Explorer {#task_msp_gz1_mfb .task}

This topic describes how to use the SQL Explorer function. ApsaraDB RDS for MySQL has upgraded the SQL audit function as SQL Explorer, which continues to provide security audit and performance diagnosis but has more diverse features and costs much less. The upgrade process does not affect the RDS for MySQL instances.

The SQL Explorer function is available only to the following DB engine versions and editions:

-   MySQL 8.0 High-availability Edition \(with local SSDs\)
-   MySQL 5.7 High-availability Edition
-   MySQL 5.6
-   MySQL 5.5

With the SQL Explorer function enabled, the system records information about all DML and DDL operations. The information is obtained through network protocol analysis and consumes only a small amount of CPU resources. The Trial Edition can retain SQL log data of one day free of charge. If you want to retain your SQL log data for more than one day, you must pay for storage.

## Scenarios {#section_c38_e6y_ueg .section}

The SQL Explorer function is suitable to the following scenarios:

-   The enterprise has high requirements on data security. Such enterprises come from the finance, security, stocks, governmental affairs, and insurance sectors.
-   The database running needs to be analyzed to locate problems or verify SQL statement performance.
-   The data needs to be restored by using the SQL statements in SQL log data.

## Differences between SQL log and binary log {#section_8uf_fji_bae .section}

You can view incremental data through SQL log or binary log. However, these two types of logs are different:

-   SQL log: similar to the auditing log of MySQL and records information about all DML and DDL operations. The information is obtained through network protocol analysis. SQL log does not parse the actual parameter values, and therefore a small amount of data may be lost if a large amount of SQL query statements are executed. If you collect statistics on incremental data by using SQL log, the obtained incremental data may be lost.
-   Binary log: records information about all add, delete, and modify operations and the incremental data used for data restoration. Binary log data is temporarily stored in the RDS instance. The system periodically transfers full binary log files to OSS. OSS then stores the files for seven days. However, the binary log files to which data is being written cannot be saved. Therefore, some binary log files may fail to be uploaded to OSS. Binary log accurately records the incremental data but cannot help you obtain real-time log data.

## Precautions {#section_rs8_3vo_yxe .section}

The time range for online query extends up to 24 hours. This is because SQL Explorer records all database-related operations, which involve a large amount of SQL statements. If the time range exceeds 24 hours, the query takes a long time and may even time out.

**Note:** If you want to query SQL log data within a time range longer than 24 hours, we recommend that you export the SQL log data to your computer and then query the needed data.

## Features {#section_ltz_buz_0f3 .section}

-   SQL log

    SQL log records all operations that have been performed on databases. With SQL log, you can do database troubleshooting, action analysis, and security audit.

-   Enhanced search

    You can search data by database, user, client ID, thread ID, execution time, or the number of scanned rows. You can also export and download the search results.

    ![SQL洞察特性功能](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156810245013817_en-US.png)

-   SQL analysis

    This new feature provides visualized interactive analysis of SQL log of a specified time period. You can use this feature to locate abnormal SQL statements and performance issues.

-   Cost reduction

    SQL explorer adopts the column-based storage and compression technology to reduce the SQL log size and reduce storage costs by about 60%. The hourly fee is US$ 0.0018 per GB.


## Activate SQL Explorer {#section_rxq_cwr_glt .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located. 

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156810245037169_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **SQL Explorer**.
5.  Click **Activate Now**. 

    ![立即开通](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156810245013750_en-US.png)

6.  Specify the SQL log storage duration \(for how long you want to keep the SQL log\), and click **Activate**. 

    **Note:** When the storage duration of an SQL log file exceeds the specified duration, the file is deleted.

    -   Trial Edition: You can use SQL Explorer for a long time. However, the SQL log files are retained for only one day, which means that you can query only the SQL log data of one day. Additionally, you cannot use advanced functions such as data export, and data integrity cannot be guaranteed.
    -   Non-Trial Edition: The SQL log files can be stored for 30 days, six months, one year, three years, or five years. You are charged an hourly fee of USD 0.0018 per GB.
    ![选择存储时长](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156810245013755_en-US.png)


## Change the SQL log storage duration {#section_xou_s8d_59s .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/)
2.  In the upper-left corner, select the region where the target RDS instance is located. 

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156810245037169_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **SQL Explorer**.
5.  Click **Service Settings**. 

    ![服务设置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156810245013804_en-US.png)

6.  Change the storage duration as needed. 

    ![修改存储时长](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156810245113805_en-US.png)


## Disable SQL Explorer {#section_e12_do8_eix .section}

**Note:** If you disable the SQL Explorer function, the existing SQL log files are deleted. We recommend that you export and save the SQL log file to your computers before you disable the function.

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located. 

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156810245037169_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **SQL Explorer**.
5.  Click **Export**. 

    ![到处SQL审计日志](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156810245113823_en-US.png)

6.  In the displayed dialog box, click **OK**.
7.  After the export is complete, click **View Exported List** and download the log file to your computer. 

    ![下载SQL审计日志](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156810245113831_en-US.png)

8.  Click **Service Settings**. 

    ![服务设置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156810245013804_en-US.png)

9.  Click the switch next to **Activate SQL Explorer** to disable SQL Explorer. 

    ![关闭SQL Explorer](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156810245113807_en-US.png)


## FAQ {#section_kya_bgw_lhz .section}

How do I obtain the SQL log size after enabling SQL Explorer?

Log on to the RDS console. In the upper-right corner, choose **Billing Management** \> **Billing Management**. In the left-side navigation pane, choose **Spending Summary** \> **Instance Spending Detail**. Then you can find the SQL log size for the target RDS instance.

![SQL洞察日志大小](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156810245139928_en-US.png)

**Note:** **SQL auditing** indicates the SQL log size.

