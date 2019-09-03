# ModifyInstanceCrossBackupPolicy {#doc_api_Rds_ModifyInstanceCrossBackupPolicy .reference}

Modifies the cross-region backup settings of an RDS instance.

This API action is applicable only to the following DB engine versions and editions:

-   MySQL 5.7 High-availability Edition \(with local SSDs\)
-   MySQL 5.6

## Debug {#api_explorer .section}

Use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifyInstanceCrossBackupPolicy&type=RPC&version=2014-08-15) to perform debug operations and generate SDK code examples.

## Request parameters {#parameters .section}

|ID|Type|Required|Example value|Description|
|--|----|--------|-------------|-----------|
|Action|String|Yes|ModifyInstanceCrossBackupPolicy| The name of this API action. Value: **ModifyInstanceCrossBackupPolicy**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx| The ID of the RDS instance.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the RDS instance belongs. You can call the [DescribeRegions](~~26243~~) API action to obtain this region ID.

 |
|CrossBackupType|String|No|1| The storage type used for saving cross-region backup files. Default value: **1**. The value 1 indicates that all backup files are saved.

 |
|RetentType|Integer|No|1| The method of retaining cross-region backup files. Default value: **1**. The value 1 indicates that cross-region backup files are retained based on a specified duration.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |
|BackupEnabled|String|No|1| The status of the switch that controls the cross-region backup function \(data backup and log backup\). Valid values:

 -   **0**: The function is disabled.
-   **1**: The function is enabled.

 |
|LogBackupEnabled|String|No|1| The status of the switch that controls the cross-region log backup function. Valid values:

 -   **0**: The function is disabled.
-   **1**: The function is enabled.

 |
|CrossBackupRegion|String|No|cn-shanghai| The ID of the destination region for cross-region backup.

 |
|Retention|Integer|No|7| The number of days for retaining cross-region backup files. Valid values: **7 to 1825**.

 |

## Response parameters {#resultMapping .section}

|ID|Type|Example value|Description|
|--|----|-------------|-----------|
|BackupEnabled|String|1| The status of the switch that controls the cross-region backup function. Valid values:

 -   **0**: The function is disabled.
-   **1**: The function is enabled.

 |
|CrossBackupRegion|String|cn-shanghai| The ID of the destination region for cross-region backup.

 |
|CrossBackupType|String|1| The storage type used for saving cross-region backup files: Default value: **1**. The value 1 indicates that all cross-region backup files are saved.

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx| The ID of the RDS instance whose data is backed up across regions.

 |
|LogBackupEnabled|String|1| The status of the switch that controls the log backup function. Valid values:

 -   **0**: The function is disabled.
-   **1**: The function is enabled.

 |
|RegionId|String|cn-hangzhou| The ID of the region to which the RDS instance belongs. You can call the [DescribeRegions](~~26243~~) API action to obtain this region ID.

 |
|RequestId|String|50A6059D-6DBB-46C6-A851-1EE93C9013CF| The ID of the request.

 |
|RetentType|Integer|1| The method of retaining cross-region backup files. Default value: **1**. The value 1 indicates that cross-region backup files are retained based on a specified duration.

 |
|Retention|Integer|15| The number of days for retaining cross-region backup files. Valid values: **7 to 1825**.

 |

## Examples {#demo .section}

Request example:

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=ModifyInstanceCrossBackupPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&RegionId=cn-hangzhou
&<Common request parameters>

```

Response example:

`XML` format:

``` {#xml_return_success_demo}
<ModifyInstanceCrossBackupPolicyResponse>
  <CrossBackupType>1</CrossBackupType>
	  <LogBackupEnabled>Enable</LogBackupEnabled>
	  <BackupEnabled>Enable</BackupEnabled>
	  <CrossBackupRegion>cn-shanghai</CrossBackupRegion>
	  <RetentType>1</RetentType>
	  <RequestId>50A6059D-6DBB-46C6-A851-1EE93C9013CF</RequestId>
	  <DBInstanceId>rm-bpxxxxx</DBInstanceId>
	  <RegionId>cn-hangzhou</RegionId>
	  <StorageType>oss</StorageType>
	  <Endpoint></Endpoint>
	  <Retention>15</Retention>
    </ModifyInstanceCrossBackupPolicyResponse>
```

`JSON` format:

``` {#json_return_success_demo}
{
	"LogBackupEnabled":"Enable",
	"CrossBackupType":"1",
	"BackupEnabled":"Enable",
	"RetentType":1,
	"CrossBackupRegion":"cn-shanghai",
	"RegionId":"cn-hangzhou",
	"DBInstanceId":"rm-bpxxxxx",
	"RequestId":"50A6059D-6DBB-46C6-A851-1EE93C9013CF",
	"Retention":15,
	"Endpoint":"",
	"StorageType":"oss"
}
```

## Errors {#section_vx2_t9w_q7f .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

