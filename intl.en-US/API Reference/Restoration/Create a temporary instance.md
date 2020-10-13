# Create a temporary instance

Creates a temporary instance.

You can create a temporary instance based on a backup set or a time within the past seven days.

Before you call this operation, make sure that the following requirements are met:

-   The instance runs SQL Server 2012 or 2016 in the Basic Edition or SQL Server 2008 R2.
-   The instance is in the running state.
-   The instance does not have ongoing migration tasks.
-   The last creation of a backup set is completed.

**Note:** After a temporary instance is created, accounts and databases inherit data in the backup set.


## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=CreateTempDBInstance&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateTempDBInstance|The operation that you want to perform. Set the value to **CreateTempDBInstance**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|BackupId|Integer|No|603524168|The ID of the backup set.

 **Note:** You must specify the **BackupId** or **RestoreTime** parameter. |
|RestoreTime|String|No|2011-06-11T16:00:00Z|The specified point in time within the backup retention period. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

 **Note:**

-   The time can be set to a point in time within the past seven days and must be more than 30 minutes earlier than the current time. The default time zone is UTC.
-   You must specify the **BackupId** or **RestoreTime** parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|TempDBInstanceId|String|sub138xxxxx\_rm-xxxxx|The ID of the temporary instance. |
|RequestId|String|248DE93F-8647-4B9D-8287-4A4A0FE56AD5|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=CreateTempDBInstance
&DBInstanceId=rm-uf6wjk5xxxxxxx
&BackupId=603524168
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateTempDBInstanceResponse>
       <RequestId>248DE93F-8647-4B9D-8287-4A4A0FE56AD5</RequestId>
  <TempDBInstanceId>sub138xxxxx_juxxxxx</TempDBInstanceId>
</CreateTempDBInstanceResponse>
```

`JSON` format

```
{
    "RequestId": "248DE93F-8647-4B9D-8287-4A4A0FE56AD5",
    "TempDBInstanceId": "sub138xxxxx_juxxxxx"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|OperationDenied.TempDBInstanceExists|The operation is not permitted due to temp instance exist.|This message returned because the temporary instance already exists.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

