# Manage sessions

Alibaba Cloud Database Autonomy Service \(DAS\) allows you to view and manage sessions on your database instance. For example, you can analyze SQL statements within a 10-second time window, export active sessions, optimize sessions, terminate sessions, and collect session statistics.

## View sessions

You can view the overview and details of the sessions on your database instance. For more information about how to view the sessions on an ApsaraDB RDS for MySQL instance, see [View the session statistics of an ApsaraDB RDS for MySQL instance]().

## Manage sessions

-   **Analyze SQL statements within a 10-second time window**.

    DAS executes the **SHOW PROCESSLIST** statement at 1-second intervals within a 10-second time window. Then, DAS analyzes all the returned result sets. Based on the analysis results, you can identify the most executed SQL statements and slowest SQL statements within the 10-second time window. DAS also allows you to view and analyze the following information:

    -   All SQL statements
    -   Slow SQL statements
    -   Overview of SQL statements
    **Note:** For more information, see [t1915607.md\#](), [Analyze slow query logs](), and [t1915616.md\#]().

-   **Export active sessions**.
-   **Terminate sessions**.
-   **Optimize sessions**.

    **Note:** This feature is not supported for ApsaraDB RDS instances that run the Basic Edition. If your ApsaraDB RDS instance runs the Basic Edition, you can upgrade the instance to the High-availability Edition.

-   **Collect session statistics**.

