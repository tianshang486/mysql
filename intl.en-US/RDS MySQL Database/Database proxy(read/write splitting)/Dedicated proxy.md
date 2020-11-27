# Dedicated proxy

This topic describes the dedicated proxy feature of ApsaraDB RDS for MySQL. This feature provides advanced features, such as read/write splitting, connection pool, and transaction splitting. You can enable this feature on your primary RDS instance.

-   Your RDS instance runs one of the following MySQL versions and RDS editions:

    -   MySQL 8.0 with a minor engine version of 20191204 or later on RDS Enterprise Edition
    -   MySQL 8.0 with a minor engine version of 20190915 or later on RDS High-availability Edition
    -   MySQL 5.7 with a minor engine version of 20191128 or later on RDS Enterprise Edition
    -   MySQL 5.7 with a minor engine version of 20190925 or later on RDS High-availability Edition
    -   MySQL 5.6 with a minor engine version of 20200229 or later on RDS High-availability Edition
    **Note:** You can log on to the ApsaraDB RDS console and go to the Basic Information page of your RDS instance. In the **Configuration Information** section of the page, you can check whether the **Upgrade Minor Version** button exists. If the button exists, you can click it to view and update the minor engine version. If the button does not exist, you are using the latest minor engine version. For more information, see [Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance.md).

    ![Upgrade Minor Version](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6040359951/p61646.png)

-   Your RDS instance does not reside in Zone D of the China \(Hangzhou\) region, Zone A of the China \(Beijing\) region, or Finance Zone B of the China \(Shenzhen\) region.

    **Note:** If your RDS instance resides in the preceding zones, you can migrate it to other zones before you enable the dedicated proxy feature. For more information, see [Migrate an ApsaraDB RDS for MySQL instance across zones in the same region](/intl.en-US/RDS MySQL Database/Instance Change/Migrate an ApsaraDB RDS for MySQL instance across zones in the same region.md).


The dedicated proxy feature uses dedicated computing resources. This feature has the following benefits:

-   A unified proxy endpoint is provided to connect to all of the dedicated proxies that are enabled on your RDS instance. This reduces maintenance costs by relieving the need to update the endpoints on your application. The proxy endpoint remains valid unless you release the dedicated proxy instance. For example, you may enable read/write splitting during peak hours, but then release read-only instances and disable read/write splitting after peak hours. In these cases, you do not need to update the endpoints on your application because the proxy endpoint is still connected.
-   Dedicated proxies exclusively serve your RDS instance and its read-only RDS instances. You do not need to compete with other users for resources. This ensures service stability.
-   Dedicated proxies support scaling. You can enable additional dedicated proxies based on your business requirements. This allows you to process more queries.

## Billing

From January 15, 2020 to August 31, 2020, you are provided with one free dedicated proxy. Additional dedicated proxies are charged to your account.

Since September 1, 2020, all dedicated proxies are charged to your account. These dedicated proxies provide more powerful processing capabilities. In normal cases, each dedicated proxy can process up to 20,000 queries per second \(QPS\).

**Note:** The discounts for the upgrade from shared proxy to dedicated proxy remain unchanged. For more information, see [Upgrade an ApsaraDB RDS for MySQL instance from shared proxy to dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Upgrade an ApsaraDB RDS for MySQL instance from shared proxy to dedicated proxy.md).

Dedicated proxies support only the pay-as-you-go billing method. The following table lists the prices of dedicated proxies in different Alibaba Cloud regions.

