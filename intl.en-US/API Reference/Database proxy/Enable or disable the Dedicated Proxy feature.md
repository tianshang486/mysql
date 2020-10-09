# Enable or disable the Dedicated Proxy feature

Enables or disables the Dedicated Proxy feature of an ApsaraDB for RDS instance.

The Dedicated Proxy feature of ApsaraDB for RDS offers functions such as read/write splitting and short-lived connection optimization. For more information, see [Dedicated proxy](~~138705~~).

Before you call this operation, make sure that the instance runs one of the following MySQL versions and RDS editions:

-   MySQL 8.0 with a minor engine version of 20191204 or later on RDS Enterprise Edition
-   MySQL 8.0 with a minor engine version of 20190915 or later on RDS High-availability Edition
-   MySQL 5.7 with a minor engine version of 20191128 or later on RDS Enterprise Edition
-   MySQL 5.7 with a minor engine version of 20190925 or later on RDS High-availability Edition
-   MySQL 5.6 with a minor engine version of 20200229 or later on RDS High-availability Edition

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyDBProxy&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBProxy|The operation that you want to perform. Set the value to **ModifyDBProxy**. |
|ConfigDBProxyService|String|Yes|Startup|Specifies whether to enable or disable the Dedicated Proxy feature. Valid values:

 -   **Startup:** enables the Dedicated Proxy feature.
-   **Shutdown:** disables the Dedicated Proxy feature. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|DBProxyInstanceNum|String|No|1|The number of proxy instances you want to create for the instance. Valid values: **1** to **60**. Default value: **1**.

 **Note:** The capability to process requests increases in proportion with the number of proxy instances. You can specify a proper number of proxy instances based on the database loads obtained from monitoring data. |
|RegionId|String|No|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|InstanceNetworkType|String|No|VPC|The network type of the instance. Only the VPC network type is supported. Set the value to **VPC**. |
|VPCId|String|No|vpc-xxxxxxxxxxxx|The ID of the VPC to which the instance belongs. |
|VSwitchId|String|No|CloudInstanceId|The ID of the VSwitch associated with the specified VPC. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|FC452BB1-EED8-4278-95C7-0324B3710DF1|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyDBProxy
&DBInstanceId=rm-uf6wjk5xxxxxxx
&ConfigDBProxyService=Startup
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBProxyResponse>
    <RequestId>FC452BB1-EED8-4278-95C7-0324B3710DF1</RequestId>
</ModifyDBProxyResponse>
```

`JSON` format

```
{
	"RequestId": "FC452BB1-EED8-4278-95C7-0324B3710DF1"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

