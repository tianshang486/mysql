# Query summary of slow query logs

Queries the summary of slow query logs for an RDS instance.

When you call this operation, ensure that the version of the instance is as follows:

-   All MySQL versions except MySQL 5.7 Basic edition.
-   SQL Server 2008 R2
-   MariaDB 10.3.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeSlowLogs&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSlowLogs|The operation that you want to perform. Set the value to**DescribeSlowLogs**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|EndTime|String|Yes|2011-05-30Z|The end time of the query. It must be later than the start time. The time span between the start and end time must be less than 31 days. Specify the time in the *yyyy-MM-dd*Z format. |
|StartTime|String|Yes|2011-05-01Z|The start time of the query. Format: *yyyy-MM-dd*Z. |
|DBName|String|No|RDS\_MySQL|The name of the PolarDB-X database. |
|SortKey|String|No|TotalExecutionCounts|The basis on which query results are sorted. Valid values:

-   **TotalExecutionCounts**: the maximum number of total executions.
-   **TotalQueryTimes**: total execution time
-   **TotalLogicalReads**: total logic read most
-   **TotalPhysicalReads**: total physical read most

**Note:** This parameter is only supported by SQL Server 2008 R2 instances. |
|PageSize|Integer|No|30|The number of records on each page. Valid values:**30**~**100**. Default value: **30**. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|2553A660-E4EB-4AF4-A402-8AFF70A49143|The ID of the request. |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|Engine|String|MySQL|The database engine that the instance is running. |
|StartTime|String|2011-05-30Z|The start time of the query. |
|EndTime|String|2011-05-30Z|The end time of the query. |
|TotalRecordCount|Integer|5|The total number of backup sets. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageRecordCount|Integer|10|The number of slow SQL queries on the current page. |
|Items|Array| |The log information about slow queries. |
|SlowLogId|Long|26584213|The ID of slow query summary. |
|SQLHASH|String|U2FsdGVkxxxx|The unique ID of the SQL statement included in the slow query log statistics. You can use the unique ID to query logs of slow queries on the SQL statement. |
|SQLIdStr|String|521584|The SQL ID in the slow log statistics template. It is deprecated. Use **SQLHASH**instead. |
|DBName|String|RDS\_MySQL|The name of the PolarDB-X database. |
|SQLText|String|select id,name from tb\_table|The SQL statement. |
|MySQLTotalExecutionCounts|Long|1|The total number of MySQL executions. |
|MySQLTotalExecutionTimes|Long|1|The total execution time of MySQL. Unit: seconds. |
|TotalLockTimes|Long|0|The total lock duration of the SQL statement. Unit: seconds. |
|MaxLockTime|Long|0|The maximum lock duration of the SQL statement. Unit: seconds. |
|ParseTotalRowCounts|Long|1|The total rows of parsed SQL statements. |
|ParseMaxRowCount|Long|1|The maximum row of parsed SQL statements. |
|ReturnTotalRowCounts|Long|1|The total rows of returned SQL statements. |
|ReturnMaxRowCount|Long|1|The maximum row of returned SQL statements |
|CreateTime|String|2011-05-30Z|The date when the data is generated. |
|SQLServerTotalExecutionCounts|Long|1|The total number of SQL Server executions. |
|SQLServerTotalExecutionTimes|Long|1000|The total execution time of SQL Server. Unit: milliseconds. |
|TotalLogicalReadCounts|Long|1|The total number of logical reads. |
|TotalPhysicalReadCounts|Long|1|The total number of physical reads. |
|ReportTime|String|2011-05-30Z|The date when the data report is generated. |
|MaxExecutionTime|Long|60|The maximum execution time. Unit: seconds. |
|AvgExecutionTime|Long|1|The average execution time. Unit: seconds. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeSlowLogs
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2011-05-01Z
&EndTime=2011-05-30Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
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

```
{
    "DescribeSlowLogs": {
        "RequestId": "A5409D02-D661-4BF3-8F3D-0A814D0574E7",
        "DBInstanceID": "rm-uf6wjk5xxxxxxx",
        "Engine": "SQLServer",
        "StartTime": "2011-06-11Z",
        "EndTime": "2011-12-11Z",
        "TotalRecordCount": "1",
        "PageNumber": "1",
        "PageRecordCount": "1",
        "Items": {
            "SQLSlowLog": {
                "SQLText": "update test.zxb set id=0 limit 1",
                "SQLServerTotalExecutionCounts": "178",
                "SQLServerTotalExecutionTimes": "189",
                "TotalLogicalReadcounts": "89",
                "TotalPhysicalReadcounts": "90",
                "ReportTime": "2013-11-12Z"
            }
        }
    }
}
```

## Error code

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

