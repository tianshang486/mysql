# Query log backup files

You can call the DescribeBinlogFiles operation to query the log backup files of an ApsaraDB RDS instance.

-   If the returned value of the **DownloadLink** parameter is NULL for a log backup file, ApsaraDB RDS does not provide a download URL for the file.
-   If the returned value of the **DownloadLink** parameter is not NULL, ApsaraDB RDS provides a download URL for the file. The expiration time of the URL is specified by the **LinkExpiredTime** parameter. You must download the file before the expiration time.
-   This operation returns SQL log entries that are generated over a specified time range. The beginning of the time range must be later than or equal to the time that is specified by the LogEndTime parameter. In addition, the end of the time range must be earlier than or equal to the time that is specified by the LogBeginTime parameter.

**Note:** This operation is not supported for instances that run SQL Server.


## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeBinlogFiles&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeBinlogFiles|The operation that you want to perform. Set the value to **DescribeBinlogFiles**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|EndTime|String|Yes|2011-06-20T15:00:00Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|StartTime|String|Yes|2011-06-01T15:00:00Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values: **30** to **100**. Default value: **30**. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|TotalRecordCount|Integer|100|The total number of log backup files returned. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageRecordCount|Integer|30|The number of log backup files returned on the current page. |
|Items|Array| |An array that consists of log backup files. |
|BinLogFile| | | |
|FileSize|Long|2269410|The size of the log backup file. Unit: bytes. |
|LogBeginTime|String|2019-02-09T17:45:21Z|The start time of the log data recorded in the log backup file. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|LogEndTime|String|2019-02-15T13:10:28Z|The end time of the log data recorded in the log backup file. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|DownloadLink|String|http://rdsxxxxx.oss.aliyuncs.com/xxxxxx|The HTTP-based download URL of the log backup file. If the returned value of this parameter is NULL, ApsaraDB RDS does not provide a download URL for the file. |
|HostInstanceID|String|5841973|The ID of the instance to which the log backup file belongs. This parameter is used to distinguish between the log backup files that are generated on a primary instance and those that are generated on a secondary instance. |
|LinkExpiredTime|String|2013-06-09T18:00:00Z|The expiration time of the download URL. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Checksum|String|18358304393468701857|The checksum. |
|IntranetDownloadLink|String|http://rdslog-hz-v3.oss-cn-hangzhou-internal.aliyuncs.com/xxxxxx|The download URL that is used over an internal network. |
|LogFileName|String|000000040000000000000019|The name of the log backup file. |
|RequestId|String|ED169A3E-1657-4104-82AB-24EA8CD0DB75|The ID of the request. |
|TotalFileSize|Long|2269410|The total size of the log backup files returned. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeBinlogFiles
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2011-06-01T15:00:00Z
&EndTime=2011-06-20T15:00:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeBinlogFilesResponse>
      <Items></Items>
      <PageNumber>1</PageNumber>
      <TotalRecordCount>0</TotalRecordCount>
      <TotalFileSize>0</TotalFileSize>
      <RequestId>ED169A3E-1657-4104-82AB-24EA8CD0DB75</RequestId>
      <PageRecordCount>0</PageRecordCount>
</DescribeBinlogFilesResponse>
```

`JSON` format

```
{
    "Items": {
        "BinLogFile": []
    },
    "PageNumber": 1,
    "TotalRecordCount": 0,
    "TotalFileSize": "0",
    "RequestId": "ED169A3E-1657-4104-82AB-24EA8CD0DB75",
    "PageRecordCount": 0
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

