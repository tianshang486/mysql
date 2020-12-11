# Query backup settings

You can call the DescribeBackupPolicy operation to query the backup settings of an ApsaraDB RDS instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeBackupPolicy&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeBackupPolicy|The operation that you want to perform. Set the value to **DescribeBackupPolicy**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|BackupPolicyMode|String|No|DataBackupPolicy|The type of backup policy to query. Valid values:

-   **DataBackupPolicy:** specifies to query the data backup settings.
-   **LogBackupPolicy:** specifies to query the log backup settings. |
|CompressType|String|No|1|The format that is used to compress backups. Valid values:

-   **0:** specifies not to compress backups.
-   **1:** specifies to compress backups by using zlib.
-   **2:** specifies to compress backups by using zlib that invokes multiple threads in parallel for each backup.
-   **4:** specifies to compress backups by using QuickLZ. These backups can be used to restore individual databases and tables.
-   **8:** specifies to compress backups by using QuickLZ if the instance runs MySQL 8.0. These backups cannot be used to restore individual databases or tables. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|BackupRetentionPeriod|Integer|7|The number of days for which data backup files are retained. |
|PreferredBackupTime|String|15:00Z-16:00Z|The time to back up data. The time follows the ISO 8601 standard in the *HH:mm*Z-*HH:mm*Z format. The time is displayed in UTC. |
|PreferredBackupPeriod|String|Monday,Wednesday,Friday,Sunday|The cycle to back up data. If more than one day within a week is specified, they are separated with commas \(,\). Valid values:

-   **Monday**
-   **Tuesday**
-   **Wednesday**
-   **Thursday**
-   **Friday**
-   **Saturday**
-   **Sunday** |
|BackupLog|String|Enable|Indicates whether the log backup feature is enabled. Value values: **Enable \| Disabled**. |
|LogBackupRetentionPeriod|Integer|7|The number of days for which log backup files are retained. |
|Duplication|String|Enable|Indicates whether backups are dumped to Alibaba Cloud Object Storage Service \(OSS\). Valid values: **Enable \| Disabled**. |
|DuplicationContent|String|DATA&LOG|The type of data that is dumped to OSS. Valid values:

-   **DATA:** Only data backups are dumped to OSS.
-   **LOG:** Only log backups are dumped to OSS.
-   **DATA&amp;LOG:** Both data and log backups are dumped to OSS.

**Note:** This parameter must be specified when you set the **Duplication** parameter to **Enable**. |
|DuplicationLocation|Struct| |The location where backups are stored. |
|Location|Struct| |The information about the location. |
|Bucket|String|mybucket|The name of the OSS bucket to which backups are dumped. |
|Endpoint|String|oss-cn-shanghai.aliyuncs.com|The endpoint of the OSS bucket. |
|Sotrage|String|OSS|The media that is used to store backups. In most cases, backups are stored in OSS. |
|EnableBackupLog|String|1|Indicates whether the log backup feature is enabled. Valid values:

-   **1:** The log backup feature is enabled.
-   **0:** The log backup feature is disabled. |
|HighSpaceUsageProtection|String|Enable|Indicates whether the log backup deletion feature is enabled. This feature deletes log backup files if the disk usage exceeds 80% or the remaining disk space is less than 5 GB on the instance. Valid values:

-   **Disable**
-   **Enable** |
|LocalLogRetentionHours|Integer|0|The number of hours for which log backup files are retained on the instance. |
|LocalLogRetentionSpace|String|30|The maximum disk usage that is allowed for log backup files on the instance. |
|LogBackupFrequency|String|LogInterval|The frequency at which log backup files are generated. Valid values:

-   The **LogInterval** value indicates that log backup files are generated every 30 minutes.
-   The default frequency is the same as the value of the **PreferredBackupPeriod** parameter.

**Note:** The **LogBackupFrequency** parameter is available only when the instance runs SQL Server. |
|PreferredNextBackupTime|String|2018-01-19T15:15Z|The time to start the next backup. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm*Z format. The time is displayed in UTC. |
|RequestId|String|B87E2AB3-B7C9-4394-9160-7F639F732031|The ID of the request. |
|ArchiveBackupKeepCount|String|1|The number of archived backups that can be retained. |
|ArchiveBackupKeepPolicy|String|ByMonth|The cycle based on which archived backups are retained. |
|ArchiveBackupRetentionPeriod|String|365|The number of days for which archived backups are retained. |
|Category|String|HighAvailability|The edition of the instance. Valid values:

