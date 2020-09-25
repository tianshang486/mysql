# DescribeTags

You can call this operation to query the tags of RDS instances.

This operation must meet the following requirements:

-   If an instance ID is specified, all tags bound to this instance can be queried, and the other filtering conditions are invalid.
-   If you only specify TagKeys, the results for tags which match the TagKey condition are returned. If you specify both TagKeys and TagValues, the results for tags which match both conditions are returned.

## Debugging

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeTags) to perform debugging. API Explorer allows you to perform various API operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|DescribeTags|The operation that you want to perform. Set the value to**DescribeTags**. |
|RegionId|String|Yes|cn-hangzhou|The region ID. The maximum length of the region ID is 50 characters. You can call the [DescribeRegions](~~26243~~) operation to view IDs of the available regions. |
|DBInstanceId|String|No|rm-uf6wjk5xxxxxxx|The ID of the instance.

 **Note:** If you specify this parameter, the other filtering conditions are invalid. |
|Tags|String|No|\{“key1”:”value1”\}|The tags to be queried. Each tag includes a TagKey and a TagValue. Format: \{“key1”:”value1”\}. |
|AccessKeyId|String|No|LTAIfCxxxxxxx|The AccessKey ID issued by Alibaba Cloud for users to access services. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Items|N/A|None|The array that consists of tag data. |
|└TagKey|String|key1|The tag key. |
|└TagValue|String|value1|The tag value. |
|└DBInstanceIds|N/A|rm-uf6wjk5xxxxxxx|The IDs of instances to which the tag has been bound. |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|The ID of the request. |

## Examples

Sample requests

```

http(s)://rds.aliyuncs.com/? Action=DescribeTags
&RegionId=cn-hangzhou 
&<Common request parameters>

```

Successful response examples

`XML` format

```
<DescribeTagsResponse>
  <Items> 
    <TagInfos> 
      <TagValue>1</TagValue> 
      <TagKey>Test</TagKey>
      <DBInstanceIds> 
        <DBInstanceIds>rm-uf6wjk5xxxxxxx</DBInstanceIds> 
      </DBInstanceIds> 
    </TagInfos>
  </Items> 
  <RequestId>6D709088-6D7D-4152-99F4-C2FE86463862</RequestId> 
</DescribeTagsResponse> 

```

`JSON` format

```
{
	"Items":{
		"TagInfos":[
			{
				"TagValue":"1",
				"TagKey":"test",
				"DBInstanceIds":{
					"DBInstanceIds":[
						"rm-uf6wjk5xxxxxxx"
					]
				}
			}
		]
	},
	"RequestId":"6D709088-6D7D-4152-99F4-C2FE86463862"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|Tag.NoRegionIdExist|the region Id can not be blank.|The error message returned when the instance ID is null while you renew an instance and change the configuration of an instance.|
|400|Tag.NoTagInfoExist|all the tags and tagN parameters is null.|The error message returned when the tag parameter is invalid.|
|400|Tag.TagKeyCanNotBeAll|tag key can not be all.|The error message returned when the TagKey is invalid.|
|400|Tag.TagKeyDuplex|tag key must be sole in one operation.|The error message returned when the TagKey is not unique.|
|400|Tag.NoDBInstanceIdExist|the dbinstance Id can not be blank.|The error message returned when the instance ID is null when you renew an instance and change the configuration of an instance.|
|400|Tag.TooManyDBInstanceIds|the dbinstance Ids is more than 30.|The error message returned when the number of instance IDs exceeds 30.|
|400|Tag.TooManyTagsForOneInstance|total 10 tags can be added to one resource.|The error message returned when the number of tags bound to one resource exceeds 10.|
|400|Tag.SetTagInfoAtTwoParamters|only tags or tagN parameter could be setted.|The error message returned when the settings of your tag parameter are canceled.|
|400|Tag.Allow5TagInfos|only 5 tags allowed in one operation.|The error message returned when more than five tags are used in a single operation.|
|400|Tag.TagKeyIsBlank|tag key can not be blank.|The error message returned when the TagKey is null.|
|400|Tag.TagKeyStartWith.aliyun|tag key and value can not be started with aliyun.|The error message returned when the TagKeyStartWith is invalid.|
|400|Tag.TagKeyTooLong|the max tag key's length is 64.|The error message returned when the TagKey contains more than 64 characters.|
|400|Tag.TagValueTooLong|the max tag value's length is 128.|The error message returned when the TagValue contains more than 128 characters.|
|400|Tag.InvalidTagsParamter|tags paramter is invalid.|The error message returned when the tag parameter is invalid.|
|404|InvalidDBInstanceId.NotFound|The DBInstanceId provided does not exist in our records.|The error message returned when the instance ID does not exist. Confirm that the instance ID has been deleted from the current account.|
|400|Tag.Malformed|The specified parameter Type is not valid.|The error message returned when the TagKey is invalid.|
|400|Tag.Malformed|The specified parameter Type is not valid.|The error message returned when the TagValue is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds?spm=5176.10421674.0.0.17f7ebed4WFmrN).

