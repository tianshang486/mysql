# Enable and disable SQL Audit \(database audit\) on an ApsaraDB RDS for PPAS instance

This topic describes how to enable and disable the SQL Audit feature of an ApsaraDB RDS for PPAS instance. This feature allows you to view and audit the SQL statements executed.

## Precautions

-   You cannot view the SQL logs that are generated before the SQL Audit feature is enabled.
-   The SQL Audit feature does not compromise the performance of your RDS instance.
-   The retention period of SQL logs is 30 days.
-   The retention period of the SQL log files that are exported from the SQL Audit feature is two days. The system deletes the SQL log files that are stored longer than two days.
-   The maximum length that the SQL Audit feature allows for an SQL statement is 2,000 bytes. The part that exceeds 2,000 bytes cannot be logged.
-   The SQL Audit feature is disabled by default. After this feature is enabled, you are charged additional fees. For more information, visit the [ApsaraDB for RDS](https://www.alibabacloud.com/product/apsaradb-for-rds?spm=a2796.7960336.224002.23.6c085179ylbVEv#pricing) product homepage.

## Enable the SQL Audit feature

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Data Security**.

5.  On the **SQL Audit** tab, click **Enable SQL Audit**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8450359951/p21214.png)

6.  In the message that appears, click **Confirm**.


After the SQL Audit feature is enabled, you can query SQL statements based on the specified search criteria, such as the time range, databases, users, and keywords.

## Disable the SQL Audit feature

If you no longer need the SQL Audit feature, you can disable it to reduce costs.

**Note:** After the SQL Audit feature is disabled, all of the SQL logs are deleted. Before you disable the SQL Audit feature, we recommend that you export the SQL logs as a file to your computer.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Data Security**.

5.  On the **SQL Audit** tab, click **Export File** to export the SQL logs as a file to your computer.

6.  After the file is exported, click **Disable SQL Audit**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8450359951/p34230.png)

7.  In the message that appears, click **Confirm**.


