# Delete a parameter template

Deletes a parameter template of an ApsaraDB for RDS instance.

You can configure a number of parameters at a time by using a parameter template and then apply the parameter template to an RDS instance. For more information, see [Use a parameter template to manage parameters](~~130565~~).

**Note:** Deleting a parameter template does not affect the instance on which the parameter template has been applied.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DeleteParameterGroup&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteParameterGroup|The operation that you want to perform. Set the value to **DeleteParameterGroup**. |
|ParameterGroupId|String|Yes|rpg-xxxxxxx|The ID of the parameter template. You can call the [DescribeParameterGroups](~~144491~~) operation to query the most recent parameter templates. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|8AF26036-B254-4212-B8E4-EFBE818B7FD6|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DeleteParameterGroup
&RegionId=cn-hangzhou
&ParameterGroupId=rpg-xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteParameterGroupResponse>
  <RequestId>8AF26036-B254-4212-B8E4-EFBE818B7FD6</RequestId>
</DeleteParameterGroupResponse>
```

`JSON` format

```
{
	"RequestId": "8AF26036-B254-4212-B8E4-EFBE818B7FD6"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

