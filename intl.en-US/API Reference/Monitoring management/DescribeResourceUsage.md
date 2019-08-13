# DescribeResourceUsage {#doc_api_1106158 .reference}

You can call this operation to view the space occupied by an instance.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeResourceUsage) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|DescribeResourceUsage| The operation that you want to perform. Set this parameter to DescribeResourceUsage.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx| The name of the instance.

 |
|Engine|String|MySQL| The type of the database.

 |
|DiskUsed|Long|2337275904| The total space occupied by both data files and log files. Unit: byte. The value -1 indicates no data.

 |
|DataSize|Long|2337275904| The total space occupied by data files. Unit: byte. The value -1 indicates no data.

 |
|LogSize|Long|2337275904| The total space occupied by log files. Unit: byte. The value -1 indicates no data.

 |
|BackupSize|Long|53002759| The total space occupied by backup data. Unit: byte. The value -1 indicates no data.

 |
|ColdBackupSize|Long|2337275904| The total space occupied by cold backup data. Unit: byte. The value -1 indicates no data.

 |
|SQLSize|Long|315052751| The total space occupied by SQL data. Unit: byte. The value -1 indicates no data.

 |
|BackupOssDataSize|Long|8821760| The size of data files in the OSS backup sets. Unit: byte. The value 0 indicates no data.

 |
|BackupOssLogSize|Long|44180999| The size of log files in the OSS backup sets. Unit: byte. The value 0 indicates no data.

 |
|RequestId|String|A88722B7-DAEE-4822-BA8B-9B019FCB8D46| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeResourceUsage
&DBInstanceId=rm-uf6wjk5xxxxxxx 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_9jo_7k1_uyu}
<DescribeResourceUsageResponse>
	  <BackupOssDataSize>8821760</BackupOssDataSize>
	  <BackupOssLogSize>44180999</BackupOssLogSize>
	  <RequestId>A88722B7-DAEE-4822-BA8B-9B019FCB8D46</RequestId>
	  <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
	  <DataSize>2337275904</DataSize>
	  <LogSize>-1</LogSize>
	  <BackupSize>53002759</BackupSize>
	  <SQLSize>315052751</SQLSize>
	  <ColdBackupSize>-1</ColdBackupSize>
	  <Engine>MySQL</Engine>
	  <DiskUsed>2337275904</DiskUsed></DescribeResourceUsageResponse>
```

`JSON` format

``` {#codeblock_jr3_6iy_zdh}
{
	"BackupOssLogSize":"44180999",
	"BackupOssDataSize":"8821760",
	"DBInstanceId":"rm-uf6wjk5xxxxxxx",
	"RequestId":"A88722B7-DAEE-4822-BA8B-9B019FCB8D46",
	"LogSize":-1,
	"DataSize":2337275904,
	"ColdBackupSize":-1,
	"SQLSize":315052751,
	"BackupSize":53002759,
	"Engine":"MySQL",
	"DiskUsed":2337275904
}
```

## Error codes { .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

