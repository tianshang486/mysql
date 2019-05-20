# DescribeBinlogFiles {#doc_api_1084643 .reference}

You can call this operation to view binlogs.

-   If **DownloadLink** is null, it indicates that the download link is unavailable.
-   If **DownloadLink** is not null, you can download backup files from this link. The expiration time for this link is specified by **LinkExpiredTime**. Make sure that you download the backup files before the expiration time.

**Note:** This operation is not applicable to SQL Server instances.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeBinlogFiles) to perform debugging.

API Explorer provides various functions to simplify API usage. For example, you can search APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeBinlogFiles| The operation that you want to perform. Set the value to **DescribeBinlogFiles**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|StartTime|String|Yes|2011-06-01T15:00:00Z| The start time of the query. Format: *yyyy-MM-dd*T*HH:mm:ss*Z.

 |
|EndTime|String|Yes|2011-06-20T15:00:00Z| The end time of the query. It must be later than the start time. Format: *yyyy-MM-dd*T*HH:mm:ss*Z.

 |
|PageSize|Integer|No|30| The number of records on each page. Valid values:

 -   **30**.
-   **50**.
-   **100**.

 Default value: **30**.

 |
|PageNumber|Integer|No|1| The page number. It must be greater than 0 and cannot exceed the maximum value of the Integer data type.

 Default value: **1**.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|TotalRecordCount|Integer|100| The total number of binlog files.

 |
|PageNumber|Integer|1| The page number.

 |
|PageRecordCount|Integer|30| The number of binlog files on the current page.

 |
|Items| | | The detailed list of binlogs.

 |
|└FileSize|Long|2269410| The size of the binlog file. Unit: byte.

 |
|└LogBeginTime|String|2019-02-09T17:45:21Z| The start time of logs in the binary file.

 |
|└LogEndTime|String|2019-02-15T13:10:28Z| The end time of logs in the binary file.

 |
|└DownloadLink|String|http://rdsxxxxx.oss.aliyuncs.com/xxxxxx| The HTTP download link. If this parameter is null, it indicates that the download link is unavailable.

 |
|└HostInstanceID|String|5841973| The ID of the instance to which a binlog file belongs. You can use this parameter to tell whether the binlog file is from a master or slave instance.

 |
|└LinkExpiredTime|String|2013-06-09T18:00:00Z| The expiration time of the download link.

 |
|└Checksum|String|18358304393468701857| The checksum.

 |
|└IntranetDownloadLink|String|http://rdslog-hz-v3.oss-cn-hangzhou-internal.aliyuncs.com/xxxxxx| The download link for the intranet.

 |
|└LogFileName|String|000000040000000000000019| The name of the binlog file.

 |
|RequestId|String|ED169A3E-1657-4104-82AB-24EA8CD0DB75| The ID of the request.

 |
|TotalFileSize|Long|2269410| The total size of binlog files.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeBinlogFiles
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2011-06-01T15:00:00Z
&EndTime=2011-06-20T15:00:00Z
&<Common request parameters>
```

Normal response example

`XML` format

``` {#xml_return_success_demo}
<DescribeBinlogFilesResponse>
  <Items/> 
  <PageNumber>1</PageNumber> 
  <TotalRecordCount>0</TotalRecordCount> 
  <TotalFileSize>0</TotalFileSize>
  <RequestId>ED169A3E-1657-4104-82AB-24EA8CD0DB75</RequestId>
  <PageRecordCount>0</PageRecordCount> 
</DescribeBinlogFilesResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"Items":{
		"BinLogFile":[]
	},
	"TotalRecordCount":0,
	"PageNumber":1,
	"TotalFileSize":"0",
	"RequestId":"ED169A3E-1657-4104-82AB-24EA8CD0DB75",
	"PageRecordCount":0
}
```

## Error codes {#errorcodes .section}

[View error codes](https://error-center.alibabacloud.com/status/product/Rds)

