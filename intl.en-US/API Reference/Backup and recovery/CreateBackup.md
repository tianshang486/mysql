# CreateBackup {#doc_api_1084693 .reference}

You can call this operation to create a backup set for an instance.

This operation must meet the following requirements.

-   The instance is in the running state.
-   The instance does not have an ongoing backup task.
-   The number of backup sets that have been created for the instance on the day does not exceed 20.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=CreateBackup) to perform debugging.

OpenAPI Explorer provides various functions to simplify API usage. For example, you can retrieve APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|CreateBackup| The operation that you want to perform. Set this parameter to CreateBackup.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|BackupMethod|String|No|Physical| The backup type. Valid values:

 -   Logical
-   Physical
-   Snapshot

 Default value: Physical.

 **Note:** 

-   Set Physical option when backing up a MariaDB snapshot.
-   Logical backups can be performed only when the instance exists in a database.

 |
|BackupStrategy|String|No|db| The backup policy. Valid values:

 -   db: single-database backups.
-   instance: instance backups.

 **Note:** This parameter can be entered when MySQL logical backups or full physical backups for SQL Server are performed.

 |
|DBName|String|No|rds\_mysql| The list of databases. Separate multiple databases with commas \(,\).

 **Note:** This parameter can be entered when single-database logical backups for MySQL or single-database full physical backups for SQL Server are performed.

 |
|BackupType|String|No|Auto| The backup method. Valid values:

 -   Auto: indicates that full or incremental backups are selected automatically.
-   FullBackup

 Default value: Auto.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|BackupJobId|String|5073731| The ID of the backup task.

 |
|RequestId|String|2C125605-266F-41CA-8AC5-3A643D4F42C5| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=CreateBackup
DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_yqi_o83_zqu}
<CreateBackupResponse>
	  <RequestId>2C125605-266F-41CA-8AC5-3A643D4F42C5</RequestId>
	  <BackupJobId>5073731</BackupJobId></CreateBackupResponse>
```

`JSON` format

``` {#codeblock_b3h_c4g_5zn}
{
	"RequestId":"2C125605-266F-41CA-8AC5-3A643D4F42C5",
	"BackupJobId":"5073731"
}
```

## Error codes {#section_31u_lfh_8ql .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

