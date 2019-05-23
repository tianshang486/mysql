# DescribeErrorLogs {#doc_api_Rds_DescribeErrorLogs .reference}

调用DescribeErrorLogs接口查看实例某段时间内的错误日志。

错误日志包含具体的错误信息和错误日志生成时间。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeErrorLogs)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeErrorLogs|系统规定参数，取值：**DescribeErrorLogs**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|StartTime|String|是|2011-05-01T20:10Z|查询开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|EndTime|String|是|2011-05-30T20:10Z|查询结束时间，大于查询开始时间，与查询开始时间间隔小于31天。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|PageSize|Integer|否|30|每页记录数，取值：

 -   **30**；
-   **50**；
-   **100**。

 默认值：**30**。

 |
|PageNumber|Integer|否|1|页码，取值：大于0且不超过Integer的最大值。

 默认值：**1**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|TotalRecordCount|Integer|100|总记录数。

 |
|PageNumber|Integer|1|页码。

 |
|PageRecordCount|Integer|30|本页错误日志个数。

 |
|Items| | |错误日志明细列表。

 |
|└ErrorInfo|String|spid52 DBCC TRACEON 3499, server process ID \(SPID\) 52. This is an informational message only; no user action is required|错误日志信息。

 |
|└CreateTime|String|2011-05-30T12:11:04Z|错误日志生成时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|RequestId|String|98504E07-BB0E-40FC-B152-E4882615812C|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeErrorLogs
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2011-05-01T20:10Z
&EndTime=2011-05-30T20:10Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeErrorLogsResponse>
  <RequestId>98504E07-BB0E-40FC-B152-E4882615812C</RequestId>
  <PageNumber>1</PageNumber>
  <TotalRecordCount>1</TotalRecordCount>
  <PageRecordCount>1</PageRecordCount>
  <Items>
    <ErrorLog>
      <ErrorInfo>spid52 DBCC TRACEON 3499, server process ID (SPID) 52. This is an informational message only; no user action is required</ErrorInfo>
      <CreateTime>2013-06-04T15:00:00</CreateTime>
    </ErrorLog>
  </Items>
</DescribeErrorLogsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"ErrorLog":[
			{
				"ErrorInfo":"spid52 DBCC TRACEON 3499, server process ID (SPID) 52. This is an informational message only; no user action is required",
				"CreateTime":"2013-06-04T15:00:00"
			}
		]
	},
	"TotalRecordCount":1,
	"PageNumber":1,
	"RequestId":"98504E07-BB0E-40FC-B152-E4882615812C",
	"PageRecordCount":1
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

