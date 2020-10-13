# Create a migration task

Creates a migration task to restore backup files from an Object Storage Service \(OSS\) bucket to an ApsaraDB RDS for SQL Server instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=CreateMigrateTask&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateMigrateTask|The operation that you want to perform. Set the value to **CreateMigrateTask**. |
|BackupMode|String|Yes|FULL|The type of the migration task. Valid values:

 -   **FULL**: specifies that full backup files are used to restore data.
-   **UPDF**: specifies that incremental backup files or log files are used to restore incremental data. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|DBName|String|Yes|testDB|The name of the database that you want to restore. |
|IsOnlineDB|String|Yes|True|Specifies whether to bring the restored database online for user access. Valid values:

 -   **True**
-   **False**

 **Note:** The value for SQL Server 2008 R2 is fixed to **True**. |
|CheckDBMode|String|No|AsyncExecuteDBCheck|The consistency check method of the database. Valid values:

 -   **SyncExecuteDBCheck**: synchronous database check
-   **AsyncExecuteDBCheck**: asynchronous database check

 Default value: **AsyncExecuteDBCheck** \(compatible with SQL Server 2008 R2\).

 **Note:** When **IsOnlineDB** is set to **True**, this value is valid. |
|OssObjectPositions|String|No|oss-ap-southeast-1.aliyuncs.com:rdsmssqlsingapore:autotest\_2008R2\_TestMigration\_FULL.bak|The information of the backup file in the OSS bucket.

 The values consist of three parts that are separated by colons \(:\):

 -   The endpoint of the OSS bucket: oss-ap-southeast-1.aliyuncs.com.
-   The name of the OSS bucket: rdsmssqlsingapore.
-   The key of the backup file in the OSS bucket: autotest\_2008R2\_TestMigration\_FULL.bak.

 **Note:**

-   This parameter is optional for instances that run SQL Server 2008 R2.
-   This parameter is required for instances that run a database engine later than SQL Server 2008 R2. |
|OSSUrls|String|No|check\_cdn\_oss.sh www.xxxxxx.mobi|The shared URL of the backup file in the OSS bucket. The URL must be encoded.

 If you specify multiple URLs, separate them with vertical bars \(\|\) and then encode them.

 **Note:** This parameter must be entered for instances that run SQL Server 2008 R2. |
|MigrateTaskId|String|No|None|The ID of the migration task. Valid values:

 -   When **BackupMode** is set to **FULL**, this value is empty \(compatible with RDS for SQL Server 2008 R2\).
-   When **BackupMode** is set to **UPDF**, this value is the ID of the required full migration task.

 Default value: FULL.

 **Note:**

-   When **IsOnlineDB** is set to **True**, **BackupMode** must be set to **FULL**.
-   When **IsOnlineDB** is set to **False**, **BackupMode** must be set to **UPDF**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|BackupMode|String|FULL|The type of the migration task. Valid values:

 -   **FULL**: indicates that full backup files are used to restore data.
-   **UPDF**: indicates that incremental backup files or log files are used to restore incremental data. |
|DBInstanceId|String|rm-uf6wjk5xxxxx|The ID of the instance. |
|DBName|String|test02|The name of the database. |
|MigrateTaskId|String|564563256|The ID of the migration task. |
|RequestId|String|866F5EB8-4650-4061-87F0-379F6F968BCE|The ID of the request. |
|TaskId|String|5451225|The ID of the task. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=CreateMigrateTask
&DBInstanceId=rm-uf6wjk5xxxxxxx
&DBName=testDB
&BackupMode=FULL
&IsOnlineDB=True
&OssObjectPositions=oss-ap-southeast-1.aliyuncs.com:rdsmssqlsingapore:autotest_2008R2_TestMigration_FULL.bak
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateMigrateTaskResponse>
	  <MigrateTaskId>135847</MigrateTaskId>
	  <DBInstanceId>rm-bp178grbxxxxxxx</DBInstanceId>
	  <RequestId>5F2B3757-BD56-40B3-B5F2-FCDD9FA0E2E2</RequestId>
	  <BackupMode>UPDF</BackupMode>
	  <TaskId>128301751</TaskId>
	  <DBName>test02</DBName>
</CreateMigrateTaskResponse>
```

`JSON` format

```
{
	"MigrateTaskId": "135847",
	"DBInstanceId": "rm-bp178grbxxxxxxx",
	"RequestId": "5F2B3757-BD56-40B3-B5F2-FCDD9FA0E2E2",
	"BackupMode": "UPDF",
	"TaskId": "128301751",
	"DBName": "test02"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|400|InvalidDBName|The instance does not have the specified DB name.|The error message returned when the specified database name does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

