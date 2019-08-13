# DescribeRegions {#doc_api_1063468 .reference}

You can call this operation to view the regions and zones.

Before you create an instance by calling the [CreateDBInstance](intl.en-US/API Reference/Instance management/CreateDBInstance.md#) API operation, you can call this operation to view the regions and zones.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeRegions) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRegions| The operation that you want to perform. Set this parameter to DescribeRegions.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Regions|N/A|N/A| The list of available regions and zones.

 |
|RegionId|String|cn-hangzhou| The ID of the region.

 |
|ZoneId|String|cn-hangzhou-b| The ID of the zone.

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

https://rds.aliyuncs.com/?Action=DescribeRegions
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_7zv_mwc_pgd}
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

``` {#codeblock_bd8_vdr_o69}
{
	"RequestId":"A36D9720-7902-42A4-B8B9-014A2135E6C3",
	"Regions":{
		"RDSRegion":[
			{
				"RegionId":"cn-hangzhou",
				"ZoneId":"cn-hangzhou-b"
			},
			{
				"RegionId":"cn-qingdao",
				"ZoneId":"cn-qingdao-b"
			},
			{
				"RegionId":"cn-shenzhen",
				"ZoneId":"cn-shenzhen-a"
			}
		]
	}
}
```

## Error codes {#section_2xe_2of_vx6 .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

