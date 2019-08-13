# DescribeSlowLogRecords {#doc_api_1106089 .reference}

You can call this operation to view the slow log details of an instance.

**Note:** 

-   The response parameters for this operation are updated once every minute.
-   This operation is not applicable to SQL Server instances.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeSlowLogRecords) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|DescribeSlowLogRecords| The operation that you want to perform. Set this parameter to DescribeSlowLogRecords.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxx| The instance of the ID.

 |
|StartTime|String|Yes|2011-06-01T16:00Z| The start time of the query. Format: yyyy-MM-ddTHH:mmZ.

 |
|EndTime|String|Yes|2011-06-20T16:00Z| The end time of the query. It must be later than the start time. The time span between the start and end time must be less than 31 days. Format: yyyy-MM-ddTHH:mmZ.

 |
|SQLHASH|String|No|U2FsdGVkxxxx| The unique ID of the SQL statement in the slow log statistics. It can be used to obtain the slow log details of the SQL statement.

 |
|DBName|String|No|RDS\_MySQL| The name of the database.

 |
|PageSize|Integer|No|30| The number of records on each page. Valid values:

 -   30
-   50
-   100

 Default value: 30.

 |
|PageNumber|Integer|No|1| The page number. It must be greater than 0 and cannot exceed the maximum value of the given Integer.

 Default value: 1.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Engine|String|MySQL| The type of the database.

 |
|TotalRecordCount|Integer|1| The total number of records.

 |
|PageNumber|Integer|1| The page number.

 |
|PageRecordCount|Integer|1| The number of SQL statements on the current page.

 |
|Items|N/A|N/A| The list of slow logs.

 |
|HostAddress|String|192.101.2.11| The client address used to connect to a database.

 |
|DBName|String|testDB| The name of the database.

 |
|SQLText|String|update test.zxb set id=0 limit 1;| The SQL statement.

 |
|QueryTimes|Long|20| The execution time of the SQL statement. Unit: second.

 |
|LockTimes|Long|12| The lock duration. Unit: second.

 |
|ParseRowCounts|Long|100| The number of parsed rows.

 |
|ReturnRowCounts|Long|1| The number of returned rows.

 |
|ExecutionStartTime|String|2011-06-11T15:00:08Z| The execution start time. Format: yyyy-MM-ddTHH:mm:ssZ.

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|RequestId|String|542BB8D6-4268-45CC-A557-B03EFD7AB30A| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeSlowLogRecords
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2011-06-01T16:00Z 
&EndTime=2011-06-20T16:00Z 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_tn8_slj_yes}
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

`JSON` format

``` {#codeblock_yic_le6_584}
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

## Error codes {#section_sp4_3bn_1aa .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

