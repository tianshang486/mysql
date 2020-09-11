# Create backup set

Creates a backup set for an ApsaraDB for RDS instance.

Before you call this operation, make sure that the following requirements are met:

-   The instance is in the Running state.
-   The instance does not have an ongoing backup task.
-   The maximum number of backup sets allowed on the instance is not reached. Up to 20 backup sets can be created for a single instance within a day.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=CreateBackup&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateBackup|The operation that you want to perform. Set the value to **CreateBackup**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|DBName|String|No|rds\_mysql|The databases that you want to back up. Separate them with commas \(,\).

**Note:** You can specify this parameter when you perform a logical backup on individual databases of an RDS for MySQL instance or when you perform a full physical backup on individual databases of an RDS for SQL Server instance. |
|BackupStrategy|String|No|db|The policy to use for backup. Valid values:

-   **db:** specifies to perform a database-level backup.
-   **instance:** specifies to perform an instance-level backup.

**Note:** You can specify this parameter when you perform a logical backup on an RDS for MySQL instance or when you perform a full physical backup on an RDS for SQL Server instance. |
|BackupMethod|String|No|Physical|The type of backup to perform. Valid values:

-   **Logical:** specifies to perform a logical backup.
-   **Physical:** specifies to perform a physical backup.
-   **Snapshot:** specifies to perform a snapshot backup.

Default value: **Physical**.

**Note:**

-   You can perform a logical backup only when databases are created on the instance.
-   You must set this parameter to **Physical** when you perform a snapshot backup on an RDS for MariaDB instance.
-   For more information about the backup types that are supported by the instance, see [Back up an ApsaraDB RDS MySQL instance](~~98818~~). |
|BackupType|String|No|Auto|The method to use for backup. Valid values:

-   **Auto:** specifies to automatically perform a full or incremental backup.
-   **FullBackup:** specifies to perform a full backup.

Default value: **Auto**.

**Note:** This parameter must be specified only when the instance is running SQL Server. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|2C125605-266F-41CA-8AC5-3A643D4F42C5|The ID of the request. |
|BackupJobId|String|5073731|The ID of the backup task. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=CreateBackup
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateBackupResponse>
      <RequestId>2C125605-266F-41CA-8AC5-3A643D4F42C5</RequestId>
      <BackupJobId>5073731</BackupJobId>
</CreateBackupResponse>
```

`JSON` format

```
{
    "RequestId": "2C125605-266F-41CA-8AC5-3A643D4F42C5", 
    "BackupJobId": "5073731"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

