# Query regions that support cross-region backup

Queries destination regions that support cross-region backup.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeAvailableCrossRegion&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAvailableCrossRegion|The operation that you want to perform. Set the value to**DescribeAvailableCrossRegion**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the source region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Regions|List|"cn-qingdao","cn-shanghai", "cn-shenzhen"|The list of destination regions that support cross-region backup. |
|RequestId|String|39265F46-EC77-4036-8AC4-F035F32F6BE2|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeAvailableCrossRegion
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeAvailableCrossRegionResponse>
  <RequestId>39265F46-EC77-4036-8AC4-F035F32F6BE2</RequestId>
	  <Regions>
		    <Region>cn-qingdao</Region>
		    <Region>cn-shanghai</Region>
		    <Region>cn-shenzhen</Region>
	  </Regions>
</DescribeAvailableCrossRegionResponse>
```

`JSON` format

```
{
	"RequestId": "39265F46-EC77-4036-8AC4-F035F32F6BE2",
	"Regions": {
		"Region": [
			"cn-qingdao",
			"cn-shanghai",
			"cn-shenzhen"
		]
	}
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

