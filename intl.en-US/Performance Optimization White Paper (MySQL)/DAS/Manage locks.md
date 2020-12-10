# Manage locks

Alibaba Cloud Database Autonomy Service \(DAS\) provides the lock analysis feature. This feature allows you to view and analyze deadlocks that are recently triggered on your database instance.

The **lock analysis** feature allows you to view and analyze the deadlocks that are triggered over a specified time period on your database instance. The time period is accurate to minute or second. Based on the analysis results, you can immediately diagnose and resolve the recent deadlocks. On the **Deadlock Analysis** page, you can view the details of diagnosed deadlocks. You can also view the overview and details of recent deadlock logs.

DAS provides the following deadlock log details:

-   Session ID
-   Request type
-   Transaction ID
-   Table involved
-   Lock pending
-   Name of the index pending the lock
-   Type of the lock pending
-   Lock being held
-   Name of the index holding the lock
-   Type of the lock being held
-   Transactional SQL

For more information about how to manage locks and how to view and analyze deadlocks on your database instance by using DAS, see [Deadlock analysis]().

**Note:** The lock analysis feature is supported only for ApsaraDB RDS for MySQL and PolarDB for MySQL.

