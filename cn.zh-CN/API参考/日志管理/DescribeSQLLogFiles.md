# DescribeSQLLogFiles {#doc_api_Rds_DescribeSQLLogFiles .reference}

调用DescribeSQLLogFiles接口查询SQL审计文件列表。

支持的实例版本如下：

-   MySQL 5.5
-   MySQL 5.6
-   MySQL 5.7高可用本地盘版
-   SQL Server 2008 R2
-   PostgreSQL
-   PPAS

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DescribeSQLLogFiles&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSQLLogFiles|系统规定参数，取值：**DescribeSQLLogFiles**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxx|实例ID。

 |
|FileName|String|否|custinsxxxxx.csv|审计文件名称。

 |
|PageSize|Integer|否|20|每页记录数，取值：**1-50**。

 默认值：**20**。

 |
|PageNumber|Integer|否|1|页码，取值：**1-100000**。

 默认值：**1**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|TotalRecordCount|Integer|10|总记录数。

 |
|PageNumber|Integer|1|页码。

 |
|PageRecordCount|Integer|10|本页记录数。

 |
|Items| | |审计文件列表。

 |
|FileID|String|custinsxxxxx.csv|文件名称。

 |
|LogStatus|String|Success|文件当前状态，取值：

 -   **Success**：生成成功；
-   **Failed**：生成失败；
-   **Generating**：生成中。

 |
|LogStartTime|String|2015-05-23T07:00:00Z|SQL起始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|LogEndTime|String|2015-05-24T07:00:00Z|SQL结束时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|LogDownloadURL|String|http://rdslog-hz-v3.oss-cn-hangzhou.aliyuncs.com/xxxxx|下载地址。若当前不可下载，则为空。

 |
|LogSize|String|3000|日志文件大小，单位：Byte。

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeSQLLogFiles
&DBInstanceId=rm-uf6wjk5xxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSQLLogFilesResponse>
	  <items>
		    <FileID>ZUBaS964T3OYtxxxxxxxx</FileID>
		    <LogStatus>Success</LogStatus>
		    <LogStartTime>2015-05-23T07:00:00Z</LogStartTime>
		    <LogEndTime>2015-05-23T07:00:00Z</LogEndTime>
		    <LogDownloadURL>xxxxxx.cn-hangzhou.oss.aliyun-inc.com/xxxxx</LogDownloadURL>
		    <LogSize>257</LogSize>
	  </items>
	  <pageRecordCount>1</pageRecordCount>
	  <requestId> 1AD222E9-E606-4A42-BF6D-8A4442913CEF</requestId>
	  <totalRecordCount>1</totalRecordCount></DescribeSQLLogFilesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"totalRecordCount":1,
	"requestId":" 1AD222E9-E606-4A42-BF6D-8A4442913CEF",
	"items":[
		{
			"LogStartTime":"2015-05-23T07:00:00Z",
			"LogEndTime":"2015-05-23T07:00:00Z",
			"LogStatus":"Success",
			"FileID":"ZUBaS964T3OYtxxxxxxxx",
			"LogDownloadURL":"xxxxxx.cn-hangzhou.oss.aliyun-inc.com/xxxxx",
			"LogSize":"257"
		}
	],
	"pageRecordCount":1
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

