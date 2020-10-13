# Query the endpoint of the dedicated proxy

Queries the endpoint of the dedicated proxy for an ApsaraDB for RDS instance.

The Dedicated Proxy feature of ApsaraDB for RDS offers functions such as read/write splitting and short-lived connection optimization. For more information, see [Dedicated proxy](~~138705~~).

Before you call this operation, make sure that the instance runs one of the following MySQL versions and RDS editions:

-   MySQL 8.0 with a minor engine version of 20191204 or later in the RDS Enterprise Edition
-   MySQL 8.0 with a minor engine version of 20190915 or later in the RDS High-availability Edition
-   MySQL 5.7 with a minor engine version of 20191128 or later in the RDS Enterprise Edition
-   MySQL 5.7 with a minor engine version of 20190925 or later in the RDS High-availability Edition
-   MySQL 5.6 with a minor engine version of 20200229 or later in the RDS High-availability Edition

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeDBProxyEndpoint&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBProxyEndpoint|The operation that you want to perform. Set the value to **DescribeDBProxyEndpoint**. |
|DBInstanceId|String|Yes|rm-t4n3axxxxx|The ID of the instance. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|DBProxyEndpointId|String|No|ta9um4xxxxx|The ID of the endpoint. |
|DBProxyConnectString|String|No|ta9umxxxxx.rwlb.singapore.rds.aliyuncs.com|The endpoint of the dedicated proxy. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBProxyConnectString|String|ta9umxxxxx.rwlb.singapore.rds.aliyuncs.com|The endpoint of the dedicated proxy. |
|DBProxyConnectStringNetType|String|InnerString|The network type of the proxy endpoint. Valid values:

-   **InnerString:** indicates an internal endpoint.
-   **OuterString:** indicates a public endpoint. |
|DBProxyConnectStringPort|String|3306|The port of the endpoint. |
|DBProxyEndpointId|String|ta9um4xxxxx|The ID of the endpoint. |
|DBProxyFeatures|String|ReadWriteSpliting:1;ConnectionPersist:0;|An array that consists of functions enabled on the endpoint of the dedicated proxy. The functions are separated with semicolons \(;\) in the following format: `Function 1:Status;Function 2:Status;...`

Valid function values:

-   **ReadWriteSpliting:** the read/write splitting function.
-   **ConnectionPersist:** the short-lived connection optimization function.

Valid status values:

-   **1:** enables the function.
-   **0:** disables the function. |
|ReadOnlyInstanceDistributionType|String|Standard|The method used to assign read weights. For more information, see [Modify the read weights](~~96076~~). Valid values:

-   **Standard:** The system automatically assigns a read weight to each instance based on the instance specifications.
-   **Custom:** You must manually assign read weights. |
|ReadOnlyInstanceMaxDelayTime|String|30|The latency threshold for read/write splitting. If the latency between the primary instance and its read-only instance exceeds this threshold, the system no longer sends read requests to that read-only instance. Unit: seconds. |
|ReadOnlyInstanceWeight|String|\{"rm-uf6wjk5xxxx":"500","rr-tfhfgk5xxx":"200"...\}|The read weights assigned to the primary instance and its read-only instances. Read weights increase in increments of 100, and the maximum read weight is 10000. Format: `{"Instance ID 1":"Read weight","Instance ID 2":"Read weight"...}`.

**Note:** This parameter must be specified when the **ReadOnlyInstanceDistributionType** parameter is set to **Custom**. |
|RequestId|String|847BA085-B377-4BFA-8267-F82345ECE1D2|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeDBProxyEndpoint
&DBInstanceId=rm-t4n3axxxxx
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDBProxyEndpointResponse>
  <DBProxyEndpointId>ta9umxxxxx</DBProxyEndpointId>
      <ReadOnlyInstanceWeight>""</ReadOnlyInstanceWeight>
      <ReadOnlyInstanceMaxDelayTime>30</ReadOnlyInstanceMaxDelayTime>
      <DBProxyConnectString>ta9umxxxxx.rwlb.singapore.rds.aliyuncs.com</DBProxyConnectString>
      <DBProxyConnectStringNetType>InnerString</DBProxyConnectStringNetType>
      <RequestId>847BA085-B377-4BFA-8267-F82345ECE1D2</RequestId>
      <DBProxyFeatures>ReadWriteSpliting:0;ConnectionPersist:0</DBProxyFeatures>
      <DBProxyConnectStringPort>3306</DBProxyConnectStringPort>
      <ReadOnlyInstanceDistributionType>Standard</ReadOnlyInstanceDistributionType>
</DescribeDBProxyEndpointResponse>
```

`JSON` format

```
{
    "DBProxyEndpointId": "ta9umxxxxx",
    "ReadOnlyInstanceWeight": "\"\"",
    "ReadOnlyInstanceMaxDelayTime": "30",
    "DBProxyConnectString": "ta9umxxxxx.rwlb.singapore.rds.aliyuncs.com",
    "DBProxyConnectStringNetType": "InnerString",
    "RequestId": "847BA085-B377-4BFA-8267-F82345ECE1D2",
    "DBProxyFeatures": "ReadWriteSpliting:0;ConnectionPersist:0",
    "DBProxyConnectStringPort": "3306",
    "ReadOnlyInstanceDistributionType": "Standard"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

