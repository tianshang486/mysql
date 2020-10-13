# Modify settings of a dedicated proxy

Modifies dedicated proxy settings of an ApsaraDB for RDS instance.

The Dedicated Proxy feature of ApsaraDB for RDS offers functions such as read/write splitting and short-lived connection optimization. For more information, see [Dedicated proxy](~~138705~~).

Before you call this operation, make sure that the following requirements are met:

-   The Dedicated Proxy feature must be enabled for the instance.
-   The instance must run one of the following MySQL versions and RDS editions:
    -   MySQL 8.0 with a minor engine version of 20191204 or later in the Enterprise Edition
    -   MySQL 8.0 with a minor engine version of 20190915 or later in the High-availability Edition
    -   MySQL 5.7 with a minor engine version of 20191128 or later in the Enterprise Edition
    -   MySQL 5.7 with a minor engine version of 20190925 or later in the High-availability Edition
    -   MySQL 5.6 with a minor engine version of 20200229 or later in the High-availability Edition

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyDBProxyInstance&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBProxyInstance|The operation that you want to perform. Set the value to **ModifyDBProxyInstance**. |
|DBInstanceId|String|Yes|rm-t4n3axxxxx|The ID of the instance. |
|DBProxyInstanceNum|String|Yes|2|The number of proxy instances. Value 0 specifies to disable the Dedicated Proxy feature for the instance. Valid values: **0** to **60**.

 **Note:** The capability to process requests increases in proportion with the number of proxy instances. You can specify a proper number of proxy instances based on the monitoring information of database loads. |
|DBProxyInstanceType|String|Yes|DedicatedProxy|The type of the proxy. Only the Dedicated Proxy feature is supported. Set the value to **DedicatedProxy**. |
|EffectiveTime|String|No|MaintainTime|The time you want the new settings to take effect. Valid values:

 -   **Immediate:** The settings immediately take effect.
-   **MaintainTime:** The new settings take effect during the maintenance window. For more information, see [ModifyDBInstanceMaintainTime](~~26249~~).
-   **SpecificTime:** The new settings take effect at the specified point in time.

 Default value: **MaintainTime**. |
|EffectiveSpecificTime|String|No|2019-07-10T13:15:12Z|The point in time when the new settings take effect. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

 **Note:** This parameter must be specified when the **EffectiveTime** parameter is set to **SpecificTime**. |
|RegionId|String|No|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|65C55572-530E-4A53-BE03-1D08CAF0F046|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyDBProxyInstance
&DBInstanceId=rm-t4n3axxxxx
&DBProxyInstanceType=DedicatedProxy
&DBProxyInstanceNum=2
&EffectiveTime=Immediate
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBProxyInstanceResponse>
    <RequestId>65C55572-530E-4A53-BE03-1D08CAF0F046</RequestId>
</ModifyDBProxyInstanceResponse>
```

`JSON` format

```
{
	"RequestId": "65C55572-530E-4A53-BE03-1D08CAF0F046"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

