# Query parameter templates

Queries parameter templates that are available in a region.

You can configure a number of parameters at a time by using a parameter template and then apply the parameter template to an ApsaraDB for RDS instance. For more information, see [Use a parameter template to manage parameters](~~130565~~).

**Note:** Parameter templates are supported only for RDS instances that run MySQL.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeParameterGroups&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeParameterGroups|The operation that you want to perform. Set this parameter to **DescribeParameterGroups**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ParameterGroups|Array| |The list of parameter templates. |
|ParameterGroup| | | |
|CreateTime|String|2019-11-21T01:48:39Z|The time when the parameter template was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Engine|String|mysql|The database engine. |
|EngineVersion|String|5.7|The version of the database engine. |
|ForceRestart|Integer|1|Indicates whether applying the parameter template requires the instance to be restarted. Valid values:

-   **0:** A restart is not required.
-   **1**: A restart is required. |
|ParamCounts|Integer|2|The number of parameters in the parameter template. |
|ParameterGroupDesc|String|testgroup|The description of the parameter template. |
|ParameterGroupId|String|rpg-xxxxxxx|The ID of the parameter template. |
|ParameterGroupName|String|test1234|The name of the parameter template. |
|ParameterGroupType|Integer|1|The type of the parameter template. Valid values:

-   **0:** indicates a default parameter template.
-   **1:** indicates a custom parameter template.
-   **2**: an automatic backup parameter template. After you apply this type of template to an RDS instance, the system automatically backs up the parameter settings of that instance and saves the data backup as a template. |
|UpdateTime|String|2019-11-21T02:21:35Z|The time when the parameter template was last updated. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|RequestId|String|D4A23265-C5B6-42E1-98A0-EFA1EB42E723|The ID of the request. |
|SignalForOptimizeParams|Boolean|false|Indicates whether no parameter templates exist in the region. Valid values:

-   true
-   false |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeParameterGroups
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeParameterGroupsResponse>
  <RequestId>D4A23265-C5B6-42E1-98A0-EFA1EB42E723</RequestId>
  <ParameterGroups>
        <ParameterGroup>
              <ParameterGroupType>1</ParameterGroupType>
              <ParameterGroupName>testgroup123</ParameterGroupName>
              <CreateTime>2019-11-21T01:48:39Z</CreateTime>
              <ParameterGroupDesc></ParameterGroupDesc>
              <ParamCounts>2</ParamCounts>
              <UpdateTime>2019-11-21T01:48:39Z</UpdateTime>
              <ForceRestart>1</ForceRestart>
              <EngineVersion>5.7</EngineVersion>
              <Engine>mysql</Engine>
              <ParameterGroupId>rpg-xxxxxxx</ParameterGroupId>
        </ParameterGroup>
        <ParameterGroup>
              <ParameterGroupType>1</ParameterGroupType>
              <ParameterGroupName>test1234</ParameterGroupName>
              <CreateTime>2019-11-21T01:42:38Z</CreateTime>
              <ParameterGroupDesc></ParameterGroupDesc>
              <ParamCounts>2</ParamCounts>
              <UpdateTime>2019-11-21T01:42:38Z</UpdateTime>
              <ForceRestart>1</ForceRestart>
              <EngineVersion>5.7</EngineVersion>
              <Engine>mysql</Engine>
              <ParameterGroupId>rpg-xxxxxxx</ParameterGroupId>
        </ParameterGroup>
  </ParameterGroups>
</DescribeParameterGroupsResponse>
```

`JSON` format

```
{
    "RequestId": "D4A23265-C5B6-42E1-98A0-EFA1EB42E723",
    "ParameterGroups": {
        "ParameterGroup": [
            {
                "ParameterGroupType": 1,
                "ParameterGroupName": "testgroup123",
                "CreateTime": "2019-11-21T01:48:39Z",
                "ParameterGroupDesc": "",
                "ParamCounts": 2,
                "UpdateTime": "2019-11-21T01:48:39Z",
                "ForceRestart": 1,
                "EngineVersion": "5.7",
                "Engine": "mysql",
                "ParameterGroupId": "rpg-xxxxxxx"
            },
            {
                "ParameterGroupType": 1,
                "ParameterGroupName": "test1234",
                "CreateTime": "2019-11-21T01:42:38Z",
                "ParameterGroupDesc": "",
                "ParamCounts": 2,
                "UpdateTime": "2019-11-21T01:42:38Z",
                "ForceRestart": 1,
                "EngineVersion": "5.7",
                "Engine": "mysql",
                "ParameterGroupId": "rpg-xxxxxxx"
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

