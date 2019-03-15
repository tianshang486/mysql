# DescribeBinlogFiles {#doc_api_1084643 .reference}

调用DescribeBinlogFiles接口查看Binlog日志。

-   当**DownloadLink**为NULL时，表示RDS没有提供下载链接URL；
-   当**DownloadLink**不为NULL时，用户可以根据此URL下载备份文件，此URL已设置过期时间**LinkExpiredTime**，请在过期时间之前下载。

**说明：** 本接口不适用于SQL Server实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeBinlogFiles)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeBinlogFiles|系统规定参数，取值：**DescribeBinlogFiles**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|StartTime|String|是|2011-06-01T15:00:00Z|查询开始时间，格式：*yyyy-MM-dd*T*HH:mm:ss*Z。

 |
|EndTime|String|是|2011-06-20T15:00:00Z|查询结束时间，大于查询开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z。

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
|TotalRecordCount|Integer|100|Binlog文件总数。

 |
|PageNumber|Integer|1|页码。

 |
|PageRecordCount|Integer|30|当前页Binlog文件个数。

 |
|Items| | |Binlog明细列表。

 |
|└FileSize|Long|2269410|Binlog文件大小，单位：Byte。

 |
|└LogBeginTime|String|2019-02-09T17:45:21Z|Binlog文件记录的开始时间。

 |
|└LogEndTime|String|2019-02-15T13:10:28Z|Binlog文件记录的结束时间。

 |
|└DownloadLink|String|http://rdsxxxxx.oss.aliyuncs.com/xxxxxx|支持HTTP协议的下载链接URL，NULL表示没有下载链接。

 |
|└HostInstanceID|String|5841973|Binlog所在实例编号，用户区分该Binlog日志产生于主实例或备实例。

 |
|└LinkExpiredTime|String|2013-06-09T18:00:00Z|URL过期时间。

 |
|└Checksum|String|18358304393468701857|校验和。

 |
|└IntranetDownloadLink|String|http://rdslog-hz-v3.oss-cn-hangzhou-internal.aliyuncs.com/xxxxxx|内网下载链接URL。

 |
|└LogFileName|String|000000040000000000000019|Binlog文件名称。

 |
|RequestId|String|ED169A3E-1657-4104-82AB-24EA8CD0DB75|请求ID。

 |
|TotalFileSize|Long|2269410|Binlog文件总大小。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeBinlogFiles
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2011-06-01T15:00:00Z
&EndTime=2011-06-20T15:00:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeBinlogFilesResponse>
  <Items/>
  <PageNumber>1</PageNumber>
  <TotalRecordCount>0</TotalRecordCount>
  <TotalFileSize>0</TotalFileSize>
  <RequestId>ED169A3E-1657-4104-82AB-24EA8CD0DB75</RequestId>
  <PageRecordCount>0</PageRecordCount>
</DescribeBinlogFilesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"BinLogFile":[]
	},
	"TotalRecordCount":0,
	"PageNumber":1,
	"TotalFileSize":"0",
	"RequestId":"ED169A3E-1657-4104-82AB-24EA8CD0DB75",
	"PageRecordCount":0
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

