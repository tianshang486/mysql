# Manage SQL statements

As your workloads grow over time, a large number of SQL statements are executed at low speeds. This causes frequent database failures that increase operations and maintenance \(O&M\) costs. To resolve this issue, you can use Alibaba Cloud Database Autonomy Service \(DAS\) to optimize tens of millions of SQL statements. This topic describes how to use DAS to analyze, identify, and optimize problem SQL statements.

## 10-second SQL analysis

In most cases, if your MySQL-running database instance encounters a sharp increase in the CPU utilization, number of active sessions, or response time, the common response is to execute the **SHOWPROCESSLIST** statement. However, this statement may return a large-sized result set that is difficult to analyze. To resolve this issue, DAS provides the **10-second SQL analysis** feature. This feature allows DAS to execute the **SHOW PROCESSLIST** statement at one-second intervals within a 10-second time window. Then, DAS analyzes all the returned result sets. Based on the analysis results, you can identify the most executed SQL statements and slowest SQL statements within the 10-second time window.

**Note:** One-second intervals indicate that DAS executes the statement on the first, third, fifth, seventh, and ninth seconds within the 10-second time window.

For more information, see [t1915607.dita\#multiTask403]().

## Slow SQL optimization

-   Slow SQL statements significantly decrease the stability of your database service. If your database instance encounters issues such as heavy load and unstable performance, we recommend that you check for slow SQL statements. This feature allows you to view the trends, execution, and optimization suggestions of slow SQL statements. You can view the slow SQL statements of a single database instance or all the database instances that are created within your Alibaba Cloud account. For more information about how to analyze slow SQL statements, see [Analyze slow query logs]().
-   DAS allows you to configure alerts for slow SQL statements. If the number of slow SQL statements exceeds the specified threshold, an alert is triggered. DAS can send the alert to you by using Short Message Service \(SMS\), email, or DingTalk. For more information, see [t1915614.md\#]().
-   DAS allows you to diagnose and optimize slow SQL statements. For more information, see [t1915616.md\#]().

## Full SQL analysis

This feature allows you to locate historical issues, obtain SQL stress testing templates, and determine whether to optimize slow SQL statements. For more information, see [Full SQL analysis]().

By default, the **full SQL analysis** feature is disabled on your database instance. For more information about how to enable this feature, see [Usage]().

You can also collect all SQL statements by using an on-premises database gateway. For more information about on-premises database gateways, see [t1915636.md\#](). For more information about how to collect all SQL statements by using an on-premises database gateway, see [CPU utilization]().

