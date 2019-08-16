# DescribeSlowLogRecords {#doc_api_Rds_DescribeSlowLogRecords .reference}

调用DescribeSlowLogRecords接口查看实例的慢日志明细。

**说明：** 

-   本接口的返回参数每分钟更新一次。
-   暂不支持SQL Server类型的实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DescribeSlowLogRecords&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSlowLogRecords|系统规定参数，取值：**DescribeSlowLogRecords**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxx|实例ID。

 |
|StartTime|String|是|2011-06-01T16:00Z|查询开始时间。格式：*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|EndTime|String|是|2011-06-20T16:00Z|查询结束时间，需要大于查询开始时间，与查询开始时间间隔小于31天。格式：*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|SQLHASH|String|否|U2FsdGVkxxxx|慢日志统计里的SQL语句唯一标识符，可用于获取该SQL语句的慢日志明细。

 |
|DBName|String|否|RDS\_MySQL|数据库名称。

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
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Engine|String|MySQL|数据库类型。

 |
|TotalRecordCount|Integer|1|总记录数。

 |
|PageNumber|Integer|1|页码。

 |
|PageRecordCount|Integer|1|本页SQL语句个数。

 |
|Items| | |慢日志明细列表。

 |
|HostAddress|String|192.101.2.11|连接数据库的客户端地址。

 |
|DBName|String|testDB|数据库名称。

 |
|SQLText|String|update test.zxb set id=0 limit 1;|查询语句。

 |
|QueryTimes|Long|20|执行时长，单位：秒。

 |
|LockTimes|Long|12|锁定时长，单位：秒。

 |
|ParseRowCounts|Long|100|解析行数。

 |
|ReturnRowCounts|Long|1|返回行数。

 |
|ExecutionStartTime|String|2011-06-11T15:00:08Z|执行开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|实例ID。

 |
|RequestId|String|542BB8D6-4268-45CC-A557-B03EFD7AB30A|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeSlowLogRecords
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2011-06-01T16:00Z
&EndTime=2011-06-20T16:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSlowLogRecordsResponse> 
    <RequestId>542BB8D6-4268-45CC-A557-B03EFD7AB30A</RequestId>
    <DBInstanceID>rm-uf6wjk5xxxxxxx</DBInstanceID> 
    <Engine>MySQL</Engine>
    <TotalRecordCount>1</TotalRecordCount>
    <PageNumber>1</PageNumber>
    <PageRecordCount>1</PageRecordCount>
    <Items>
        <SQLSlowRecord>
          <HostAddress>192.101.2.11</HostAddress>
          <DBName>test</DBName>
          <SQLText>update test.zxb set id=0 limit 1</SQLText>
          <QueryTimes>123</QueryTimes>
          <LockTimes>12</LockTimes>
          <ParseRowCounts>125</ParseRowCounts>
          <ReturnRowCounts>1</ReturnRowCounts>
          <ExecutionStartTime>2011-06-11T15:00:08Z</ExecutionStartTime>
        </SQLSlowRecord>
    </Items>
</DescribeSlowLogRecordsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"DescribeSlowLogRecordsResponse":{
		"Items":{
			"SQLSlowRecord":{
				"ReturnRowCounts":"1",
				"HostAddress":"192.101.2.11",
				"SQLText":"update test.zxb set id=0 limit 1",
				"LockTimes":"12",
				"ExecutionStartTime":"2011-06-11T15:00:08Z",
				"ParseRowCounts":"125",
				"QueryTimes":"123",
				"DBName":"test"
			}
		},
		"PageNumber":"1",
		"TotalRecordCount":"1",
		"DBInstanceID":"rm-uf6wjk5xxxxxxx",
		"RequestId":"542BB8D6-4268-45CC-A557-B03EFD7AB30A",
		"Engine":"MySQL",
		"PageRecordCount":"1"
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

