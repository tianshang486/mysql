# DescribeInstanceCrossBackupPolicy {#doc_api_Rds_DescribeInstanceCrossBackupPolicy .reference}

Queries the cross-region backup settings of an RDS instance.

This API action is applicable only to the following DB engine versions and editions:

-   MySQL 5.7 High-availability Edition \(with local SSDs\)
-   MySQL 5.6

## Debug {#api_explorer .section}

Use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeInstanceCrossBackupPolicy&type=RPC&version=2014-08-15) perform debug operations and generate SDK code examples.

## Request parameters {#parameters .section}

|ID|Type|Required|Example value|Description|
|--|----|--------|-------------|-----------|
|Action|String|Yes|DescribeInstanceCrossBackupPolicy| The name of this API action. Value: **DescribeInstanceCrossBackupPolicy**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx| The ID of the RDS instance.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the RDS instance belongs. You can call the [DescribeRegions](~~26243~~) API action to obtain this region ID.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|ID|Type|Example value|Description|
|--|----|-------------|-----------|
|BackupEnabled|String|Enable| The status of the switch that controls the cross-region backup function. Valid values:

 -   **Disable**: The function is disabled.
-   **Enable**: The function is enabled.

 |
|BackupEnabledTime|String|2019-06-12T05:44:21Z| The start time of cross-region backup. Format: *yyyy-MM-dd*T*HH:mm:ss*Z \(UTC time\).

 |
|CrossBackupRegion|String|cn-shanghai| The ID of the destination region for cross-region backup.

 |
|CrossBackupType|String|1| The storage type for saving cross-region backup files. Default value: **1**. The value 1 indicates that all cross-region backup files are saved.

 |
|DBInstanceDescription|String|Test Database| The name of the RDS instance. The name must start with a letter and can contain 2 to 256 characters including letters, digits, hyphens, and underscores \(\_\). do not translate

 **Note:** The name cannot start with http:// or https://.

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx| The ID of the RDS instance whose data you want to back up across regions.

 |
|DBInstanceStatus|String|Running|The status of the RDS instance. For more information, see [Instance status table](intl.en-US/API Reference/Appendix/Instance status table.md#).|
|Engine|String|MySQL| The database type to use.

 |
|EngineVersion|String|5.6| The database version to use.

 |
|LockMode|String|Unlock| The lock status of the RDS instance. Valid values:

 -   **Unlock**: The RDS instance is running properly without being locked.
-   **ManualLock**: The RDS instance is locked manually.
-   **LockByExpiration**: The RDS instance is locked automatically upon expiration.
-   **LockByRestoration**: The RDS instance is locked automatically before a rollback.
-   **LockByDiskQuota**: The RDS instance is locked automatically because its storage capacity is used up.

 |
|LogBackupEnabled|String|Enable| The status of the switch that controls the cross-region log backup function. Valid values:

 -   **Disable**: The function is disabled.
-   **Enable**: The function is enabled.

 |
|LogBackupEnabledTime|String|2019-06-12T05:44:21Z| The start time of cross-region log backup. Format: *yyyy-MM-dd*T*HH:mm:ss*Z \(UTC time \).

 |
|RegionId|String|cn-hangzhou| The ID of the region to which the RDS instance belongs.

 |
|RequestId|String|CB7667B2-72C8-497B-9BD8-3B343CEF51AB| The ID of the request.

 |
|RetentType|Integer|1| The method of retaining cross-region backup files. Default value: **1**. The value 1 indicates that cross-region backup files are retained based on a specified duration.

 |
|Retention|Integer|15| The number of days for retaining cross-region backup files. Value range: **7 to 1825**.

 |

## Examples {#demo .section}

Request example:

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeInstanceCrossBackupPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<Common request parameter>

```

Response example:

`XML` format:

``` {#xml_return_success_demo}
<DescribeInstanceCrossBackupPolicyResponse>
  <DBInstanceStatusDesc>ACTIVATION</DBInstanceStatusDesc>
	  <LockMode>Unlock</LockMode>
	  <BackupEnabledTime>2019-06-12T05:44:21Z</BackupEnabledTime>
	  <CrossBackupType>1</CrossBackupType>
	  <LogBackupEnabled>Enable</LogBackupEnabled>
	  <BackupEnabled>Enable</BackupEnabled>
	  <RetentType>1</RetentType>
	  <DBInstanceId>rm-bpxxxxx</DBInstanceId>
	  <DBInstanceDescription></DBInstanceDescription>
	  <Retention>15</Retention>
	  <Engine>mysql</Engine>
	  <LogBackupEnabledTime>2019-06-12T05:44:21Z</LogBackupEnabledTime>
	  <CrossBackupRegion>cn-shanghai</CrossBackupRegion>
	  <StorageOwner>rds</StorageOwner>
	  <RegionId>cn-hangzhou</RegionId>
	  <RequestId>CB7667B2-72C8-497B-9BD8-3B343CEF51AB</RequestId>
	  <EngineVersion>5.6</EngineVersion>
	  <StorageType>oss</StorageType>
	  <Endpoint></Endpoint>
	  <DBInstanceStatus>1</DBInstanceStatus>
    </DescribeInstanceCrossBackupPolicyResponse>
```

`JSON` format:

``` {#json_return_success_demo}
{
	"DBInstanceStatusDesc":"ACTIVATION",
	"LockMode":"Unlock",
	"BackupEnabledTime":"2019-06-12T05:44:21Z",
	"CrossBackupType":"1",
	"LogBackupEnabled":"Enable",
	"BackupEnabled":"Enable",
	"RetentType":1,
	"DBInstanceId":"rm-bpxxxxx",
	"DBInstanceDescription":"",
	"Retention":15,
	"Engine":"mysql",
	"LogBackupEnabledTime":"2019-06-12T05:44:21Z",
	"CrossBackupRegion":"cn-shanghai",
	"StorageOwner":"rds",
	"RequestId":"CB7667B2-72C8-497B-9BD8-3B343CEF51AB",
	"RegionId":"cn-hangzhou",
	"Endpoint":"",
	"StorageType":"oss",
	"EngineVersion":"5.6",
	"DBInstanceStatus":"1"
}
```

## Errors {#section_zjj_cct_6l8 .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

