# Query error logs

Queries error logs of an ApsaraDB for RDS instance within a specified time range.

Error logs contain the time when they were generated and the error messages.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeErrorLogs&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeErrorLogs|The operation that you want to perform. Set the value to **DescribeErrorLogs**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|EndTime|String|Yes|2011-05-30T20:10Z|The end of the time range to query. The end time must be later than the start time. The time span between the start time and the end time must be less than 31 days. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|StartTime|String|Yes|2011-05-01T20:10Z|The start of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values: **30** to **100**. Default value: **30**. |
|PageNumber|Integer|No|1|The number of the page to return. Valid values: a non-zero positive integer.

 Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|TotalRecordCount|Integer|100|The total number of error logs. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageRecordCount|Integer|30|The number of error logs on the current page. |
|Items|Array| |The list of items in an error log. |
|ErrorLog| | | |
|ErrorInfo|String|spid52 DBCC TRACEON 3499, server process ID \(SPID\) 52. This is an informational message only; no user action is required|The error log information. |
|CreateTime|String|2011-05-30T12:11:04Z|The time when the error log was generated. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|RequestId|String|98504E07-BB0E-40FC-B152-E4882615812C|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeErrorLogs
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2011-05-01T20:10Z
&EndTime=2011-05-30T20:10Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeErrorLogsResponse>
	  <RequestId>98504E07-BB0E-40FC-B152-E4882615812C</RequestId>
	  <PageNumber>1</PageNumber>
	  <TotalRecordCount>1</TotalRecordCount>
	  <PageRecordCount>1</PageRecordCount>
	  <Items>
		    <ErrorLog>
			      <ErrorInfo>spid52 DBCC TRACEON 3499, server process ID (SPID) 52. This is an informational message only; no user action is required</ErrorInfo>
			      <CreateTime>2013-06-04T15:00:00</CreateTime>
		    </ErrorLog>
      </Items>
</DescribeErrorLogsResponse>
```

`JSON` format

```
{
"RequestId":"98504E07-BB0E-40FC-B152-E4882615812C",
"PageNumber":1,
"TotalRecordCount":1,
"PageRecordCount":1,
"Items":
{"ErrorLog":
[
{
"ErrorInfo":"spid52 DBCC TRACEON 3499, server process ID (SPID) 52. This is an informational message only; no user action is required",
"CreateTime":"2013-06-04T15:00:00"
}
]
}
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

