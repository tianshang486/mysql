# DescribeDBInstancePerformance {#doc_api_1104939 .reference}

调用DescribeDBInstancePerformance接口查看实例性能数据。

根据性能参数查看某个实例、某时间段范围内的性能监控数据。根据查询时间范围的不同，有如下3种输出形式：

-   查询时间范围小于等于1天，采集粒度为5分钟；
-   查询时间范围大于7天小于等于15天，采集粒度为1小时；
-   查询时间范围大于等于30天小于等于1年，采集粒度为1天。

**说明：** 

-   查询时间范围大于1天小于7天，暂不支持；
-   查询时间范围大于15天小于30天，暂不支持。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstancePerformance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstancePerformance|系统规定参数，取值：**DescribeDBInstancePerformance**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|Key|String|是|MySQL\_Sessions|想要查询的性能指标，多个值用英文逗号（,）分隔，详细参数请参见[性能参数表](~~26316~~)。

 **说明：** **Key**为**MySQL\_SpaceUsage**或**SQLServer\_SpaceUsage**时，仅支持查询1天内的监控数据。

 |
|StartTime|String|是|2012-06-08T15:00Z|查询开始时间。格式：*yyyy-MM-dd*T*HH:mm*Z。

 |
|EndTime|String|是|2012-06-18T15:00Z|查询结束时间。格式：*yyyy-MM-dd*T*HH:mm*Z。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|Engine|String|MySQL|数据库类型。

 |
|StartTime|String|2012-06-10T15:00Z|查询开始时间。

 |
|EndTime|String|2012-06-19T15:00Z|查询结束时间。

 |
|PerformanceKeys| | |实例性能参数列表。

 |
|└Key|String|MySQL\_Sessions|性能参数。

 |
|└Unit|String|KB|数据单位。

 |
|└ValueFormat|String|recv\_k&sent\_k|性能值的格式。如果性能值由多个参数构成，以“&”分隔，例如com\_delete&com\_insert&com\_insert\_select&com\_replace。

 |
|└Values| | |数组格式：\{value1, value2, …\}。

 |
|└Value|String|0.0&13.6|性能值。

 |
|└Date|String|2011-05-30T03:29:00Z|记录日期。

 |
|RequestId|String|A5409D02-D661-4BF3-8F3D-0A814D0574E7|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDBInstancePerformance
&DBInstanceId= rm-uf6wjk5xxxxxxx
&Key=MySQL_Sessions
&StartTime=2012-06-08T15:00Z
&EndTime=2012-06-18T15:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstancePerformanceResponse>
  <RequestId>A5409D02-D661-4BF3-8F3D-0A814D0574E7</RequestId>
  <DBInstanceID>rdsaiiabnaiiabn</DBInstanceID>
  <StartTime>2012-06-11T15:00Z</StartTime>
  <EndTime>2013-10-17T15:00Z</EndTime>
  <Engine>MySQL</Engine>
  <PerformanceKeys>
    <PerformanceKey>
      <Key>MySQL_NetworkTraffic</Key>
      <Unit>KB</Unit>
      <ValueFormat>recv_k&amp;sent_k</ValueFormat>
      <Values/>
    </PerformanceKey>
  </PerformanceKeys>
</DescribeDBInstancePerformanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"DBInstanceID":"rdsaiiabnaiiabn",
	"RequestId":"A5409D02-D661-4BF3-8F3D-0A814D0574E7",
	"PerformanceKeys":{
		"PerformanceKey":[
			{
				"Values":{
					"PerformanceValue":[]
				},
				"Key":"MySQL_NetworkTraffic",
				"Unit":"KB",
				"ValueFormat":"recv_k&sent_k"
			}
		]
	},
	"EndTime":"2013-10-17T15:00Z",
	"StartTime":"2012-06-11T15:00Z",
	"Engine":"MySQL"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

