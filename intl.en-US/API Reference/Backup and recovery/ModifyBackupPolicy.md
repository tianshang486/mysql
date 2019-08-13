# ModifyBackupPolicy {#doc_api_1105047 .reference}

You can call this operation to modify the backup settings of an RDS instance.

This operation must meet the following requirements:

-   The instance cannot be a read-only instance.
-   The instance is in the running state.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifyBackupPolicy) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|ModifyBackupPolicy| The operation that you want to perform. Set this parameter to ModifyBackupPolicy.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|BackupPolicyMode|String|No|DataBackupPolicy| The type of the backup. Valid values:

 -   DataBackupPolicy
-   LogBackupPolicy

 |
|PreferredBackupTime|String|No|00:00Z-01:00Z| The time when the backup task is performed. Format: yyyy-MM-ddZ-HH:mm:ssZ.

 **Note:** When the BackupPolicyMode parameter is set to DataBackupPolicy, this parameter is required.

 |
|PreferredBackupPeriod|String|No|Monday| The backup period. Separate multiple values with commas \(,\). The default value is the original value. Valid values:

 -   Monday
-   Tuesday
-   Wednesday
-   Thursday
-   Friday
-   Saturday
-   Sunday

 **Note:** When the BackupPolicyMode parameter is set to DataBackupPolicy, this parameter is required.

 |
|BackupRetentionPeriod|String|No|7| The retention period of the data backup. Value range: 7 to 730. The default value is the original value.

 **Note:** When the BackupPolicyMode parameter is set to LogBackupPolicy, this parameter is required.

 |
|BackupLog|String|No|Enable| Indicates whether to enable log backups. Valid values: Enable | Disabled. The default value is the original value.

 **Note:** When the BackupPolicyMode parameter is set to DataBackupPolicy, this parameter can be used to enable or disable log backups.

 |
|LogBackupRetentionPeriod|String|No|7| The retention period of the log backup. Value range: 7 to 730. It cannot be greater than the retention period of the data backup.

 **Note:** When you enable log backups, you can set the retention period of log backup files. This operation is applicable only to the following instances: MySQL, PostgreSQL, and PPAS.

 |
|EnableBackupLog|String|No|True| Indicates whether to enable log backups. Valid values: True | False.

 **Note:** When the BackupPolicyMode parameter is set to LogBackupPolicy, this parameter can be used to enable or disable log backups.

 |
|LocalLogRetentionHours|String|No|18| The local retention hours of the log backup. Value range: \(0 to 7\)\*24. The value 0 indicates that log backups are not retained locally. The default value is the original value.

 **Note:** When the BackupPolicyMode parameter is set to LogBackupPolicy, this parameter is required.

 |
|LocalLogRetentionSpace|String|No|30| The maximum cycle space utilization of the local log. If the maximum value of this parameter is exceeded, you can start to delete the first Binlog until the space utilization is less than this ratio. Value range: 0 to 50. The default value is the original value.

 **Note:** When the BackupPolicyMode parameter is set to BackupPolicyMode, this parameter is required.

 |
|HighSpaceUsageProtection|String|No|Enable| Indicates whether to delete Binlogs unconditionally when the used space exceeds 80% or the remaining space is less than 5 GB. Valid values: Enable | Disable. The default value is the original value.

 **Note:** When the BackupPolicyMode parameter is set to LogBackupPolicy, this parameter is required.

 |
|Duplication|String|No|Disable| Indicates whether to dump backup files to OSS. Valid values: Enable | Disable.

 |
|DuplicationContent|String|No|DATA| Indicates whether to dump data backups or log backups to OSS. Valid values:

 -   DATA: Only data backups are dumped.
-   LOG: Only log backups are dumped.
-   DATA&LOG: Both data backups and log backups are dumped.

 **Note:** When the Duplication parameter is set to Enable, this parameter is required.

 |
|DuplicationLocation|String|No|\{"Storage":"OSS","Location": \{"Bucket": 'xxx', "Location":'cn-hangzhou',"OSSEndPoint":"oss-test","Object":"obje1"\}| Indicates whether RAM can authorize RDS to access your OSS. The log files can be dumped to OSS only after authorization. Format:

 \{"Storage":"OSS","Location": \{"Bucket": 'xxx', "Location":'cn-hangzhou',"OSSEndPoint":"oss-test","Object":"obje1"\}

 **Note:** When the Duplication parameter is set to Enable, this parameter is required.

 |
|LogBackupFrequency|String|No|LogInterval| The log backup frequency. Valid values:

 -   LogInterval: Logs are backed up every 30 minutes.
-   It is the same as the data backup frequency by default.

 **Note:** The LogInterval parameter is applicable only to SQL Server instances.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |
|CompressType|String|No|4| The compression method. This parameter is valid only when you change the compression method to QuickLZ for an RDS MySQL 5.6 instance. The backup data can be used to restore database tables. Value: 4.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CompressType|String|4| The compression method. Valid values:

 -   0: The backup data is not compressed.
-   1: The backup data is compressed by using zlib.
-   2: The backup data is compressed through multiple threads concurrently by using zlib.
-   4: The backup data is compressed by using QuickLZ and database tables can be restored.
-   8: For MySQL 8.0, the backup data is compressed by using QuickLZ but database tables cannot be restored.

 |
|DBInstanceID|String|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|EnableBackupLog|String|False| Indicates whether to enable log backups.

 |
|HighSpaceUsageProtection|String|Disable| Indicates whether to delete Binlogs unconditionally when the used space exceeds 80% or the remaining space is less than 5 GB.

 |
|LocalLogRetentionHours|Integer|18| The local retention hours of the log backup.

 |
|LocalLogRetentionSpace|String|30| The maximum cycle space utilization of the local log.

 |
|RequestId|String|DA147739-AEAD-4417-9089-65E9B1D8240D| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? &Action= ModifyBackupPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxx
&BackupPolicyMode=LogBackupPolicy
&EnableBackupLog=True
&HighSpaceUsageProtection=Enable 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_hbx_15q_dnq}
<ModifyBackupPolicyResponse>
        <HighSpaceUsageProtection>Disable</HighSpaceUsageProtection>
	  <DBInstanceID>rm-bp1z3xxxxx</DBInstanceID>
	  <RequestId>E4BF5598-ED12-4406-AAA4-F375428BE741</RequestId>
	  <LocalLogRetentionHours>18</LocalLogRetentionHours>
	  <EnableBackupLog>1</EnableBackupLog>
	  <LocalLogRetentionSpace>30</LocalLogRetentionSpace>
</ModifyBackupPolicyResponse>
```

`JSON` format

``` {#codeblock_k4n_4xn_af8}
{
	"HighSpaceUsageProtection":"Disable",
	"DBInstanceID":"rm-bp1z3xxxxx",
	"RequestId":"E4BF5598-ED12-4406-AAA4-F375428BE741",
	"EnableBackupLog":"1",
	"LocalLogRetentionHours":"18",
	"LocalLogRetentionSpace":"30"
}
```

## Error codes {#section_ys1_5fn_5i6 .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

