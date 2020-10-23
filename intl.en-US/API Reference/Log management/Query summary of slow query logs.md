# Query summary of slow query logs

You can call the DescribeSlowLogs operation to query the summary of slow query logs of an ApsaraDB RDS instance.

Before you call this operation, make sure that the instance runs one of the following database engine versions and RDS editions:

-   All MySQL editions \(except MySQL 5.7 that is used with the RDS Basic edition\)
-   SQL Server 2008 R2
-   MariaDB 10.3

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeSlowLogs&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSlowLogs|The operation that you want to perform. Set the value to **DescribeSlowLogs**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|EndTime|String|Yes|2011-05-30Z|The end of the time range to query. The end time must be later than the start time. The time span between the start time and the end time cannot exceed 31 days. Specify the time in the *yyyy-MM-dd*Z format. |
|StartTime|String|Yes|2011-05-01Z|The beginning of the time range to query. Specify the time in the *yyyy-MM-dd*Z format. |
|DBName|String|No|RDS\_MySQL|The name of the database to query. |
|SortKey|String|No|TotalExecutionCounts|The dimension based on which to sort the query results. Valid values:

 -   **TotalExecutionCounts**: sorts the query results based on the total number of execution times.
-   **TotalQueryTimes**: sorts the query results based on the total execution duration.
-   **TotalLogicalReads**: sorts the query results based on the total number of logical reads.
-   **TotalPhysicalReads**: sorts the query results based on the total number of physical reads.

 **Note:** This parameter is supported only for instances that run SQL Server 2008 R2. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values: **30** to **100**. Default value: **30**. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

 Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Engine|String|MySQL|The database engine that the instance runs. |
|StartTime|String|2011-05-30Z|The beginning of the time range queried. |
|EndTime|String|2011-05-30Z|The end of the time range queried. |
|TotalRecordCount|Integer|5|The total number of entries returned. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageRecordCount|Integer|10|The number of SQL statements returned on the current page. |
|Items|Array of SQLSlowLog| |An array that consists of slow query logs. |
|SQLSlowLog| | | |
|DBName|String|RDS\_MySQL|The name of the database queried. |
|SQLText|String|select id,name from tb\_table|The SQL statement recorded in the log. |
|SQLServerTotalExecutionCounts|Long|1|The total execution times of the SQL statement if the instance runs SQL Server. |
|MySQLTotalExecutionCounts|Long|1|The total execution times of the SQL statement if the instance runs MySQL. |
|SQLServerTotalExecutionTimes|Long|1000|The total execution duration of the SQL statement if the instance runs SQL Server. Unit: milliseconds. |
|MySQLTotalExecutionTimes|Long|1|The total execution duration of the SQL statement if the instance runs MySQL. Unit: seconds. |
|MaxExecutionTime|Long|60|The longest execution duration of the SQL statement among all logged execution durations. Unit: seconds. |
|ReportTime|String|2011-05-30Z|The date when the log was generated. |
|TotalLockTimes|Long|0|The total lock duration of the SQL statement. Unit: seconds. |
|MaxLockTime|Long|0|The longest lock duration of the SQL statement among all logged lock durations. Unit: seconds. |
|ParseTotalRowCounts|Long|1|The total number of rows parsed by the SQL statement. |
|ParseMaxRowCount|Long|1|The largest number of rows parsed by the SQL statement among all logged numbers. |
|ReturnTotalRowCounts|Long|1|The total number of rows returned by the SQL statement. |
|ReturnMaxRowCount|Long|1|The largest number of rows returned by the SQL statement among all logged numbers. |
|CreateTime|String|2011-05-30Z|The date when the SQL statement was executed. |
|AvgExecutionTime|Long|1|The average execution duration of the SQL statement. Unit: seconds. |
|SQLHASH|String|U2FsdGVkxxxx|The unique ID of the SQL statement. The ID is used to obtain the slow query logs of the SQL statement. |
|SQLIdStr|String|521584|The ID of the SQL statement. This parameter is replaced by the **SQLHASH** parameter. |
|SlowLogId|Long|26584213|The ID of the log. |
|TotalLogicalReadCounts|Long|1|The total number of logical reads. |
|TotalPhysicalReadCounts|Long|1|The total number of physical reads. |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|RequestId|String|2553A660-E4EB-4AF4-A402-8AFF70A49143|The ID of the request. |

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

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

