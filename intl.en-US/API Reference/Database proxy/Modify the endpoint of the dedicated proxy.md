# Modify the endpoint of the dedicated proxy

Modifies the endpoint of the dedicated proxy for an ApsaraDB for RDS instance.

The Dedicated Proxy feature of ApsaraDB for RDS offers functions such as read/write splitting and short-lived connection optimization. For more information, see [Dedicated proxy](~~138705~~).

Before you call this operation, make sure that the following requirements are met:

-   The Dedicated Proxy feature must be enabled for the instance.
-   The instance must run one of the following MySQL versions and RDS editions:
    -   MySQL 8.0 with a minor engine version of 20191204 or later in the RDS Enterprise Edition
    -   MySQL 8.0 with a minor engine version of 20190915 or later in the RDS High-availability Edition
    -   MySQL 5.7 with a minor engine version of 20191128 or later in the RDS Enterprise Edition
    -   MySQL 5.7 with a minor engine version of 20190925 or later in the RDS High-availability Edition
    -   MySQL 5.6 with a minor engine version of 20200229 or later in the RDS High-availability Edition

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyDBProxyEndpoint&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBProxyEndpoint|The operation that you want to perform. Set the value to **ModifyDBProxyEndpoint**. |
|DBInstanceId|String|Yes|rm-t4n3axxxxx|The ID of the instance. |
|DBProxyEndpointId|String|Yes|ta9um4xxxxx|The ID of the proxy endpoint. You can call the [DescribeDBProxyEndpoint](~~140955~~) operation to query the ID of a proxy endpoint. |
|ConfigDBProxyFeatures|String|No|ReadWriteSpliting:1;ConnectionPersist:0;|The function that you want to enable on the proxy endpoint. If you specify more than one function, separate them with semicolons \(;\). Format: `Function 1:Status;Function 2:Status;...`

Valid function values:

-   **ReadWriteSpliting:** the read/write splitting function.
-   **ConnectionPersist:** the short-lived connection optimization function.
-   **TransactionReadSqlRouteOptimizeStatus:** the transaction splitting function.

Valid status values:

-   **1:** enables the function.
-   **0:** disables the function. |
|RegionId|String|No|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|ReadOnlyInstanceMaxDelayTime|String|No|30|The latency threshold for read/write splitting. If the latency on a read-only instance exceeds this threshold, ApsaraDB for RDS no longer distributes read requests to that instance. If you do not specify this parameter, the original value is retained. Unit: seconds. Valid values: **30** to **3600**. Default value: **30**.

**Note:** You must specify this parameter when the read/write splitting function is enabled. |
|ReadOnlyInstanceDistributionType|String|No|Standard|The method used to assign read weights. For more information, see [Modify the read weights](~~96076~~). Valid values:

-   **Standard**: The system automatically assigns a read weight to each instance based on the instance specifications.
-   **Custom:** You must manually assign read weights.

**Note:** You must specify this parameter when the read/write splitting function is enabled. |
|ReadOnlyInstanceWeight|String|No|\{"rm-uf6wjk5xxxx":"500","rr-tfhfgk5xxx":"200"...\}|The read weights assigned to the primary instance and its read-only instances. Read weights increase in increments of 100, and the maximum read weight is 10000. Format: `{"Instance ID 1":"Read weight","Instance ID 2":"Read weight"...}`.

**Note:** This parameter must be specified when the **ReadOnlyInstanceDistributionType** parameter is set to **Custom**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|6B50D92C-1960-4D4F-A290-AFADD6B1A5C8|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyDBProxyEndpoint
&DBInstanceId=rm-uf6wjk5xxxxxxx
&DBProxyEndpointId=ta9um4xxxxx
&ConfigDBProxyFeatures=ReadWriteSpliting:1;ConnectionPersist:1;
&ReadOnlyInstanceMaxDelayTime=30
&ReadOnlyInstanceDistributionType=Standard
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBProxyEndpointResponse>
    <RequestId>6B50D92C-1960-4D4F-A290-AFADD6B1A5C8</RequestId>
</ModifyDBProxyEndpointResponse>
```

`JSON` format

```
{
    "RequestId": "6B50D92C-1960-4D4F-A290-AFADD6B1A5C8"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

