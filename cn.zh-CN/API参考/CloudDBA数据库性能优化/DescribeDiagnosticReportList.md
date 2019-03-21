# DescribeDiagnosticReportList {#doc_api_1105951 .reference}

调用DescribeDiagnosticReportList接口获取诊断报告列表。

返回[诊断报告](~~96129~~)的数据采集时间、生成时间和下载地址等，诊断报告保留15天。

**说明：** SQL Server 2017集群版不支持该接口。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDiagnosticReportList)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDiagnosticReportList|系统规定参数。取值：**DescribeDiagnosticReportList**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B7E9A79C-DE1B-4398-845F-D654FC0958BD|请求ID。

 |
|ReportList| | |返回的诊断报告列表。

 |
|└DiagnosticTime|String|2018-01-17T12:46:09Z|诊断时间。

 |
|└DownloadURL|String|http://rdsreport-hz-v3.oss-cn-hangzhou.aliyuncs.com/xxxxx|公网下载地址，若当前不可下载，则为空串。

 |
|└EndTime|String|2012-06-11T15:00Z|监控数据结束时间。

 |
|└Score|Integer|100|诊断分数。

 |
|└StartTime|String|2012-06-11T15:00Z|监控数据起始时间。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDiagnosticReportList
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDiagnosticReportListResponse>
  <reportList>
    <diagnosticTime>2018-01-17T12:46:09Z</diagnosticTime>
    <downloadURL>http://rdsreport-hzi-v2.oss-cn-hangzhou-i.aliyuncs.com/xxxxx</downloadURL>
    <endTime>2018-01-10T15:31:00Z</endTime>
    <score>100</score>
    <startTime>2018-01-10T15:30:00Z</startTime>
  </reportList>
  <requestId>B7E9A79C-DE1B-4398-845F-D654FC0958BD</requestId>
</DescribeDiagnosticReportListResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"B7E9A79C-DE1B-4398-845F-D654FC0958BD",
	"reportList":[
		{
			"startTime":"2018-01-10T15:30:00Z",
			"downloadURL":"http://rdsreport-hzi-v2.oss-cn-hangzhou-i.aliyuncs.com/xxxxx",
			"score":100,
			"diagnosticTime":"2018-01-17T12:46:09Z",
			"endTime":"2018-01-10T15:31:00Z"
		}
	]
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

