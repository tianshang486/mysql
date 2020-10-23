# Restore individual databases or tables

You can call the RestoreTable operation to restore individual databases or tables of an ApsaraDB for RDS instance.

ApsaraDB RDS for MySQL supports the restoration of individual databases and tables. If you accidentally delete databases or tables from an instance, you can restore the databases or tables by using a backup file. For more information, see [Restore individual databases and tables of an ApsaraDB RDS for MySQL instance](~~103175~~).

Before you call this operation, make sure that the following requirements are met:

-   The instance must run MySQL 5.7 on RDS High-availability Edition with local SSDs or run MySQL 5.6 on RDS High-availability Edition.
-   The instance must be in the Running state.
-   The instance cannot have ongoing migration tasks.
-   If you want to restore data to a specific point in time, the log backup function must be enabled for the instance. For more information, see [Back up an ApsaraDB RDS for MySQL instance](~~98818~~).
-   The restoration of individual databases and tables is enabled, and new backups are created. For more information, see [Restore individual databases and tables of an ApsaraDB RDS for MySQL instance](~~103175~~).
-   The names that you want to use for the restored tables cannot exist on the instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=RestoreTable&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RestoreTable|The operation that you want to perform. Set the value to **RestoreTable**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx|The ID of the instance. |
|TableMeta|String|Yes|\[\{"type":"db","name":"testdb1","newname":"testdb1\_new","tables":\[\{"type":"table","name":"testdb1table1","newname":"testdb1table1\_new"\}\]\}\]|The databases and tables that you want to restore. Format:

```
[{"type":"db","name":"<The name of the original database 1>","newname":"<The name of the new database 1>","tables":[{"type":"table","name":"<The name of the original table 1 in the original database 1>","newname":"<The name of the new table 1 in the new database 1>"},{"type":"table","name":"<The name of the original table 2 in the original database 1>","newname":"<The name of the new table 2 in the new database 1>"}]},{"type":"db","name":"<The name of the original database 2>","newname":"<The name of the new database 2>","tables":[{"type":"table","name":"<The name of the original table 3 in the original database 2>","newname":"<The name of the new table 3 in the new database 2>"},{"type":"table","name":"<The name of the original table 4 in the original database 2>","newname":"<The name of the new table 4 in the new database 2>"}]}]
``` |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|BackupId|String|No|9026262|The ID of the backup set that you want to use.

You can call the [DescribeBackups](~~26273~~) operation to obtain the most recent backup set list.

**Note:** You must specify at least one of the **BackupId** and **RestoreTime** parameters. |
|RestoreTime|String|No|2011-06-11T16:00:00Z|The point in time to which you want to restore data. The point in time must fall within the specified log backup retention period. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

**Note:**

-   You must specify at least one of the **BackupId** and **RestoreTime** parameters.
-   You must enable the log backup function. For more information, see [Back up an ApsaraDB RDS for MySQL instance](~~98818~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|EA2D4F34-01A7-46EB-A339-D80882135206|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=RestoreTable
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&RestoreTime=2019-08-20T16:00:00Z
&TableMeta=[{"type":"db","name":"dtstestdata","newname":"dtstestdata","tables":[{"type":"table","name":"customer_old","newname":"customer_old123"},{"type":"table","name":"order","newname":"order123"}]}]
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RestoreTableResponse>
  <RequestId>EA2D4F34-01A7-46EB-A339-D80882135206</RequestId>
</RestoreTableResponse>
```

`JSON` format

```
{
    "RequestId": "EA2D4F34-01A7-46EB-A339-D80882135206"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidRestoreType.Format|Specified restore type is not valid.|The error message returned because the specified restoration type is invalid.|
|400|InvalidRestoreTime.Format|Specified restore time is not valid.|The error message returned because the specified RestoreTime is invalid.|
|404|InvalidBackup.NotFound|The available backup does not exist in recovery time.|The error message returned because no backup sets are available.|
|404|InvalidBackupSetID.NotFound|Specified backup set ID does not exist.|The error message returned because the specified BackupId is invalid.|
|403|IncorrectBackupSetState|Current backup set state does not support operations.|The error message returned because this operation is not supported due to the status of the specified backup set.|
|400|InvalidDBName.Duplicate|Specified DB name already exists in the This instance.|The error message returned because the specified new name of a database already exists on the instance.|
|403|ChildDBInstanceExists|Current DB instance had child instance.|The error message returned because the instance is attached with other instances.|
|400|InvalidParameters.Format|Specified parameters is not valid.|The error message returned because a specified parameter is invalid.|
|404|InsufficientResourceCapacity|There is insufficient capacity available for the requested instance.|The error message returned because the available resources are insufficient. Please try again later.|
|400|MissingUserID|The request is missing a user\_id parameter.|The error message returned because the specified channel does not exist.|
|400|MissingUID|The request is missing a uid parameter.|The error message returned because the specified account does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