|Region|Dedicated proxy|
|Name|Code|USD/hour/proxy|
|------|---------------|
|----|----|--------------|
|China \(Hangzhou\)|cn-hangzhou|0.173|
|China \(Shanghai\)|cn-shanghai|0.173|
|China \(Qingdao\)|cn-qingdao|0.173|
|China \(Beijing\)|cn-beijing|0.173|
|China \(Zhangjiakou\)|cn-zhangjiakou|0.120|
|China \(Hohhot\)|cn-huhehaote|0.173|
|China \(Shenzhen\)|cn-shenzhen|0.173|
|China \(Heyuan\)|cn-heyuan|0.173|
|China \(Chengdu\)|cn-chengdu|0.173|
|China \(Hong Kong\)|cn-hongkong|0.297|
|Japan \(Tokyo\)|ap-northeast-1|0.288|
|India \(Mumbai\)|ap-south-1|0.231|
|Singapore \(Singapore\)|ap-southeast-1|0.271|
|Australia \(Sydney\)|ap-southeast-2|0.273|
|Malaysia \(Kuala Lumpur\)|ap-southeast-3|0.253|
|Indonesia \(Jakarta\)|ap-southeast-5|0.271|
|Germany \(Frankfurt\)|eu-central-1|0.243|
|UK \(London\)|eu-west-1|0.280|
|UAE \(Dubai\)|me-east-1|0.377|
|US \(Virginia\)|us-east-1|0.237|
|US \(Silicon Valley\)|us-west-1|0.284|

## Limits

-   Dedicated proxies do not support Secure Sockets Layer \(SSL\) encryption.
-   Dedicated proxies do not support compression protocols.
-   Dedicated proxies do not support vSwitch changes.

## Precautions

