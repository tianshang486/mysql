# DescribeRegions {#doc_api_Rds_DescribeRegions .reference}

调用DescribeRegions接口查询当前可选的RDS地域和可用区信息。

调用创建实例接口[CreateDBInstance](~~26228~~)之前，可以先用本接口查询RegionId和ZoneId。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DescribeRegions&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeRegions|系统规定参数，取值：**DescribeRegions**。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Regions| | |可选的地域和可用区列表。

 |
|RegionId|String|cn-hangzhou|地域ID。

 |
|ZoneId|String|cn-hangzhou-b|可用区ID。

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://rds.aliyuncs.com/?Action=DescribeRegions
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
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

`JSON` 格式

``` {#json_return_success_demo}
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

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

