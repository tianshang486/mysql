# Query migration tasks

Queries tasks to migrate backup data to an ApsaraDB for RDS instance that runs SQL Server.

You can call this operation to query backup data migration tasks of the instance within the last week.

**Note:**

-   Only full backup data files can be migrated.
-   If the instance runs SQL Server 2017 EE, this operation is not supported.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeMigrateTasks&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeMigrateTasks|The operation that you want to perform. Set the value to **DescribeMigrateTasks**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|EndTime|String|Yes|2017-10-25T01:00Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|StartTime|String|Yes|2017-10-20T01:00Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values: **30** to **100**. Default value: **30**. |
|PageNumber|Integer|No|1|The number of the page to return. Valid values: a non-zero positive integer.

Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|Items|Array| |An array that consists of backup data migration tasks. |
|MigrateTask| | | |
|BackupMode|String|FULL|The type of the migration task. Valid values:

-   **FULL**: indicates that full backup files are used to restore data.
-   **UPDF**: indicates that incremental files or log files are used to restore incremental data. |
|CreateTime|String|2017-05-30T12:11:04Z|The time when the migration task was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|DBName|String|testDB|The name of the database. |
|Description|String|Api description|The description of the migration task. |
|EndTime|String|2017-05-30T13:11:04Z|The time when the backup data migration task was complete. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|IsDBReplaced|String|True|Indicates whether the imported data overwrites the existing data. |
|MigrateTaskId|String|564522545|The ID of the migration task. |
|Status|String|Success|The status of the migration task. Valid values:

-   **NoStart:** The task is not started.
-   **Running:** The task is in progress.
-   **Success:** The task is successful.
-   **Failed:** The task failed.
-   **Waiting:** The task is waiting for the incremental backup data file to be imported. |
|PageRecordCount|Integer|10|The number of entries returned per page. |
|PageNumber|Integer|1|The page number of the returned page. |
|RequestId|String|4E356DDF-6B83-45DB-99D5-4B1E8A0D286B|The ID of the request. |
|TotalRecordCount|Integer|30|The total number of entries. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeMigrateTasks
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2017-10-20T01:00Z
&EndTime=2017-10-25T01:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeMigrateTasksResponse>
      <RequestId>A5409D02-D661-4BF3-8F3D-0A814D0574E7</RequestId>
      <PageRecordCount>1</PageRecordCount>
      <PageNumber>1</PageNumber>
      <TotalRecordCount>10</TotalRecordCount>
      <Items>
            <MigrateTaskId>rm-bp1842vxxxxx</MigrateTaskId>
            <DBName>test02</DBName>
            <CreateTime>2017-05-30 T12:11:4Z</CreateTime>
            <EndTime>2017-05-30 T12:11:4Z</EndTime>
            <IsDBReplaced>True</IsDBReplaced>
            <Status>Success</Status>
            <BackupMode>FULL</BackupMode>
            <Description>Api description</Description>
      </Items>
</DescribeMigrateTasksResponse>
```

`JSON` format

```
{
    "RequestId": "A5409D02-D661-4BF3-8F3D-0A814D0574E7",
    "PageRecordCount": 1,
    "PageNumber": 1,
    "TotalRecordCount": 10,
    "Items": {
        "MigrateTaskId": "rm-bp1842vxxxxx",
        "DBName": "test02",
        "CreateTime": "2017-05-30 T12:11:4Z",
        "EndTime": "2017-05-30 T12:11:4Z",
        "IsDBReplaced": "True",
        "Status": "Success",
        "BackupMode": "FULL",
        "Description": "Api description"
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

