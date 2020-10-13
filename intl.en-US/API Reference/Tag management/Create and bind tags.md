# Create and bind tags

Creates and binds tags to one or more ApsaraDB for RDS instances.

If you have a large number of instances, you can create multiple tags and bind these tags to the instances. Then, you can filter the instances by tag.

-   A tag consists of a key and a value. Each key must be unique in a region for an Alibaba Cloud account. Different keys can be mapped to the same value.
-   If a specified tag does not exist, the tag is created and bound to the specified instances.
-   If the key of the specified tag is the same as that of an existing tag, the specified tag overwrites the existing tag.
-   You can bind up to 20 tags to an instance.
-   You can bind tags to up to 50 instances in each call.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=TagResources&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|TagResources|The operation that you want to perform. Set the value to **TagResources**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|ResourceId.N|RepeatList|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. You can bind tags to N instances at a time. Valid values of N: **1** to **50**. |
|ResourceType|String|Yes|INSTANCE|The type of the resource. Set the value to **INSTANCE**. |
|Tag.N.Key|String|Yes|testkey1|The key of the tag. You can create N keys at a time. Valid values of N: **1** to **20**. The tag key cannot be left empty. |
|Tag.N.Value|String|No|testvalue1|The value of the tag. You can create N values at a time. Valid values of N: **1** to **20**. The tag value can be left empty. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|224DB9F7-3100-4899-AB9C-C938BCCB43E7|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=TagResources
&RegionId=cn-hangzhou
&ResourceType=INSTANCE
&ResourceId.1=rm-uf6wjk5xxxxxxx
&Tag.1.Key=testkey1
&Tag.1.Value=testvalue1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<TagResourcesResponse>
  <RequestId>224DB9F7-3100-4899-AB9C-C938BCCB43E7</RequestId>
</TagResourcesResponse>
```

`JSON` format

```
{
	"RequestId":"224DB9F7-3100-4899-AB9C-C938BCCB43E7"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

