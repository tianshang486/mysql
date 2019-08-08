# DescribeDBInstancePerformance {#doc_api_Rds_DescribeDBInstancePerformance .reference}

调用DescribeDBInstancePerformance接口查看实例性能数据。

根据性能参数查看某个实例、某时间段范围内的性能监控数据。根据版本、[监控频率](~~26200~~)（[ModifyDBInstanceMonitor](~~26282~~)）和查询时间范围的不同，有如下几种输出形式：

-   除MySQL 5.7高可用云盘版和MariaDB之外的版本：
    -   监控频率为5秒：
        -   查询时间范围大于7天，采集粒度为1天；
        -   查询时间范围大于1天，小于等于7天，采集粒度为1小时；
        -   查询时间范围大于1小时，小于等于1天，采集粒度为1分钟；
        -   查询时间范围小于等于1小时，采集粒度为5秒。
    -   监控频率为60秒：
        -   查询范围大于30天的，采集粒度为1天；
        -   查询范围大于7天小于等于30天的，采集粒度为1小时；
        -   查询范围小于等于7天的，采集粒度为1分钟。
    -   监控频率为300秒：
        -   查询范围大于30天的，采集粒度为1天；
        -   查询范围大于7天小于等于30天的，采集粒度为1小时；
        -   查询范围小于等于7天的，采集粒度为5分钟。
-   MySQL 5.7高可用云盘版和MariaDB：
    -   查询范围大于30天的，采集粒度为1天；
    -   查询范围大于7天小于等于30天的，采集粒度为1小时；
    -   查询范围小于等于7天的，采集粒度为1分钟。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DescribeDBInstancePerformance&type=RPC&version=2014-08-15)

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
|StartTime|String|是|2012-06-08T15:00Z|查询开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|EndTime|String|是|2012-06-18T15:00Z|查询结束时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|Engine|String|MySQL|数据库类型。

 |
|StartTime|String|2012-06-10T15:00Z|查询开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|EndTime|String|2012-06-19T15:00Z|查询结束时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|PerformanceKeys| | |实例性能参数列表。

 |
|Key|String|MySQL\_Sessions|性能参数。

 |
|Unit|String|KB|数据单位。

 |
|ValueFormat|String|recv\_k&sent\_k|性能值的格式。如果性能值由多个参数构成，以“&”分隔，例如com\_delete&com\_insert&com\_insert\_select&com\_replace。

 |
|Values| | |数组格式：\{value1, value2, …\}。

 |
|Value|String|0.0&13.6|性能值。

 |
|Date|String|2011-05-30T03:29:00Z|记录日期。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

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
	  <DBInstanceID> rm-uf6wjk5xxxxxxx</DBInstanceID>
	  <StartTime>2012-06-11T15:00Z</StartTime>
	  <EndTime>2013-10-17T15:00Z</EndTime>
	  <Engine>MySQL</Engine>
	  <PerformanceKeys>
		    <PerformanceKey>
			      <Key>MySQL_NetworkTraffic</Key>
			      <Unit>KB</Unit>
			      <ValueFormat>recv_k&amp;sent_k</ValueFormat>
			      <Values></Values>
		    </PerformanceKey>
	  </PerformanceKeys></DescribeDBInstancePerformanceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"DBInstanceID":" rm-uf6wjk5xxxxxxx",
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

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

