# Query available regions and zones

You can call the DescribeRegions operation to query the regions and zones that are available.

You can call this operation before you call the [CreateDBInstance](~~26228~~) operation.

**Note:** If the returned region supports the multi-zone deployment method, the value of the ZoneId parameter contains an MAZ part. Examples: cn-hangzhou-MAZ6\(b,f\) and cn-hangzhou-MAZ5\(b,e,f\).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeRegions&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRegions|The operation that you want to perform. Set the value to **DescribeRegions**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Regions|Array| |An array that consists of available regions and zones. |
|RDSRegion| | | |
|RegionId|String|cn-hangzhou|The ID of the region. |
|ZoneId|String|cn-hangzhou-b|The ID of the zone. |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|The ID of the request. |

## Examples

Sample requests

```
https://rds.aliyuncs.com/?Action=DescribeRegions
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeRegionsResponse>
	  <Regions>
		    <RDSRegion>
			      <RegionId>cn-hangzhou</RegionId>
			      <ZoneId>cn-hangzhou-b</ZoneId>
		    </RDSRegion>
		    <RDSRegion>
			      <RegionId>cn-qingdao</RegionId>
			      <ZoneId>cn-qingdao-b</ZoneId>
		    </RDSRegion>
		    <RDSRegion>
			      <RegionId>cn-shenzhen</RegionId>
			      <ZoneId>cn-shenzhen-a</ZoneId>
		    </RDSRegion>
	  </Regions>
	  <RequestId>A36D9720-7902-42A4-B8B9-014A2135E6C3</RequestId></DescribeRegionsResponse>
```

`JSON` format

```
{
  "Regions": {
    "RDSRegion": [
      {"RegionId": "cn-hangzhou","ZoneId":"cn-hangzhou-b"},
      { "RegionId": "cn-qingdao","ZoneId":"cn-qingdao-b"}, 
      {"RegionId": "cn-shenzhen","ZoneId": "cn-shenzhen-a"}
    ]
}, 
  "RequestId": "A36D9720-7902-42A4-B8B9-014A2135E6C3"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

