# Connection pool

ApsaraDB RDS provides connection pools for dedicated proxies. You can select a connection pool type based on your business requirements. This reduces high loads that are caused by excessive connections or frequent short-lived connections \(for example, when PHP is used\) on your RDS instance.

The dedicated proxy feature is enabled for your RDS instance. For more information, see [Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md).

The dedicated proxy feature supports the following two types of connection pools:

-   **Transaction Connection Pool**

    This is the default connection pool type. If tens of thousands of connections are established, we recommend that you select this type of connection pool.

    A transaction connection pool reduces the number of connections and the loads that are caused by frequent short-lived connections. Your database client can establish a large number of connections to the dedicated proxy that is enabled on your RDS instance. However, the dedicated proxy establishes only a small number of connections to your RDS instance. When your database client sends a request to your RDS instance, the dedicated proxy selects a qualified connection from the transaction connection pool and sends information about the connection to your RDS instance. The connection must match the specified system variables. After the specified transaction is complete, the dedicated proxy releases the connection back to the transaction connection pool.

    For more information about the limits on **Transaction Connection Pool**, see [Limits on transaction connection pool](#section_ug0_uuu_77j).

-   **Session Connection Pool**

    If short-lived connections are used, we recommend that you select this type of connection pool.

    A session connection pool reduces the loads that are caused by frequent short-lived connections on your RDS instance. When your database client is disconnected, the dedicated proxy that is enabled on your RDS instance checks whether the current connection is idle. If the connection is idle, the dedicated proxy retains the connection in the session connection pool for a short period of time. When your database client initiates a request to establish a connection again, the dedicated proxy matches the request with the idle connections that are retained in the session connection pool. The matching is implemented based on the values of the user, clientip, and dbname fields in the request. If the dedicated proxy finds an idle connection that matches the request, it uses the matched idle connection. If the dedicated proxy does not find an idle connection that matches the request, it establishes a new connection. This reduces the overheads from connection establishment.

    **Note:** A session connection pool does not reduce concurrent connections to your RDS instance. It decreases the frequency to establish connections between your application and RDS instance. This reduces the overheads from the primary MySQL thread and improves the efficiency to process business requests. However, idle connections in the session connection pool still consume the quota for threads that are allowed on your RDS instance for a short period of time.


## Precautions

-   You cannot configure different permissions for the same account with different source IP addresses. If you configure different permissions for the same account with different source IP addresses, errors may occur when connections are reused. For example, the account has permissions on database\_a when it logs on from the 192.168.1.1 IP address. However, the account does not have permissions on database\_a when it logs on from the 192.168.1.2 IP address. In this case, permission errors may occur if you enable the connection pool function.
-   The connection pool function is provided by the dedicated proxy feature on your RDS instance. It does not affect the connection pool feature of your database client. If your database client provides a connection pool, you do not need to enable the connection pool function on your RDS instance.

## Limits on transaction connection pool

-   When the following operations are performed over a connection, the dedicated proxy that is enabled on your RDS instance locks the connection. The dedicated proxy does not release the connection to the connection pool until the operations are complete.
    -   Execute the PREPARE statement.
    -   Create a temporary table.
    -   Modify user variables.
    -   Process large packets. For example, if the size of a packet exceeds 16 MB, the packet is large.
    -   Execute the LOCK TABLE statement.
    -   Run a multi-statement query.
    -   Invoke a stored procedure.
-   The FOUND\_ROWS, ROW\_COUNT, and LAST\_INSERT\_ID functions are not supported. These functions can be called but may return inaccurate results.
-   When your database client is connected to the dedicated proxy that is enabled on your RDS instance, the dedicated proxy selects a connection from the connection pool. If the connection has the wait\_timeout parameter configured, your RDS instance closes the connection with the dedicated proxy after the time specified by the wait\_timeout parameter elapses. However, your database client may remain connected to the dedicated proxy.
-   The connection pool matches requests with connections based on the following four variables: `sql_mode`, `character_set_server`, `collation_server`, and `time_zone`. If a request includes other session-level system variables, after the requested connection is established, you must explicitly execute the SET statement to configure these variables. Otherwise, the connection pool may reuse the connection whose system variables are changed.
-   You can use the `SELECT CONNECTION_ID()` statement to query the thread ID of the current connection to determine whether the connection is reused.
-   The IP address and port that are returned by the `SHOW PROCESSLIST` statement may differ from the actual IP address and port of your database client. This is because connections may be reused.
-   The dedicated proxy merges the results that the `SHOW PROCESSLIST` statement obtains from all of the RDS instances in your database system. Then, the dedicated proxy returns a result set to your database client. After you enable the transaction connection pool function, the thread ID of the connection between your database client and the dedicated proxy differs from the thread ID of the connection between the dedicated proxy and your RDS instance. In this case, when you kill a process, the kill command may return an error message even if it is successfully executed. You can execute the `SHOW PROCESSLIST` statement again to check whether the process is killed.

## Change the connection pool type

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Database Proxy**.

5.  Select a connection pool type from the drop-down list to the right of **Connection Pool**.

    **Note:** The connection pool change is applied only to new connections.

    ![Connection Pool](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0140359951/p71549.png)


