# Query storage usage

You can call the DescribeResourceUsage operation to query the storage usage of an ApsaraDB RDS instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeResourceUsage&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeResourceUsage|The operation that you want to perform. Set the value to **DescribeResourceUsage**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|Engine|String|MySQL|The database engine that the instance runs. |
|DiskUsed|Long|2337275904|The storage space that is occupied by data and log files on the instance. Unit: bytes. The value -1 indicates that no data or log files are stored on the instance. |
|DataSize|Long|1292094741|The storage space that is occupied by data files on the instance. Unit: bytes. The value -1 indicates that no data files are stored on the instance. |
|LogSize|Long|1045181163|The storage space that is occupied by log files on the instance. Unit: bytes. The value -1 indicates that no log files are stored on the instance. |
|BackupSize|Long|53002759|The storage space that is occupied by backup files on the instance. Unit: bytes. The value -1 indicates that no backup files are stored on the instance. |
|ColdBackupSize|Long|2337275904|The storage space that is occupied by cold backup files on the instance. Unit: bytes. The value -1 indicates that no cold backup files are stored on the instance. |
|SQLSize|Long|315052751|The storage space that is occupied by SQL data on the instance. Unit: bytes. The value -1 indicates that no SQL data is stored on the instance. |
|ArchiveBackupSize|Long|0|The storage space that is occupied by archived backup files on the instance. Unit: bytes. |
|BackupDataSize|Long|94324736|The storage space that is occupied by data backup files \(excluding archived data backup files\) on the instance. Unit: bytes. |
|BackupLogSize|Long|45145563|The storage space that is occupied by log backup files \(excluding archived log backup files\) on the instance. Unit: bytes. |
|BackupOssDataSize|Long|8821760|The size of data backup files that are stored in OSS buckets. Unit: bytes. The value 0 indicates no data backup files are stored in OSS buckets. |
|BackupOssLogSize|Long|44180999|The size of log backup files that are stored in OSS buckets. Unit: bytes. The value 0 indicates no log backup files are stored in OSS buckets. |
|PaidBackupSize|Long|0|The backup storage for which you must pay. ApsaraDB RDS provides a free quota for backup storage. You must pay for the backup storage that exceeds the free quota. Unit: bytes. |
|RequestId|String|F937E173-559C-4498-8D90-38D32342B9E4|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeResourceUsage
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeResourceUsageResponse>
  <PaidBackupSize>0</PaidBackupSize>
  <RequestId>28E73580-103C-4925-A48D-9A7E25F24297</RequestId>
  <BackupSize>51305057407</BackupSize>
  <ArchiveBackupSize>0</ArchiveBackupSize>
  <ColdBackupSize>-1</ColdBackupSize>
  <LogSize>2097152</LogSize>
  <BackupOssLogSize>48565375</BackupOssLogSize>
  <DBInstanceId> rm-uf6wjk5xxxxxxx</DBInstanceId>
  <BackupDataSize>51256492032</BackupDataSize>
  <DataSize>3198156800</DataSize>
  <BackupLogSize>48565375</BackupLogSize>
  <BackupOssDataSize>0</BackupOssDataSize>
  <SQLSize>446228522</SQLSize>
  <DiskUsed>3200253952</DiskUsed>
  <Engine>MySQL</Engine>
</DescribeResourceUsageResponse>
```

`JSON` format

```
{
	"PaidBackupSize": 0,
	"RequestId": "28E73580-103C-4925-A48D-9A7E25F24297",
	"BackupSize": 51305057407,
	"ArchiveBackupSize": 0,
	"ColdBackupSize": -1,
	"LogSize": 2097152,
	"BackupOssLogSize": "48565375",
	"DBInstanceId": " rm-uf6wjk5xxxxxxx",
	"BackupDataSize": 51256492032,
	"DataSize": 3198156800,
	"BackupLogSize": 48565375,
	"BackupOssDataSize": "0",
	"SQLSize": 446228522,
	"DiskUsed": 3200253952,
	"Engine": "MySQL"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

