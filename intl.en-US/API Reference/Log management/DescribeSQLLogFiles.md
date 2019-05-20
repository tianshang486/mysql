# DescribeSQLLogFiles {#doc_api_1106095 .reference}

You can call this operation to query the list of SQL audit files of an RDS instance.

This operation is applicable to the following instances:

-   MySQL 5.5
-   MySQL 5.6
-   MySQL 5.7 High-availability Edition \(based on local SSDs\)
-   SQL Server 2008 R2
-   PostgreSQL
-   PPAS

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeSQLLogFiles) to perform debugging.

API Explorer provides various functions to simplify API usage. For example, you can search APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSQLLogFiles| The operation that you want to perform. Set the value to**DescribeSQLLogFiles**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxx| The ID of the instance.

 |
|FileName|String|No|custinsxxxxx.csv| The name of the audit file.

 |
|PageSize|Integer|No|20| The number of records on each page. Valid values: **1 to 50**.

 Default value: **20**.

 |
|PageNumber|Integer|No|1| The page number. Valid values: **1 to 100,000**.

 Default value: **1**.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|TotalRecordCount|Integer|10| The total number of records.

 |
|PageNumber|Integer|1| The page number.

 |
|PageRecordCount|Integer|10| The number of records on the current page.

 |
|Items| | | The list of audit files.

 |
|└FileID|String|custinsxxxxx.csv| The name of the file.

 |
|└LogStatus|String|Success| The status of the file. Valid values:

 -   **Success**.
-   **Failed**.
-   **Generating**.

 |
|└LogStartTime|String|2015-05-23T07:00:00Z| The SQL start time.

 |
|└LogEndTime|String|2015-05-24T07:00:00Z| The SQL end time.

 |
|└LogDownloadURL|String|http://rdslog-hz-v3.oss-cn-hangzhou.aliyuncs.com/xxxxx| The download link. If the download is unavailable, this link is empty.

 |
|└LogSize|String|3,000| The size of the audit file. Unit: byte.

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeSQLLogFiles
&DBInstanceId=rm-uf6wjk5xxxxxx
&<Common request parameters>
```

Normal response example

`XML` format

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
  <totalRecordCount>1</totalRecordCount>
</DescribeSQLLogFilesResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"totalRecordCount":1,
	"requestId":" 1AD222E9-E606-4A42-BF6D-8A4442913CEF",
	"items":[
		{
			"StartTime":"2015-05-23T07:00:00Z"
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

## Error codes { .section}

[View error codes](https://error-center.alibabacloud.com/status/product/Rds)

