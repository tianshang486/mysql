# Copy a parameter template

Copies a parameter template to the current region or another region.

You can configure a number of parameters at a time by using a parameter template and then apply the parameter template to an ApsaraDB for RDS instance. For more information, see [Use a parameter template to manage parameters](~~130565~~).

**Note:** Parameter templates are supported only for RDS instances that run MySQL.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=CloneParameterGroup&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CloneParameterGroup|The operation that you want to perform. Set the value to **CloneParameterGroup**. |
|ParameterGroupDesc|String|Yes|CloneGroup1|The description of the parameter template in the destination region. |
|ParameterGroupId|String|Yes|rpg-xxxxxxx|The ID of the source parameter template. You can call the [DescribeParameterGroups](~~144491~~) operation to query the most recent parameter templates in a region. |
|ParameterGroupName|String|Yes|tartestgroup|The name of the parameter template in the destination region. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the source parameter template. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|TargetRegionId|String|Yes|cn-qingdao|The ID of the destination region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1D3D5995-6BDD-43B5-93B8-2C41A2ACD6AA|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=CloneParameterGroup
&RegionId=cn-hangzhou
&ParameterGroupId=rpg-xxxxxxx
&TargetRegionId=cn-qingdao
&ParameterGroupName=tartestgroup
&ParameterGroupDesc=CloneGroup1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CloneParameterGroupResponse>
  <RequestId>1D3D5995-6BDD-43B5-93B8-2C41A2ACD6AA</RequestId>
</CloneParameterGroupResponse>
```

`JSON` format

```
{
    "RequestId": "1D3D5995-6BDD-43B5-93B8-2C41A2ACD6AA"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

