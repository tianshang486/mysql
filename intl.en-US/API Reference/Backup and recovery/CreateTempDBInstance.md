# CreateTempDBInstance {#doc_api_1105050 .reference}

You can call this operation to create temporary instances.

You can create a temporary instance based on a backup set or a time point within the past seven days.

This operation must meet the following requirements:

-   The instance uses the SQL Server 2012 or 2016 Basic Edition or SQL Server 2008 R2 engine.
-   The instance is in the running state.
-   The instance does not have an ongoing migration task.
-   The last creation of a backup set is completed.

**Note:** When a temporary instance is created, accounts and databases inherit the data in the backup set.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=CreateTempDBInstance) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|CreateTempDBInstance| The operation that you want to perform. Set this parameter to CreateTempDBInstance.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance

 |
|BackupId|Integer|No|603524168| The ID of the backup set.

 **Note:** At least one of the BackupId and RestoreTime parameters is entered.

 |
|RestoreTime|String|No|2011-06-11T16:00:00Z| The specified point in time within the backup retention period. Format: yyyy-MM-ddTHH:mm:ssZ.

 **Note:** 

-   The time can be set to any point in time within the past seven days which is more than 30 minutes earlier than the current time. The default time zone is UTC.
-   At least one of the BackupId and RestoreTime parameters is entered.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|TempDBInstanceId|String|sub138xxxxx\_rm-xxxxx| The ID of the temporary instance.

 |
|RequestId|String|248DE93F-8647-4B9D-8287-4A4A0FE56AD5| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=CreateTempDBInstance
&DBInstanceId=rm-uf6wjk5xxxxxxx
&BackupId=603524168
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_duz_yb5_w65}
<CreateTempDBInstanceResponse>
       <RequestId>248DE93F-8647-4B9D-8287-4A4A0FE56AD5</RequestId>
  <TempDBInstanceId>sub138xxxxx_juxxxxx</TempDBInstanceId>
</CreateTempDBInstanceResponse>
```

`JSON` format

``` {#codeblock_31g_5a0_5eb}
{
	"RequestId":"248DE93F-8647-4B9D-8287-4A4A0FE56AD5",
	"TempDBInstanceId":"sub138xxxxx_juxxxxx"
}
```

## Error codes {#section_auf_en2_tqk .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|OperationDenied.TempDBInstanceExists|The operation is not permitted due to temp instance exist.|The error message returned when the temporary instance already exists.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

