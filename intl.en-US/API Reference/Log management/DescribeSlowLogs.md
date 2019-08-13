# DescribeSlowLogs {#doc_api_Rds_DescribeSlowLogs .reference}

You can call this operation to view the statistics of slow logs.

**Note:** This operation is not applicable to SQL Server 2017 Cluster Edition instances.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeSlowLogs) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|DescribeSlowLogs| The operation that you want to perform. Set this parameter to DescribeSlowLogs.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|StartTime|String|Yes|2011-05-01Z| The start time of the query. Format: yyyy-MM-ddZ.

 |
|EndTime|String|Yes|2011-05-30Z| The end time of the query. It must be later than the start time. The time span between the start and end time must be less than or equal to 31 days. Format: yyyy-MM-ddZ.

 |
|DBName|String|No|RDS\_MySQL| The name of the database.

 |
|SortKey|String|No|TotalExecutionCounts| The basis on which query results are sorted. Valid values:

 -   TotalExecutionCounts
-   TotalQueryTimes
-   TotalLogicalReads
-   TotalPhysicalReads

 |
|PageSize|Integer|No|30| The number of records on each page. Valid values:

 -   30
-   50
-   100

 Default value: 30.

 |
|PageNumber|Integer|No|1| The page number. It must greater than 0 and cannot exceed the maximum value of the given Integer.

 Default value: 1.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Engine|String|MySQL| The type of the database.

 |
|StartTime|String|2011-05-30Z| The start time of the query.

 |
|EndTime|String|2011-05-30Z| The end time of the query.

 |
|TotalRecordCount|Integer|5| The total number of records.

 |
|PageNumber|Integer|1| The page number.

 |
|PageRecordCount|Integer|10| The number of SQL statements on the current page.

 |
|Items|N/A|N/A| The list of slow logs.

 |
|DBName|String|RDS\_MySQL| The name of the database.

 |
|SQLText|String|select id,name from tb\_table| The SQL statement.

 |
|SQLServerTotalExecutionCounts|Long|1| The total number of SQL Server executions.

 |
|MySQLTotalExecutionCounts|Long|1| The total number of MySQL executions.

 |
|SQLServerTotalExecutionTimes|Long|1,000| The total execution time of SQL Server. Unit: millisecond.

 |
|MySQLTotalExecutionTimes|Long|1| The total execution time of MySQL. Unit: second.

 |
|MaxExecutionTime|Long|60| The maximum execution time. Unit: second.

 |
|ReportTime|String|2011-05-30Z| The date when the data report is generated.

 |
|TotalLockTimes|Long|0| The total lock duration. Unit: second.

 |
|MaxLockTime|Long|0| The maximum lock duration. Unit: second.

 |
|ParseTotalRowCounts|Long|1| The total rows of parsed SQL statements.

 |
|ParseMaxRowCount|Long|1| The maximum row of parsed SQL statements.

 |
|ReturnTotalRowCounts|Long|1| The total rows of returned SQL statements.

 |
|ReturnMaxRowCount|Long|1| The maximum row of returned SQL statements

 |
|CreateTime|String|2011-05-30Z| The date when the data is generated.

 |
|AvgExecutionTime|Long|1| The average execution time. Unit: second.

 |
|SQLHASH|String|U2FsdGVkxxxx| The unique ID of the SQL statement in the slow log statistics. It can be used to obtain the slow log details of the SQL statement.

 |
|SQLIdStr|String|521584| the SQL ID in the slow log statistics template. It is deprecated. Use the SQLHASH parameter instead.

 |
|SlowLogId|Long|26584213| The ID of slow query summary.

 |
|TotalLogicalReadCounts|Long|1| The total number of logical reads.

 |
|TotalPhysicalReadCounts|Long|1| The total number of physical reads.

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|RequestId|String|2553A660-E4EB-4AF4-A402-8AFF70A49143| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeSlowLogs
&DBInstanceId=rm-uf6wjk5xxxxxxx 
&StartTime=2011-05-01Z
&EndTime=2011-05-30Z 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_lln_dmw_hm6}
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

`JSON` format

``` {#codeblock_jc1_538_ylc}
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

## Error codes {#section_5rh_32l_znb .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

