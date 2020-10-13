# Modify a parameter template

Modifies a parameter template of an ApsaraDB for RDS instance.

You can configure a number of parameters at a time by using a parameter template and apply the parameter template to an RDS instance. For more information, see [Use a parameter template to manage parameters](~~130565~~).

**Note:** Parameter templates are supported only for RDS instances that run MySQL.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyParameterGroup&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyParameterGroup|The operation that you want to perform. Set the value to **ModifyParameterGroup**. |
|ParameterGroupId|String|Yes|rpg-xxxxxxx|The ID of the parameter template. You can call the [DescribeParameterGroups](~~144491~~) operation to query the most recent parameter templates. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list.

 **Note:** The region of a parameter template cannot be changed. You can call the [CloneParameterGroup](~~144581~~) operation to replicate a parameter template to a specific region. |
|ParameterGroupName|String|No|testgroup1|The name of the parameter template.

 -   The name must start with a letter and can contain letters, digits, dots \(.\), and underscores \(\_\).
-   The name must be 8 to 64 characters in length.

 **Note:** If you do not specify this parameter, the original name of the parameter template is retained. |
|ParameterGroupDesc|String|No|test|The new description of the parameter template. The description can be up to 200 characters in length.

 **Note:** If you do not specify this parameter, the original description of the parameter template is retained. |
|Parameters|String|No|\{"back\_log":"3000"\}|A JSON string that consists of parameters and their values in the parameter template. Format: \{"Parameter 1":"Value of Parameter 1","Parameter 2":"Value of Parameter 2 ",...\}. For information about configurable parameters, see [Reconfigure parameters for an RDS for MySQL instance](~~96063~~).

 **Note:**

-   If you specify this parameter, the new parameters replace the original ones.
-   If you do not specify this parameter, the original parameters remain unchanged. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|857DC00B-7B85-4853-8B27-AD65EB618BC6|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=ModifyParameterGroup
&RegionId=cn-hangzhou
&ParameterGroupId=rpg-xxxxxxx
&Parameters={"back_log":"3000"}
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyParameterGroupResponse>
  <RequestId>857DC00B-7B85-4853-8B27-AD65EB618BC6</RequestId>
</ModifyParameterGroupResponse>
```

`JSON` format

```
{
	"RequestId": "857DC00B-7B85-4853-8B27-AD65EB618BC6"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

