# Read/write splitting

This topic introduces the read/write splitting feature of ApsaraDB RDS for MySQL in the dedicated proxy feature. This topic also describes how to enable this feature.

-   The RDS instance is a primary instance. It cannot be a read-only or disaster recovery instance.
-   The dedicated proxy feature is enabled for the RDS instance. For more information, see [Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md).
-   The RDS instance is attached with read-only instances. For more information, see [Create a read-only ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Read-only instances/Create a read-only ApsaraDB RDS for MySQL instance.md).

If the primary RDS instance needs to process a large number of read requests but only a small number of write requests, it may become overwhelmed. This may even interrupt your workloads. In this case, you can create one or more read-only RDS instances to offload read requests from the primary RDS instance. This allows you to scale the read capability of your database system. For more information, see [Overview of ApsaraDB RDS for MySQL read-only instances](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md).

After you create read-only RDS instances, you can enable the read/write splitting feature. In this case, the endpoint that is generated to connect to the dedicated proxies of your database system is used to implement read/write splitting. After you add this endpoint to your application, write requests are routed to the primary RDS instance and read requests are routed to the read-only RDS instances.

## Differences between the read/write splitting endpoint and the internal and public endpoints

After you enable the read/write splitting feature and add the generated proxy endpoint to your application, all requests are routed to this endpoint. Then, the requests are routed from this endpoint to the primary and read-only RDS instances based on the request types and the read weights of these instances.

If the internal or public endpoint of the primary RDS instance is added to your application, all requests are routed to the primary RDS instance. To implement read/write splitting, you must add the endpoints and read weights of the primary and read-only RDS instances to your application.

## Logic to route requests

