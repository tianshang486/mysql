# Query slow query logs

You can call the DescribeSlowLogRecords operation to query the slow query logs of an ApsaraDB RDS instance.

**Note:**

-   The response parameters returned by this operation are updated every minute.
-   This operation is not supported for instances that run SQL Server.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeSlowLogRecords&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSlowLogRecords|The operation that you want to perform. Set the value to **DescribeSlowLogRecords**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxx|The ID of the instance. |
|EndTime|String|Yes|2020-06-18T16:00Z|The end of the time range to query. The end time must be later than the start time. The time span between the start time and the end time must be less than 31 days. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|StartTime|String|Yes|2020-06-17T16:00Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|SQLHASH|String|No|U2FsdGVkxxxx|The unique ID of the SQL statement to query. The ID is used to obtain the slow query logs of the SQL statement. |
|DBName|String|No|RDS\_MySQL|The name of the database to query. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values: **30** to **100**. Default value: **30**. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

 Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Engine|String|MySQL|The database engine that the instance runs. |
|TotalRecordCount|Integer|1|The total number of entries returned. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageRecordCount|Integer|1|The number of SQL statements returned on the current page. |
|Items|Array of SQLSlowRecord| |An array that consists of slow query logs. |
|SQLSlowRecord| | | |
|HostAddress|String|xxx\[xxx\] @ \[1xx.xxx.xxx.xx\]|The name and IP address of the client that is connected to the instance. |
|DBName|String|testDB|The name of the database queried. |
|SQLText|String|select sleep\(2\)|The details about the SQL statement. |
|QueryTimes|Long|2|The execution duration of the SQL statement. Unit: seconds. |
|LockTimes|Long|0|The lock duration of the SQL statement. Unit: seconds. |
|ParseRowCounts|Long|1|The number of rows parsed by the SQL statement. |
|ReturnRowCounts|Long|1|The number of rows returned by the SQL statement. |
|ExecutionStartTime|String|2020-06-18T01:40:44Z|The time when the execution of the SQL statement started. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|QueryTimeMS|Long|2001|The execution duration of the SQL statement. Unit: milliseconds. |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|RequestId|String|4DBB1BB0-E5D8-4D41-B1C9-142364DB4986|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeSlowLogRecords
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2020-06-17T16:00Z
&EndTime=2020-06-18T16:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
</DescribeSlowLogRecordsResponse>
<TotalRecordCount>1</TotalRecordCount>
<PageRecordCount>1</PageRecordCount>
<RequestId>4DBB1BB0-E5D8-4D41-B1C9-142364DB4986</RequestId>
<DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
<PageNumber>1</PageNumber>
<Items>
    <SQLSlowRecord>
        <QueryTimes>2</QueryTimes>
        <ExecutionStartTime>2020-07-20T02:03:10Z</ExecutionStartTime>
        <ReturnRowCounts>1</ReturnRowCounts>
        <LockTimes>0</LockTimes>
        <DBName>testDB</DBName>
        <ParseRowCounts>1</ParseRowCounts>
        <HostAddress>test1[test1] @  [100.xxx.xxx.xxx]</HostAddress>
        <QueryTimeMS>2000</QueryTimeMS>
        <SQLText>select sleep(2)</SQLText>
    </SQLSlowRecord>
</Items>
<Engine>MySQL</Engine>
</DescribeSlowLogRecordsResponse>
```

`JSON` format

```
{
	"TotalRecordCount": 1,
	"PageRecordCount": 1,
	"RequestId": "4DBB1BB0-E5D8-4D41-B1C9-142364DB4986",
	"DBInstanceId": "rm-uf6wjk5xxxxxxx",
	"PageNumber": 1,
	"Items": {
		"SQLSlowRecord": [
			{
				"QueryTimes": 2,
				"ExecutionStartTime": "2020-07-20T02:03:10Z",
				"ReturnRowCounts": 1,
				"LockTimes": 0,
				"DBName": "testDB",
				"ParseRowCounts": 1,
				"HostAddress": "test1[test1] @  [100.xxx.xxx.xxx]",
				"QueryTimeMS": 2000,
				"SQLText": "select sleep(2)"
			}
		]
	},
	"Engine": "MySQL"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