-   When you change the specifications of your RDS instance or its read-only RDS instances, a transient connection error may occur.
-   If you connect your application to the proxy endpoint, all of the requests that are encapsulated in transactions are routed to your RDS instance. This applies if you do not enable the transaction splitting feature.
-   If you use the proxy endpoint to implement read/write splitting, the read consistency of the requests that are not encapsulated in transactions cannot be guaranteed. If you require this read consistency, you must encapsulate these requests in transactions.
-   If you connect your application to the proxy endpoint, a `SHOW PROCESSLIST` statement is invoked to return a result set for each query. This result set consists of the query results from your RDS instance and its read-only RDS instances.
-   If you execute multi-statements or run stored procedures, the read/write splitting feature is disabled and all subsequent requests over the current connection are routed to your RDS instance. To enable the read/write splitting feature again, you must close the current connection and establish a new connection. For more information about multi-statements, see [Multi-Statement](https://dev.mysql.com/doc/internals/en/multi-statement.html).
-   The dedicated proxy feature supports the `/*FORCE_MASTER*/` and `/*FORCE_SLAVE*/` hints. However, requests that contain hints have the highest route priorities, and therefore these requests are not constrained by consistency or transaction limits. Before you use these hints, you must check whether these hints are suitable for your workloads. In addition, these hints cannot contain statements such as `/*FORCE_SLAVE*/ set names utf8;`. These statements can change environment variables. If you include these statements in these hints, errors may occur when you process subsequent workloads.

    **Note:** If you use the MySQL command line tool to establish a connection and execute these hints, you must add `-c` to the statements. Otherwise, the MySQL command line tool filters these hints.

-   After you enable the dedicated proxy feature, each connection is replicated to your RDS instance and its read-only RDS instances in compliance with the 1:N connection model. We recommend that you specify the same connection specifications for these instances. If these instances have different connection specifications, the number of connections allowed is subject to the lowest connection specifications among these instances.
-   If you create or restart a read-only RDS instance after you enable the dedicated proxy feature, only the requests over a new connection are routed to the new or restarted read-only RDS instance.
-   The **max\_prepared\_stmt\_count** parameter must be set to the same value for your RDS instance and its read-only RDS instances.

## Enable the dedicated proxy feature

This section describes how to enable the dedicated proxy feature in the ApsaraDB RDS console. You can also enable this feature when you create a read-only RDS instance. For more information, see [Create a read-only ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Read-only instances/Create a read-only ApsaraDB RDS for MySQL instance.md).

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Database Proxy**.

5.  Click **Enable now**.

    ![Enable the dedicated proxy feature](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6040359951/p60623.png)

6.  Configure the **Network Type** and **Proxy Instances** parameters. Then, click **Enable**.

    **Note:**

    -   The default network type varies based on the instance configuration. For more information, see [Create a proxy endpoint for a dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Create a proxy endpoint for a dedicated proxy.md).
    -   We recommend that you specify the number of dedicated proxies as the rounded-up integer of the total number of CPU cores of your RDS instance and its read-only RDS instances divided by 8. A maximum of 60 dedicated proxies are supported.

        For example, if your RDS instance has 8 CPU cores and its read-only RDS instances have 4 CPU cores, the recommended number of dedicated proxies is 2 based on the following formula: \(8 + 4\)/8 = 1.5 \(rounded up to 2\).

    ![Enable the database proxy feature](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4272364061/p99416.png)


## Overview of the Database Proxy page

After the dedicated proxy feature is enabled, you can use the generated proxy endpoint to implement features such as read/write splitting, connection pool, and transaction splitting.

![Database Proxy page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6040359951/p60624.png)

|Section|Parameter|Description|
|-------|---------|-----------|
|**Proxy Endpoint**|**Instance ID**|The ID of the dedicated proxy instance.|
|**Enabled Proxies**|The number of dedicated proxies that are enabled on your RDS instance. You can enable additional dedicated proxies. This allows you to process more queries.|
|**Read/Write Splitting**|Specifies whether to enable the read/write splitting feature for the proxy endpoint. For more information, see [Read/write splitting](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Read/write splitting.md).|
|**Connection Pool**|Specifies whether to enable the connection pool feature for the proxy endpoint. If you want to enable the connection pool feature, this parameter also specifies the type of connection pool to enable. Valid values: -   Enable Transaction Connection Pool: This is the default value. If tens of thousands of connections are established, select this value.
-   Enable Session Connection Pool: If only PHP short-lived connections are established, select this value.
-   Disable: If you want to disable the connection pool feature, select this value.

For more information, see [Connection pool](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Connection pool.md). |
|**Transaction Splitting**|Specifies whether to enable the transaction splitting feature for the proxy endpoint. For more information, see [Transaction splitting](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Transaction splitting.md). **Note:** You can click **Enable** or **Disable** to the right of the Transaction Splitting parameter to enable or disable this feature. |
|**Endpoint**|The proxy endpoint that is generated after the dedicated proxy feature is enabled. This endpoint connects to all of the dedicated proxies that are enabled on your RDS instance. The read/write splitting feature is also bound to this endpoint. You can also create, modify, or delete additional proxy endpoints. For more information, see [Create a proxy endpoint for a dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Create a proxy endpoint for a dedicated proxy.md).|
|**Port**|The port that is associated with the proxy endpoint. **Note:** To change the port, you can click **Change Port** to the right of the displayed port number. Valid values: 1000 to 5999. |
|**Endpoint Type**|The network type of the proxy endpoint. You cannot change the network type.|
|**Proxy**|**Proxy Type**|The type of proxy that is enabled on your RDS instance. Only the **Dedicated Proxy** type is supported.|
|**CPU and Memory**|The specifications that are provided per dedicated proxy. Only two CPU cores and four GB of memory are supported.|
|**Enabled Proxies**|The number of dedicated proxies that are enabled on your RDS instance. A maximum of 60 dedicated proxies are supported. **Note:** We recommend that you specify the number of dedicated proxies as the rounded-up integer of the total number of CPU cores of your RDS instance and its read-only RDS instances divided by 8.

For example, if your RDS instance has 8 CPU cores and its read-only RDS instances have 4 CPU cores, the recommended number of dedicated proxies is 2 based on the following formula: \(8 + 4\)/8 = 1.5 \(rounded up to 2\). |

## Adjust the number of dedicated proxies

**Note:** When you adjust the number of dedicated proxies, a transient connection error will occur. Make sure that your application is configured to automatically reconnect to your database system.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Database Proxy**.

5.  In the Proxy section of the Proxy Service tab, change the number in the **Adjusted Proxies** column and click **Apply** in the Adjustment Plan column.

    ![Adjust the number of dedicated proxies](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6040359951/p60627.png)

6.  Set **Applied At** and click **OK**.

    ![Configure Proxy Resources](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6040359951/p60629.png)


## View the monitoring data of dedicated proxies

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Database Proxy**.

5.  Click the **Monitoring Data** tab.

6.  Select a time range and view the **CPU Utilization \(%\)** metric for the selected time range.

    **Note:** The CPU Utilization \(%\) metric indicates the CPU utilization that is contributed by the dedicated proxies.

    ![View the monitoring data of dedicated proxies](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7040359951/p60641.png)


## Update the minor engine version of the dedicated proxy instance

**Note:** If you update the minor engine version of the dedicated proxy instance, the dedicated proxy instance will restart. The restart causes a transient connection error of about 30 seconds. The time when the dedicated proxy instance will restart depends on the **Upgrade Time** that you specify. You can select **Upgrade Immediate** or **Upgrade within maintenance period**. We recommend that you update the minor engine version of the dedicated proxy instance during off-peak hours. Otherwise, make sure that your application is configured to automatically reconnect to your database system.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Database Proxy**.

5.  In the Proxy Endpoint section of the Proxy Service tab, click **Upgrade Dedicated Proxy Version**.

    ![Upgrade Dedicated Proxy Version](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7040359951/p128450.png)

6.  Specify **Upgrade Time** and click **OK**.


## Disable the dedicated proxy feature

**Note:** If read/write splitting is enabled, when you disable the dedicated proxy feature, read/write splitting is disabled as well.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Database Proxy**.

5.  In the upper-right corner of the Proxy Service tab, click **Disable Proxy Service**.

    ![Disable Proxy Service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7040359951/p60650.png)

6.  In the message that appears, click **OK**.


## FAQ

-   After I update my RDS instance that runs MySQL 5.7 to the latest minor engine version, why is the dedicated proxy feature still unavailable?

    Before you can use the dedicated proxy feature, you must disable the original read/write splitting feature. This applies after you update your RDS instance that runs MySQL 5.7 to the latest minor engine version.

-   After I enable the dedicated proxy feature, do I need to use the proxy endpoint or the read/write splitting endpoint to implement read/write splitting?

    After you enable the dedicated proxy feature, the proxy endpoint and the read/write splitting endpoint are the same. The backend uses the proxy endpoint to implement read/write splitting.


## Related operations

|Operation|Description|
|---------|-----------|
|[ModifyDBProxy](/intl.en-US/API Reference/Database proxy/Enable or disable the Dedicated Proxy feature.md)|Enables or disables the dedicated proxy feature on an ApsaraDB RDS instance.|
|[ModifyDBProxyInstance](/intl.en-US/API Reference/Database proxy/Modify settings of a dedicated proxy.md)|Modifies the settings of the dedicated proxy feature on an ApsaraDB RDS instance.|
|[DescribeDBProxy](/intl.en-US/API Reference/Database proxy/Query dedicated proxy details.md)|Queries details about the dedicated proxies that are enabled on an ApsaraDB RDS instance.|
|[DescribeDBProxyEndpoint](/intl.en-US/API Reference/Database proxy/Query the endpoint of the dedicated proxy.md)|Queries information about the proxy endpoint of an ApsaraDB RDS instance.|
|[ModifyDBProxyEndpoint](/intl.en-US/API Reference/Database proxy/Modify the endpoint of the dedicated proxy.md)|Modifies information about the proxy endpoint of an ApsaraDB RDS instance.|
|[DescribeDBProxyPerformance](/intl.en-US/API Reference/Database proxy/Query performance metrics of a dedicated proxy.md)|Queries the performance of the dedicated proxies that are enabled on an ApsaraDB RDS instance.|
|[CreateDBProxyEndpointAddress](/intl.en-US/API Reference/Database proxy/Create proxy endpoint.md)|Creates an endpoint that is used to connect to the dedicated proxies of an ApsaraDB RDS instance.|
|[ModifyDBProxyEndpointAddress](/intl.en-US/API Reference/Database proxy/Modify proxy endpoint.md)|Modifies the endpoint that is used to connect to the dedicated proxies of an ApsaraDB RDS instance.|
|[DeleteDBProxyEndpointAddress](/intl.en-US/API Reference/Database proxy/Delete proxy endpoint.md)|Deletes the endpoint that is used to connect to the dedicated proxies of an ApsaraDB RDS instance.|

