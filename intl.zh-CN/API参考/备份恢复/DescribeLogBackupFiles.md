# DescribeLogBackupFiles {#doc_api_1085892 .reference}

调用DescribeLogBackupFiles接口查询实例的日志备份文件。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeLogBackupFiles)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeLogBackupFiles|系统规定参数。取值：**DescribeLogBackupFiles**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|StartTime|String|是|2018-10-01T08:40Z|查询开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z。

 |
|EndTime|String|是|2018-10-31T08:40Z|查询结束时间，必须晚于查询开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z。

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
|Items| | |日志文件列表。

 |
|└DownloadLink|String|http://rdsbak-hz-v3.oss-cn-hangzhou.aliyuncs.com/xxxxx|HTTP协议的下载链接。若当前不可下载，则为空串。

 |
|└FileSize|Long|788480|日志文件大小。单位：Byte。

 |
|└IntranetDownloadLink|String|http://rdsbak-hz-v3.oss-cn-hangzhou.aliyuncs.com/xxxxx|内网下载地址，若当前不可下载，则为空串。有效期1小时。

 |
|└LinkExpiredTime|String|2019-03-01T15:04:13Z|链接过期时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z。

 |
|└LogBeginTime|String|2018-10-31T08:40Z|日志文件记录的开始时间。

 |
|└LogEndTime|String|2018-10-31T08:40Z|日志文件记录的结束时间。

 |
|PageNumber|Integer|1|页码。

 |
|PageRecordCount|Integer|100|本页日志文件个数。

 |
|RequestId|String|F8EC669C-FC85-43D7-AF06-C3641626B37E|请求ID。

 |
|TotalFileSize|Long|2300|所有日志文件大小之和，单位：Byte。

 |
|TotalRecordCount|Integer|17|日志文件总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeLogBackupFiles
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2018-10-01T08:40Z
&EndTime=2018-10-31T08:40Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeLogBackupFilesResponse>
  <Items/>
  <PageNumber>1</PageNumber>
  <TotalRecordCount>0</TotalRecordCount>
  <RequestId>F8EC669C-FC85-43D7-AF06-C3641626B37E</RequestId>
  <PageRecordCount>0</PageRecordCount>
</DescribeLogBackupFilesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"BinLogFile":[]
	},
	"TotalRecordCount":0,
	"PageNumber":1,
	"RequestId":"F8EC669C-FC85-43D7-AF06-C3641626B37E",
	"PageRecordCount":0
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