-   The following requests are routed only to the primary RDS instance:
    -   Requests for data manipulation language \(DML\) statements, which are INSERT, UPDATE, DELETE, and SELECT FOR UPDATE
    -   Requests for all data definition language \(DDL\) statements that are used to perform operations such as creating databases or tables, deleting databases or tables, and changing schemas or permissions
    -   All requests that are encapsulated in transactions
    -   Requests for user-defined functions
    -   Requests for stored procedures
    -   Requests for EXECUTE statements
    -   Requests for [multi-statements](https://dev.mysql.com/doc/internals/en/multi-statement.html)
    -   Requests that involve temporary tables
    -   Requests for SELECT last\_insert\_id\(\) statements
    -   All the requests to query or modify user variables
    -   Requests for SHOW PROCESSLIST statements
    -   All requests for KILL statements in SQL \(Note: These statements are not KILL commands in Linux.\)
-   The following requests are routed to the primary RDS instance or its read-only RDS instances:
    -   Read requests that are not encapsulated in transactions
    -   Requests for COM\_STMT\_EXECUTE statements
-   The following requests are routed to all the primary and read-only RDS instances:
    -   All requests to modify system variables
    -   Requests for USE statements
    -   Requests for COM\_STMT\_PREPARE statements
    -   Requests for COM\_CHANGE\_USER, COM\_QUIT, and COM\_SET\_OPTION statements

## Benefits

-   Easier maintenance by using a unified endpoint

    If you do not enable the read/write splitting feature, you must add the endpoints of the primary and read-only RDS instances to your application. After you add the endpoints, your database system can route write requests to the primary RDS instance and read requests to the read-only RDS instances.

    If you enable the read/write splitting feature, the generated proxy endpoint is used to implement read/write splitting. After your application is connected to this endpoint, your database system routes read and write requests to the primary and read-only RDS instances based on the read weights of these instances. This reduces maintenance costs.

    In addition, you can scale up the read capability of your database system by creating read-only RDS instances. This way, you do not need to modify the configuration data on your application.

-   Higher performance and lower maintenance cost by using a native RDS link

    If you build a proxy layer on the cloud, data must be parsed and forwarded by a number of components before the data reaches your database system. This increases the response latency. The read/write splitting feature that is provided by ApsaraDB RDS shortens the response latency, increases the processing speed, and reduces the maintenance costs.

-   Ideal in various use scenarios based on configurable read weights and thresholds

    You can specify the read weights of the primary and read-only RDS instances. You can also specify a latency threshold for data replication to the read-only RDS instances.

-   Highly available with instance-level health checks

    The read/write splitting feature actively performs health checks on the primary and read-only RDS instances. If a read-only RDS instance unexpectedly exits or its latency exceeds the specified threshold, your database system stops routing read requests to the instance and redirects the requests that were destined for the instance to other healthy instances. Instance-level health checks allow you to ensure service availability in the event of faults on a single read-only RDS instance. After the faulty read-only RDS instance is recovered, your database system resumes routing read requests to the recovered read-only RDS instance.

    **Note:** We recommend that you create at least two read-only RDS instances to avoid single points of failure \(SPOFs\).


## Precautions

-   When you change the specifications of your RDS instance or its read-only RDS instances, a transient connection error may occur.
-   After you create a read-only RDS instance, only the requests over new connections can be routed to the new instance.
-   The proxy endpoint does not support SSL encryption.
-   The proxy endpoint does not support compression.
-   If the proxy endpoint is used for connection, all the requests that are encapsulated in transactions are routed to the primary RDS instance.
-   If the proxy endpoint is used for read/write splitting, the read consistency of the requests that are not encapsulated in transactions cannot be ensured. If you require read consistency, you can encapsulate the requests in transactions.
-   If the proxy endpoint is used for connection, the `SHOW PROCESSLIST` statement combines the results from the primary RDS instance and all the read-only RDS instances that are attached to the primary RDS instance. Then, the statement returns a result set.
-   If the short-lived connection optimization feature is enabled, the `SHOW PROCESSLIST` statement may return idle connections.
-   If you execute [multi-statements](https://dev.mysql.com/doc/internals/en/multi-statement.html) or stored procedures, the read/write splitting feature is disabled and all the subsequent requests over the current connection are routed to the primary RDS instance. To enable the read/write splitting feature again, you must close the current connection and establish a new connection.
-   The dedicated proxy feature supports the `/*FORCE_MASTER*/` and `/*FORCE_SLAVE*/` hints. However, requests that contain hints have the highest route priorities. Therefore, these requests are not constrained by consistency or transaction limits. Before you use these hints, you must check whether these hints are suitable for your workloads. In addition, the hints cannot contain statements such as `/*FORCE_SLAVE*/ set names utf8;`. These statements can change environment variables. If you include these statements in the hints, errors may occur in your subsequent workloads.

## Enable the read/write splitting feature

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Database Proxy**.

5.  On the **Read/Write Splitting** tab, click **Enable now**.

6.  Configure the following parameters.

    ![Configure read weights](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9040359951/p95288.png)

    |Parameter|Description|
    |---------|-----------|
    |**Latency Threshold**|The maximum latency that is allowed for data replication from the primary RDS instance to the read-only RDS instances that are attached to the primary RDS instance. This applies regardless of the read weight that is specified for the read-only instance. If the read-only RDS instance has a high read-weight, your database system stops routing read requests to the read-only RDS instance. Valid values: 0 to 7200. Unit: seconds. A read-only RDS instance may replicate data at a latency due to SQL statement execution limits. We recommend that you set this parameter to a value that is greater than or equal to 30. |
    |**Read Weight Distribution**|The read weight of each RDS instance in your database system. A higher read weight indicates more read requests to process. For example, the primary RDS instance is attached with three read-only RDS instances, and the read weights of these instances are 0, 100, 200, and 200. In this case, the primary RDS instance processes only write requests, and the three read-only RDS instances process all the read requests at the 1:2:2 ratio.     -   **Automatic Distribution**: Your database system assigns a read weight to each RDS instance based on the specifications of the RDS instance. After you create a read-only RDS instance, your database system assigns a read weight to the read-only RDS instance and adds the instance to the read/write splitting link. For more information, see [Rules of weight allocation by the system](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/Rules of weight allocation by the system.md).
    -   **Customized Distribution**: You must manually specify a read weight for each RDS instance. Valid values: 0 to 10000. When you create a read-only RDS instance, the read weight of the instance is 0. You must manually specify a new read weight for the instance.
**Note:** If you specify a replication latency for a read-only RDS instance, you cannot specify a read weight for the instance. For more information, see [Set a replication delay for an RDS MySQL read-only instance](/intl.en-US/RDS MySQL Database/Read-only instances/Set a replication delay for an RDS MySQL read-only instance.md). |

7.  Click **OK**.


After the read/write splitting feature is enabled, you must add the proxy endpoint to your application. After you add the proxy endpoint, your database system can route write requests to the primary RDS instance and read requests to the read-only RDS instances.

![Endpoint for read/write splitting](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9040359951/p113257.png)

## FAQ

-   If the primary RDS instance processes only a small number of write requests, can the read requests be sent to the primary RDS instance?

    Yes, if the primary RDS instance processes only a small number of write requests, the read requests can be sent to the primary RDS instance.

-   Does the read/write splitting feature support hint-nested statements?

    Yes, the read/write splitting feature supports hint-nested statements. You can use such statements to forcibly route requests to the primary RDS instance. For more information about the hint formats that are supported by ApsaraDB RDS, see [Rules of weight allocation by the system](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/Rules of weight allocation by the system.md).


## References

[FAQ on read/write splitting](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/FAQ on read/write splitting.md)

