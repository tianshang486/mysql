# CreateDiagnosticReport {#doc_api_Rds_CreateDiagnosticReport .reference}

调用CreateDiagnosticReport接口创建诊断报告。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CreateDiagnosticReport)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDiagnosticReport|系统规定参数。取值：**CreateDiagnosticReport**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxx|实例ID。

 |
|StartTime|String|是|2018-06-11T15:00Z|用于生成诊断报告的监控数据起始时间。

 **说明：** 格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|EndTime|String|是|2018-06-12T15:00Z|用于生成诊断报告的监控数据结束时间。

 **说明：** 格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ReportId|String|10166270|诊断报告ID。

 |
|RequestId|String|8DA8956A-53DA-423E-9540-387428ED37FF-5711|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CreateDiagnosticReport
&DBInstanceId=rm-uf6wjk5xxxxxx
&StartTime=2018-06-11T15:00Z
&EndTime=2018-06-12T15:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateDiagnosticReportResponse>
  <reportId>10166270</reportId>
  <requestId>8DA8956A-53DA-423E-9540-387428ED37FF-5711</requestId>
</CreateDiagnosticReportResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"8DA8956A-53DA-423E-9540-387428ED37FF-5711",
	"reportId":"10166270"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

