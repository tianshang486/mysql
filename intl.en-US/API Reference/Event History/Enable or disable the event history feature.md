# Enable or disable the event history feature

Enables or disables the event history feature of an ApsaraDB for RDS instance.

The event history feature enables you to view historical events that occurred in a region over a specific time range. These events include instance creation and parameter reconfiguration. For more information, see [Event history](~~129759~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyActionEventPolicy&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyActionEventPolicy|The operation that you want to perform. Set the value to **ModifyActionEventPolicy**. |
|EnableEventLog|String|Yes|True|Specifies whether to enable the event history feature. Valid values: **True \| False**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region for which you want to enable the event history feature. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|EnableEventLog|String|True|Indicates whether the event history feature is enabled. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|RequestId|String|BAC0952C-0EB3-4DE7-A567-B83269BFE43F|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyActionEventPolicy
&Region=cn-hangzhou
&EnableEventLog=True
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyActionEventPolicyResponse>
   <RequestId>BAC0952C-0EB3-4DE7-A567-B83269BFE43F</RequestId>
   <RegionId>cn-hangzhou</RegionId>
   <EnableEventLog>True</EnableEventLog>
</ModifyActionEventPolicyResponse>
```

`JSON` format

```
{
    "RequestId": "BAC0952C-0EB3-4DE7-A567-B83269BFE43F",
    "RegionId": "cn-hangzhou",
    "EnableEventLog": "True"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

