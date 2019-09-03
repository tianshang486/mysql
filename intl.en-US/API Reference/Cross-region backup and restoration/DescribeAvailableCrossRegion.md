# DescribeAvailableCrossRegion {#doc_api_Rds_DescribeAvailableCrossRegion .reference}

Queries the available destination regions for an RDS instance.

## Debug {#api_explorer .section}

Use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeAvailableCrossRegion&type=RPC&version=2014-08-15) to perform debug operations and generate SDK code examples.

## Request parameters {#parameters .section}

|ID|Type|Required|Example value|Description|
|--|----|--------|-------------|-----------|
|Action|String|Yes|DescribeAvailableCrossRegion| The name of this API action. Value: **DescribeAvailableCrossRegion**.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the RDS instance belongs. You can call the [DescribeRegions](~~26243~~) API action to obtain this region ID.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|ID|Type|Example value|Description|
|--|----|-------------|-----------|
|Regions| |"cn-qingdao","cn-shanghai", "cn-shenzhen"| The list of destination regions available to the RDS instance.

 |
|RequestId|String|39265F46-EC77-4036-8AC4-F035F32F6BE2| The ID of the request.

 |

## Examples {#demo .section}

Request example:

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeAvailableCrossRegion
&RegionId=cn-hangzhou
&<Common request parameters>

```

Response example:

`XML` format:

``` {#xml_return_success_demo}
<DescribeAvailableCrossRegionResponse>
  <RequestId>39265F46-EC77-4036-8AC4-F035F32F6BE2</RequestId>
	  <Regions>
		    <Region>cn-qingdao</Region>
		    <Region>cn-shanghai</Region>
		    <Region>cn-shenzhen</Region>
	  </Regions>
    </DescribeAvailableCrossRegionResponse>
```

`JSON` format:

``` {#json_return_success_demo}
{
	"RequestId":"39265F46-EC77-4036-8AC4-F035F32F6BE2",
	"Regions":{
		"Region":[
			"cn-qingdao",
			"cn-shanghai",
			"cn-shenzhen"
		]
	}
}
```

## Errors {#section_aqq_rs7_3g0 .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

