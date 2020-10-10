# Delete backup sets

Deletes backup sets of an ApsaraDB for RDS instance.

Only the backup sets of the instance itself are deleted. The backup sets of the associated instances such as read-only, disaster recovery, and clone instances are not deleted.

Before you call this operation, make sure that the following requirements are met:

-   The instance is in the running state.
-   The instance is of the High-availability Edition and runs MySQL, PostgreSQL, or PPAS.
-   If log backups are disabled, RDS instance does not support data restoration by time. You can delete data backup sets which are retained for more than seven days.
-   If log backups are enabled and the retention period of log backups is less than the retention period of data backups, the data backup sets that exceed the retention period of log backups can be deleted.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DeleteBackup&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteBackup|The operation that you want to perform. Set the value to **DeleteBackup**. |
|BackupId|String|Yes|324909958|The ID of the backup set. You can call the [DescribeBackups](~~26273~~) operation to query backup set IDs. Up to 100 IDs can be specified in a single request. Separate multiple IDs with commas \(,\).

**Note:** Only the backup sets whose **StoreStatus** is **Enabled** when you call the [DescribeBackups](~~26273~~) operation can be deleted. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|37441409-FFD1-40AA-8EC5-9ECF5E2F7C29|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DeleteBackup
&DBInstanceId=rm-uf6wjk5xxxxxxx
&BackupId=324909958
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteBackupResponse>
      <RequestId>37441409-FFD1-40AA-8EC5-9ECF5E2F7C29</RequestId>
</DeleteBackupResponse>
```

`JSON` format

```
{
    "RequestId": "37441409-FFD1-40AA-8EC5-9ECF5E2F7C29"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