-   **Basic:** The instance runs the Basic Edition.
-   **HighAvailability:** The instance runs the High-availability Edition.
-   **AlwaysOn:** The instance runs the Cluster Edition.
-   **Finance:** The instance runs the Enterprise Edition. |
|CompressType|String|1|The format that is used to compress backups. Valid values:

-   **0:** Backups are not compressed.
-   **1:** Backups are compressed by using zlib.
-   **2:** Backups are compressed by using zlib that invokes multiple threads in parallel for each backup.
-   **4:** Backups are compressed by using QuickLZ and can be used to restore individual databases and tables.
-   **8:** Backups are compressed by using QuickLZ but cannot be used to restore individual databases or tables. This value is available only when the instance runs MySQL 8.0. |
|LogBackupLocalRetentionNumber|Integer|60|The number of log backup files that can be retained on the instance. |
|ReleasedKeepPolicy|String|None|The policy that is used to retain archived backups if the instance is released. Valid values:

-   **None:** No archived backups are retained.
-   **Lastest:** Only the last archived backup is retained.
-   **All:** All of the archived backups are retained. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeBackupPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeBackupPolicyResponse>
  <LogBackupRetentionPeriod>100</LogBackupRetentionPeriod>
  <LogBackupFrequency></LogBackupFrequency>
  <HighSpaceUsageProtection>Enable</HighSpaceUsageProtection>
  <DuplicationLocation>
        <Location>
              <Bucket></Bucket>
              <Endpoint></Endpoint>
        </Location>
        <Sotrage>OSS</Sotrage>
  </DuplicationLocation>
  <ArchiveBackupKeepPolicy>ByMonth</ArchiveBackupKeepPolicy>
  <CompressType>4</CompressType>
  <Duplication></Duplication>
  <LocalLogRetentionHours>18</LocalLogRetentionHours>
  <EnableBackupLog>1</EnableBackupLog>
  <PreferredNextBackupTime>2019-12-24T07:56Z</PreferredNextBackupTime>
  <BackupLog>Enable</BackupLog>
  <ArchiveBackupKeepCount>1</ArchiveBackupKeepCount>
  <PreferredBackupPeriod>Monday,Tuesday</PreferredBackupPeriod>
  <ArchiveBackupRetentionPeriod>0</ArchiveBackupRetentionPeriod>
  <RequestId>E48F2D79-C580-44DB-B756-AB21B5DAA3A7</RequestId>
  <DuplicationContent></DuplicationContent>
  <ReleasedKeepPolicy>None</ReleasedKeepPolicy>
  <BackupRetentionPeriod>7</BackupRetentionPeriod>
  <PreferredBackupTime>07:00Z-08:00Z</PreferredBackupTime>
  <LogBackupLocalRetentionNumber>50</LogBackupLocalRetentionNumber>
  <LocalLogRetentionSpace>30</LocalLogRetentionSpace>
</DescribeBackupPolicyResponse>
```

`JSON` format

```
{
    "LogBackupRetentionPeriod": "100",
    "LogBackupFrequency": "",
    "HighSpaceUsageProtection": "Enable",
    "DuplicationLocation": {
        "Location": {
            "Bucket": "",
            "Endpoint": ""
        },
        "Sotrage": "OSS"
    },
    "ArchiveBackupKeepPolicy": "ByMonth",
    "CompressType": "4",
    "Duplication": "",
    "LocalLogRetentionHours": "18",
    "EnableBackupLog": "1",
    "PreferredNextBackupTime": "2019-12-24T07:56Z",
    "BackupLog": "Enable",
    "ArchiveBackupKeepCount": 1,
    "PreferredBackupPeriod": "Monday,Tuesday",
    "ArchiveBackupRetentionPeriod": 0,
    "RequestId": "E48F2D79-C580-44DB-B756-AB21B5DAA3A7",
    "DuplicationContent": "",
    "ReleasedKeepPolicy": "None",
    "BackupRetentionPeriod": 7,
    "PreferredBackupTime": "07:00Z-08:00Z",
    "LogBackupLocalRetentionNumber": 50,
    "LocalLogRetentionSpace": "30"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

