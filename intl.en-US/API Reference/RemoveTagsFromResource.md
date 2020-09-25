# RemoveTagsFromResource

You can call this operation to unbind tags.

This operation must meet the following requirements:

-   A maximum of 10 tags can be unbound in a single request.
-   If a tag is unbound from all of the instances to which the tag has been bound, the tag is automatically deleted.
-   If you only specify TagKeys when you unbind tags, all tags which match the TagKey condition are unbound.
-   You must specify at least one set of tags or a single TagKey.

## Debugging

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=RemoveTagsFromResource) to perform debugging. API Explorer allows you to perform various API operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|RemoveTagsFromResource|The operation that you want to perform. Set the value to **RemoveTagsFromResource**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|RegionId|String|Yes|cn-hangzhou|The region ID. The maximum length of the region ID is 50 characters. You can call the [DescribeRegions](~~26243~~) operation to view IDs of the available regions. |
|AccessKeyId|String|No|LTAIfCxxxxxxx|The AccessKey ID issued by Alibaba Cloud for users to access services. |
|Tag. 1.key|String|No|key1|The TagKeys of the first set of tags to be unbound. Each tag includes a TagKey and a TagValue. Up to five key-value pairs can be entered in a single request. The TagKey is required, and the TagValue is optional. |
|Tag. 1.value|String|No|value1|The TagValues of the first set of tags to be unbound. Each tag includes a TagKey and a TagValue. Up to five key-value pairs can be entered in a single request. The TagKey is required, and the TagValue is optional. |
|Tag. 2.key|String|No|key2|The TagKeys of the second set of tags to be unbound. Each tag includes a TagKey and a TagValue. Up to five key-value pairs can be entered in a single request. The TagKey is required, and the TagValue is optional. |
|Tag. 2.value|String|No|value2|The TagValues of the second set of tags to be unbound. Each tag includes a TagKey and a TagValue. Up to five key-value pairs can be entered in a single request. The TagKey is required, and the TagValue is optional. |
|Tag. 3.key|String|No|key3|The TagKeys of the third set of tags to be unbound. Each tag includes a TagKey and a TagValue. Up to five key-value pairs can be entered in a single request. The TagKey is required, and TagValue is optional. |
|Tag. 3.value|String|No|value4|The TagValues of the third set of tags to be unbound. Each tag includes a TagKey and a TagValue. Up to five key-value pairs can be entered in a single request. The TagKey is required, and TagValue is optional. |
|Tag. 4.key|String|No|key4|The TagKeys of the fourth set of tags to be unbound. Each tag includes a TagKey and a TagValue. Up to five key-value pairs can be entered in a single request. The TagKey is required, and TagValue is optional. |
|Tag. 4.value|String|No|value4|The TagValues of the fourth set of tags to be unbound. Each tag includes a TagKey and a TagValue. Up to five key-value pairs can be entered in a single request. The TagKey is required, and TagValue is optional. |
|Tag. 5.key|String|No|key5|The TagKeys of the fifth set of tags to be unbound. Each tag includes a TagKey and a TagValue. Up to five key-value pairs can be entered in a single request. The TagKey is required, and the TagValue is optional. |
|Tag. 5.value|String|No|value5|The TagValues of the fifth set of tags to be unbound. Each tag includes a TagKey and a TagValue. Up to five key-value pairs can be entered in a single request. The TagKey is required, and the TagValue is optional. |
|Tags|String|No|\{"key1":"value1"\}|A set of tags to be bound. Each tag has a TagKey and a TagValue. Format: \{"key1":"value1"\}.

 **Note:** The TagKey is required, and the TagValue is optional. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|AE00ACCD-1CF9-4920-9BB9-0175EFF43405|The ID of the request. |

## Examples

Sample requests

```

http(s)://rds.aliyuncs.com/? Action=RemoveTagsFromResource
&DBInstanceId=rm-uf6wjk5xxxxxxx 
&RegionId=cn-hangzhou
&Tag. 1.key=test
&<Common request parameters>

```

Successful response examples

`XML` format

```
<RemoveTagsFromResourceResponse> 
  <requestId>AE00ACCD-1CF9-4920-9BB9-0175EFF43405</requestId> 
</RemoveTagsFromResourceResponse> 

```

`JSON` format

```
{
	"requestId":"AE00ACCD-1CF9-4920-9BB9-0175EFF43405"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds?spm=5176.10421674.0.0.17f7ebed4WFmrN).

