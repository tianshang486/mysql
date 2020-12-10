# Read/write splitting

ApsaraDB RDS provides the read/write splitting feature. This feature uses a proxy endpoint to route read and write requests.

If the primary RDS instance needs to process a large number of read requests but only a small number of write requests, it may become overwhelmed. This may even interrupt your workloads. In this case, you can create one or more read-only RDS instances to offload read requests from the primary RDS instance. This allows you to scale the read capability of your database system. For more information, see [Overview of ApsaraDB RDS for MySQL read-only instances](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md).

After you create read-only RDS instances, you can enable the read/write splitting feature. In this case, the endpoint that is generated to connect to the dedicated proxies of your database system is used to implement read/write splitting. After you add this endpoint to your application, write requests are routed to the primary RDS instance and read requests are routed to the read-only RDS instances.

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


## Usage notes

For more information, see [Read/write splitting](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Read/write splitting.md).

