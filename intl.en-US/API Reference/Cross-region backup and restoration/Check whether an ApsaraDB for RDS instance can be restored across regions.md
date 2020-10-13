# Check whether an ApsaraDB for RDS instance can be restored across regions

Checks whether an ApsaraDB for RDS instance can be restored across regions by using a data backup set in another region.

Before you call this operation, make sure that the instances is running one of the following database engine versions and RDS editions:

-   MySQL 8.0 in the High-availability Edition \(with local SSDs\)
-   MySQL 5.7 in the High-availability Edition \(with local SSDs\)
-   MySQL 5.6

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=CheckCreateDdrDBInstance&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CheckCreateDdrDBInstance|The operation that you want to perform. Set the value to **CheckCreateDdrDBInstance**. |
|DBInstanceClass|String|Yes|rds.mysql.s1.small|The type of the destination instance. For more information, see [Instance types](~~26312~~). |
|DBInstanceStorage|Integer|Yes|20|The storage space of the destination instance. Valid values: **5 to 2000**.

 The value must be a multiple of 5 GB. Unit: GB. For more information, see [Instance types](~~26312~~). |
|Engine|String|Yes|MySQL|The database engine of the destination instance. Valid values: **MySQL**.

 **Note:** Currently, only MySQL is supported for cross-region backup. |
|EngineVersion|String|Yes|5.6|The database engine version of the destination instance. Valid values:

 -   **8.0**
-   **5.7**
-   **5.6** |
|RegionId|String|Yes|cn-hangzhou|The region ID of the destination instance. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|RestoreType|String|Yes|0|The restoration method of the instance. Valid values:

 -   **0**: restores the instance by using a backup set. You must also specify the **BackupSetId** parameter.
-   **1**: restores the instance to a specific point in time. You must also specify the **RestoreTime**, **SourceRegion**, **SourceDBInstanceName** parameters.

 Default value: **0**. |
|BackupSetId|String|No|14358|The ID of the backup set used for restoration. You can call the [DescribeCrossRegionBackups](~~121733~~) operation to query backup set IDs.

 **Note:** When the **RestoreType** parameter is set to **0**, this parameter is required. |
|RestoreTime|String|No|2019-05-30T03:29:10Z|The point in time to which you want to restore the instance. The value must be earlier than the current time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

 **Note:** When the **RestoreType** parameter is set to **1**, this parameter is required. |
|SourceRegion|String|No|cn-hangzhou|The region ID of the instance which you want to restore to a specific point in time.

 **Note:** When the **RestoreType** parameter is set to **1**, this parameter is required. |
|SourceDBInstanceName|String|No|rm-uf6wjk5xxxxxxx|The ID of the instance which you want to restore to a specific point in time.

 **Note:** When the **RestoreType** parameter is set to **1**, this parameter is required. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsValid|String|true|Indicates whether the instance can be restored across regions. Valid values:**true and false** |
|RequestId|String|1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=CheckCreateDdrDBInstance
&RegionId=cn-hangzhou
&Engine=MySQL
&DBInstanceClass=rds.mysql.s1.small
&DBInstanceStorage=20
&EngineVersion=5.6
&RestoreType=0
&BackupSetId=14358
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CheckCreateDdrDBInstanceResponse>
    <IsValid>true</IsValid>
    <RequestId>346C62D7-8BB9-4516-93E7-25A469EAABCB</RequestId>
</CheckCreateDdrDBInstanceResponse>
```

`JSON` format

```
{
	"IsValid": "true",
	"RequestId": "346C62D7-8BB9-4516-93E7-25A469EAABCB"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|400|IncorrectDBInstanceType|Current DB instance engine and type does not support operations.|The error message returned because the database engine and type of the instance do not support this operation.|
|400|InvalidRestoreType.Format|Specified restore type is not valid.|The error message returned because the specified restoration method is invalid.|
|400|InvalidBackupType.Format|Specified backup type is not valid.|The error message returned because the specified backup type is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

