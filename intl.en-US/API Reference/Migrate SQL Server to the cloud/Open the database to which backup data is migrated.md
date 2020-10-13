# Open the database to which backup data is migrated

Opens the database to which backup data is migrated on an RDS for SQL Server instance.

This operation is used to migrate backup data to the cloud. Before you call this operation, check [Migrate full backup data to ApsaraDB RDS for SQL Server 2008 R2](~~95737~~), [Migrate full backup data to ApsaraDB RDS for SQL Server 2012, 2014, 2016, 2017, or 2019](~~95738~~), and [Migrate incremental backup data to ApsaraDB RDS for SQL Server 2012, 2014, 2016, 2017, or 2019](~~95736~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=CreateOnlineDatabaseTask&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateOnlineDatabaseTask|The operation that you want to perform. Set the value to **CreateOnlineDatabaseTask**. |
|CheckDBMode|String|Yes|AsyncExecuteDBCheck|The consistency check method after the database is open. Valid values:

 -   **SyncExecuteDBCheck**: synchronous database check
-   **AsyncExecuteDBCheck**: asynchronous database check

 **Note:** The check methods are supported for RDS instances that run SQL Server 2008 R2. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|DBName|String|Yes|testDB|The name of the database. |
|MigrateTaskId|String|Yes|5652255443|The ID of the migration task. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxx|The client token that is used to ensure the idempotency of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1B2EBD14-36F6-4645-A3F9-DE19D321C18F|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=CreateOnlineDatabaseTask
&DBInstanceId=rm-uf6wjk5xxxxxxx
&DBName=testDB
&MigrateTaskId=5652255443
&CheckDBMode=AsyncExecuteDBCheck
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateOnlineDatabaseTaskResponse>
	  <code>200</code>
	  <data>
		    <RequestId>1B2EBD14-36F6-4645-A3F9-DE19D321C18F</RequestId>
	  </data>
	  <requestId>1B2EBD14-36F6-4645-A3F9-DE19D321C18F</requestId>
	  <successResponse>true</successResponse>
</CreateOnlineDatabaseTaskResponse>
```

`JSON` format

```
{
    "code": "200", 
    "data": {
        "RequestId": "1B2EBD14-36F6-4645-A3F9-DE19D321C18F"
    }, 
    "requestId": "1B2EBD14-36F6-4645-A3F9-DE19D321C18F", 
    "successResponse": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

