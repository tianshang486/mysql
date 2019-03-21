# DescribeSlowLogs {#doc_api_1106084 .reference}

调用DescribeSlowLogs查看慢日志统计情况。

该接口用于查看实例的慢慢日志统计情况，支持分页查询。

**说明：** 该接口暂不支持SQL Server 2017集群版实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeSlowLogs)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSlowLogs|系统规定参数，取值：**DescribeSlowLogs**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|StartTime|String|是|2011-05-01Z|查询开始日期，格式：*yyyy-MM-dd*Z。

 |
|EndTime|String|是|2011-05-30Z|查询结束日期，不能小于查询开始日期，与查询开始日期间隔不超过31天。格式：*yyyy-MM-dd*Z。

 |
|DBName|String|否|RDS\_MySQL|数据库名称。

 |
|SortKey|String|否|TotalExecutionCounts|排序依据，取值：

 -   **TotalExecutionCounts**：总执行次数最多；
-   **TotalQueryTimes**：总执行时间最多；
-   **TotalLogicalReads**：总逻辑读最多；
-   **TotalPhysicalReads**：总物理读最多。

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
|Engine|String|MySQL|数据库类型。

 |
|StartTime|String|2011-05-30Z|查询开始日期。

 |
|EndTime|String|2011-05-30Z|查询结束日期。

 |
|TotalRecordCount|Integer|5|总记录数。

 |
|PageNumber|Integer|1|页码。

 |
|PageRecordCount|Integer|10|本页SQL语句个数。

 |
|Items| | |慢日志信息列表。

 |
|└DBName|String|RDS\_MySQL|数据库名称。

 |
|└SQLText|String|select id,name from tb\_table|SQL语句。

 |
|└SQLServerTotalExecutionCounts|Long|1|SQL Server总执行次数。

 |
|└MySQLTotalExecutionCounts|Long|1|MySQL总执行次数。

 |
|└SQLServerTotalExecutionTimes|Long|1000|SQL Server总执行时间，单位：毫秒。

 |
|└MySQLTotalExecutionTimes|Long|1|MySQL总执行时间，单位：秒。

 |
|└MaxExecutionTime|Long|60|最大执行时长，单位：秒。

 |
|└ReportTime|String|2011-05-30Z|数据报表生成日期。

 |
|└TotalLockTimes|Long|0|锁定总时长，单位：秒。

 |
|└MaxLockTime|Long|0|最大锁定时长，单位：秒。

 |
|└ParseTotalRowCounts|Long|1|解析总行数。

 |
|└ParseMaxRowCount|Long|1|解析最大行数。

 |
|└ReturnTotalRowCounts|Long|1|返回总行数。

 |
|└ReturnMaxRowCount|Long|1|返回最大行数。

 |
|└CreateTime|String|2011-05-30Z|数据生成日期。

 |
|└AvgExecutionTime|Long|1|平均执行时间，单位：秒。

 |
|└SQLHASH|String|U2FsdGVkxxxx|慢日志统计里的SQL语句唯一标识符，可用于获取该SQL语句的慢日志明细。

 |
|└SQLIdStr|String|521584|对应的是慢日志统计模版SQL的ID，现已废弃，请使用**SQLHASH**。

 |
|└SlowLogId|Long|26584213|慢查询汇总标识ID。

 |
|└TotalLogicalReadCounts|Long|1|总逻辑读。

 |
|└TotalPhysicalReadCounts|Long|1|总物理读。

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|实例ID。

 |
|RequestId|String|2553A660-E4EB-4AF4-A402-8AFF70A49143|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeSlowLogs
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2011-05-01Z
&EndTime=2011-05-30Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSlowLogsResponse>
  <RequestId>A5409D02-D661-4BF3-8F3D-0A814D0574E7</RequestId>
  <DBInstanceID>rm-uf6wjk5xxxxxxx</DBInstanceID>
  <Engine>SQLServer</Engine>
  <StartTime>2011-06-11Z</StartTime>
  <EndTime>2011-12-11Z</EndTime>
  <TotalRecordCount>1</TotalRecordCount>
  <PageNumber>1</PageNumber>
  <PageRecordCount>1</PageRecordCount>
  <Items>
    <SQLSlowLog>
      <SQLText>update test.zxb set id=0 limit 1</SQLText>
      <SQLServerTotalExecutionCounts>178</SQLServerTotalExecutionCounts>
      <SQLServerTotalExecutionTimes>189</SQLServerTotalExecutionTimes>
      <TotalLogicalReadcounts>89</TotalLogicalReadcounts>
      <TotalPhysicalReadcounts>90</TotalPhysicalReadcounts>
      <ReportTime>2013-11-12Z</ReportTime>
    </SQLSlowLog>
  </Items>
</DescribeSlowLogsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"DescribeSlowLogsResponse":{
		"Items":{
			"SQLSlowLog":{
				"SQLServerTotalExecutionTimes":"189",
				"SQLText":"update test.zxb set id=0 limit 1",
				"TotalLogicalReadcounts":"89",
				"SQLServerTotalExecutionCounts":"178",
				"TotalPhysicalReadcounts":"90",
				"ReportTime":"2013-11-12Z"
			}
		},
		"PageNumber":"1",
		"TotalRecordCount":"1",
		"DBInstanceID":"rm-uf6wjk5xxxxxxx",
		"RequestId":"A5409D02-D661-4BF3-8F3D-0A814D0574E7",
		"EndTime":"2011-12-11Z",
		"StartTime":"2011-06-11Z",
		"Engine":"SQLServer",
		"PageRecordCount":"1"
	}
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

