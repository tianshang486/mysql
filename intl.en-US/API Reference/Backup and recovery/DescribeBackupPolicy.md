# DescribeBackupPolicy {#doc_api_Rds_DescribeBackupPolicy .reference}

You can call this operation to view the backup settings of instances.

RDS instances are backed up regularly based on your backup settings.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeBackupPolicy) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|DescribeBackupPolicy| The operation that you want to perform. Set this parameter to DescribeBackupPolicy.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|BackupPolicyMode|String|No|DataBackupPolicy| The backup type. Valid values:

 -   DataBackupPolicy
-   LogBackupPolicy

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |
|CompressType|String|No|1| The compression method. Valid values:

 -   0: The backup data is not compressed.
-   1: The backup data is compressed by using zlib.
-   2: The backup data is compressed through multiple threads concurrently by using zlib.
-   4: The backup data is compressed by using QuickLZ and database tables can be restored.
-   8: For MySQL 8.0, the backup data is compressed by using QuickLZ but database tables cannot be restored.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|BackupRetentionPeriod|Integer|7| The retention period of the data backup.

 |
|PreferredBackupTime|String|15:00Z-16:00Z| The data backup time. Format: HH:mmZ-HH:mmZ.

 |
|PreferredBackupPeriod|String|Monday,Wednesday,Friday,Sunday| The data backup period. Separate multiple values with commas \(,\). Valid values:

 -   Monday
-   Tuesday
-   Wednesday
-   Thursday
-   Friday
-   Saturday
-   Sunday

 |
|BackupLog|String|Enable| Indicates whether to enable log backups. Valid values: Enable | Disabled.

 |
|LogBackupRetentionPeriod|Integer|7| The retention period of the log backup.

 |
|Duplication|String|Enable| Indicates whether to dump backup files to OSS. Valid values: Enable | Disabled.

 |
|DuplicationContent|String|DATA&LOG| Indicates whether to dump data backups or log backups to OSS. Valid values:

 -   DATA: Only data backups are dumped.
-   LOG: Only log backups are dumped.
-   DATA&LOG: Both data backups and log backups are dumped.

 **Note:** When the Duplication parameter is set to Enable, this parameter is required.

 |
|DuplicationLocation|N/A|N/A| The storage location of the backup file.

 |
|Location|N/A|N/A| The location information.

 |
|Bucket|String|mybucket| The name of the target OSS bucket.

 |
|Endpoint|String|oss-cn-shanghai.aliyuncs.com| The name of the endpoint.

 |
|Sotrage|String|OSS| The storage media of the backup.

 |
|EnableBackupLog|String|1| Indicates whether to enable log backups. Valid values:

 -   1: indicates that log backups are enabled.
-   0: indicates that log backups are disabled.

 |
|HighSpaceUsageProtection|String|Enable| Indicates whether Binlogs must be deleted when the used space exceeds 80% or the remaining space is less than 5 GB. Valid values:

 -   Disable
-   Enable

 |
|LocalLogRetentionHours|Integer|0| The local retention hours of the log backup.

 |
|LocalLogRetentionSpace|String|30| The maximum space utilization of the local log.

 |
|LogBackupFrequency|String|LogInterval| The log backup frequency. Valid values:

 -   LogInterval: Logs are backed up every 30 minutes.
-   It is the same as the PreferredBackupPeriod value by default.

 **Note:** The LogBackupFrequency parameter is applicable only to SQL Server instances.

 |
|PreferredNextBackupTime|String|2018-01-19T15:15Z| The next backup time. Format: yyyy-MM-ddTHH:mm:ssZ.

 |
|RequestId|String|B87E2AB3-B7C9-4394-9160-7F639F732031| The ID of the request.

 |
|CompressType|String|1| The compression method. Valid values:

 -   0: The backup data is not compressed.
-   1: The backup data is compressed by using zlib.
-   2: The backup data is compressed through multiple threads concurrently by using zlib.
-   4: The backup data is compressed by using QuickLZ and database tables can be restored.
-   8: For MySQL 8.0, the backup data is compressed by using QuickLZ but database tables cannot be restored.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeBackupPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_ebk_dck_jxz}
<DescribeBackupPolicyResponse>
	  <backupLog>Enable</backupLog>
	  <backupRetentionPeriod>7</backupRetentionPeriod>
	  <logBackupRetentionPeriod>7</logBackupRetentionPeriod>
	  <preferredBackupPeriod>Monday,Wednesday,Friday,Sunday</preferredBackupPeriod>
	  <preferredBackupTime>15:00Z-16:00Z</preferredBackupTime>
	  <preferredNextBackupTime>2018-01-19T15:15Z</preferredNextBackupTime>
	  <requestId>B87E2AB3-B7C9-4394-9160-7F639F732031</requestId></DescribeBackupPolicyResponse>
```

`JSON` format

``` {#codeblock_m59_pw2_xr6}
{
	"preferredBackupPeriod":"Monday,Wednesday,Friday,Sunday",
	"requestId":"B87E2AB3-B7C9-4394-9160-7F639F732031",
	"logBackupRetentionPeriod":7,
	"backupRetentionPeriod":7,
	"backupLog":"Enable",
	"preferredNextBackupTime":"2018-01-19T15:15Z",
	"preferredBackupTime":"15:00Z-16:00Z"
}
```

## Error codes {#section_55p_e4n_5qs .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

