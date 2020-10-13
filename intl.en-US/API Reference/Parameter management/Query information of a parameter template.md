# Query information of a parameter template

Queries information of a parameter template.

You can configure a number of parameters at a time by using a parameter template and then apply the parameter template to an RDS instance. For more information, see [Use a parameter template to manage parameters](~~130565~~).

**Note:** Parameter templates are supported only for RDS instances that run MySQL.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeParameterGroup&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeParameterGroup|The operation that you want to perform. Set the value to **DescribeParameterGroup**. |
|ParameterGroupId|String|Yes|rpg-dpxxxxxxx|The ID of the parameter template. You can call the [DescribeParameterGroups](~~144491~~) operation to query the most recent parameter templates in a region. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ParamGroup|Array| |The information of the parameter template. |
|ParameterGroup| | | |
|CreateTime|String|2019-10-22T06:02:53Z|The time when the parameter template was created. |
|Engine|String|mysql|The database engine. |
|EngineVersion|String|5.6|The version of the database engine. |
|ForceRestart|Integer|1|Indicates whether applying the parameter template requires the RDS instance to be restarted. Valid values:

 -   **0:** A restart is not required.
-   **1**: A restart is required. |
|ParamCounts|Integer|2|The number of parameters in the parameter template. |
|ParamDetail|Array| |The list of parameters in the parameter template. |
|ParameterDetail| | | |
|ParamName|String|back\_log|The name of a parameter. |
|ParamValue|String|2000|The value of a parameter. |
|ParameterGroupDesc|String|testGroup1|The description of the parameter template. |
|ParameterGroupId|String|rpg-dpxxxxxxx|The ID of the parameter template. |
|ParameterGroupName|String|test123456|The name of the parameter template. |
|ParameterGroupType|Integer|1|The type of the parameter template. Valid values:

 -   **0:** indicates a default parameter template.
-   **1:** indicates a custom parameter template.
-   **2**: indicates an automatic backup parameter template. After you apply this type of template to an RDS instance, the system automatically backs up the parameter settings of this instance and saves the backup as a template. |
|UpdateTime|String|2019-10-22T06:07:54Z|The time when the parameter template was last updated. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|RequestId|String|498AE8CA-8C81-4A01-AF37-2B902014ED30|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeParameterGroup
&RegionId=cn-hangzhou
&ParameterGroupId=rpg-xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeParameterGroupResponse>
  <RequestId>498AE8CA-8C81-4A01-AF37-2B902014ED30</RequestId>
  <ParamGroup>
        <ParameterGroup>
              <ParameterGroupType>1</ParameterGroupType>
              <ParameterGroupName>test123456</ParameterGroupName>
              <CreateTime>2019-10-22T06:02:53Z</CreateTime>
              <ParameterGroupDesc></ParameterGroupDesc>
              <ParamCounts>1</ParamCounts>
              <UpdateTime>2019-10-22T06:07:54Z</UpdateTime>
              <ForceRestart>1</ForceRestart>
              <EngineVersion>5.6</EngineVersion>
              <Engine>mysql</Engine>
              <ParamDetail>
                    <ParameterDetail>
                          <ParamName>back_log</ParamName>
                          <ParamValue>2000</ParamValue>
                    </ParameterDetail>
              </ParamDetail>
              <ParameterGroupId>rpg-xxxxxxx</ParameterGroupId>
        </ParameterGroup>
  </ParamGroup>
</DescribeParameterGroupResponse>
```

`JSON` format

```
{
	"RequestId": "498AE8CA-8C81-4A01-AF37-2B902014ED30",
	"ParamGroup": {
		"ParameterGroup": [
			{
				"ParameterGroupType": 1,
				"ParameterGroupName": "test123456",
				"CreateTime": "2019-10-22T06:02:53Z",
				"ParameterGroupDesc": "",
				"ParamCounts": 1,
				"UpdateTime": "2019-10-22T06:07:54Z",
				"ForceRestart": 1,
				"EngineVersion": "5.6",
				"Engine": "mysql",
				"ParamDetail": {
					"ParameterDetail": [
						{
							"ParamName": "back_log",
							"ParamValue": "2000"
						}
					]
				},
				"ParameterGroupId": "rpg-xxxxxxx"
			}
		]
	}
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

