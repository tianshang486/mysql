# DescribeSQLLogRecords {#doc_api_Rds_DescribeSQLLogRecords .reference}

调用DescribeSQLLogRecords接口查询实例的SQL审计日志。

支持的实例版本如下：

-   MySQL 5.5
-   MySQL 5.6
-   MySQL 5.7高可用本地盘版
-   SQL Server 2008 R2
-   PostgreSQL
-   PPAS

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeSQLLogRecords)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSQLLogRecords|系统规定参数，取值：**DescribeSQLLogRecords**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|StartTime|String|是|2011-06-01T15:00:00Z|查询开始时间，格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|EndTime|String|是|2011-06-11T15:00:00Z|查询结束时间，大于查询开始时间，与查询开始时间间隔小于31天。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|SQLId|Long|否|25623548|SQL语句唯一标识ID。

 |
|QueryKeywords|String|否|rds|用于查询的关键字，多个关键字以空格分隔，不超过10个关键字。

 |
|Database|String|否|Database|数据库名称。默认为所有数据库，也可以输入数据库名称查询，一次只能输入一个。

 |
|User|String|否|user|用户名称。默认为所有用户，也可以输入用户名称查询，一次只能输入一个。

 |
|Form|String|否|Stream|触发审计文件的生成或者返回SQL记录列表，取值：

 -   **File**：若传入这个值，则触发审计文件的生成，只返回公共参数，需再调用[DescribeSQLLogFiles](~~26295~~)接口获取文件的最终下载地址；
-   **Stream**：默认值，返回SQL记录列表。

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
|TotalRecordCount|Long|100|总记录数。

 |
|PageNumber|Integer|1|页码。

 |
|PageRecordCount|Integer|30|本页SQL审计日志个数。

 |
|Items| | |SQL审计日志列表。

 |
|└DBName|String|testDB|数据库名称。

 |
|└AccountName|String|accounttest|执行操作的账号名称。

 |
|└HostAddress|String|192.168.0.121|连接数据库的客户端IP地址。

 |
|└SQLText|String|update test.zxb set id=0 limit 1|SQL语句。

 |
|└TotalExecutionTimes|Long|600|执行耗时，单位：微秒。

 |
|└ReturnRowCounts|Long|30|返回记录数。

 |
|└ThreadID|String|1025865428|线程ID。

 |
|└ExecuteTime|String|2011-06-11T15:00:23Z|执行时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|RequestId|String|08A3B71B-FE08-4B03-974F-CC7EA6DB1828|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeSQLLogRecords
&DBInstanceId=rm-uf6wjk5xxxxxx
&StartTime=2011-06-01T15:00:00Z
&EndTime=2011-06-11T15:00:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSQLLogRecordsResponse>
  <PageNumber>1</PageNumber>
  <TotalRecordCounts>1</TotalRecordCounts>
  <ItemsCounts>1</ItemsCounts>
  <SQLItems>
    <SQLItem>
      <DBName>test</DBName>
      <AccountName>accounttest</AccountName>
      <HostAddress>192.168.0.121</HostAddress>
      <SQLText>update test.zxb set id=0 limit 1</SQLText>
      <TotalExecutionTimes>12</TotalExecutionTimes>
      <ReturnRowCounts>34</ReturnRowCounts>
      <ExecuteTime>2011-06-11T15:00:23Z</ExecuteTime>
    </SQLItem>
  </SQLItems>
  <RequestId>08A3B71B-FE08-4B03-974F-CC7EA6DB1828</RequestId>
</DescribeSQLLogRecordsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"RequestId":"08A3B71B-FE08-4B03-974F-CC7EA6DB1828",
	"TotalRecordCounts":1,
	"SQLItems":{
		"SQLItem":[
			{
				"ReturnRowCounts":34,
				"TotalExecutionTimes":12,
				"HostAddress":"192.168.0.121",
				"ExecuteTime":"2011-06-11T15:00:23Z",
				"SQLText":"update test.zxb set id=0 limit 1",
				"AccountName":"accounttest",
				"DBName":"test"
			}
		]
	},
	"ItemsCounts":1
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

