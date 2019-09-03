# DescribeCrossRegionBackupDBInstance {#doc_api_Rds_DescribeCrossRegionBackupDBInstance .reference}

Queries which RDS instances have cross-region backup enabled in a specified region, as well as the cross-region backup settings of these instances.

This API action is applicable only to the following DB engine versions and editions:

-   MySQL 5.7 High-availability Edition \(with local SSDs\)
-   MySQL 5.6

## Debug {#apiExplorer .section}

Use [API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeCrossRegionBackupDBInstance) to perform debug operations and generate SDK code examples.

## Request parameters {#parameters .section}

|ID|Type|Required|Example value|Description|
|--|----|--------|-------------|-----------|
|Action|String|Yes|DescribeCrossRegionBackupDBInstance| The name of this API action. Value: **DescribeCrossRegionBackupDBInstance**.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the RDS instances belong.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |
|PageNumber|Integer|No|1| The page number, which must be an integer greater than 0 within the allowed integer range.

 Default value: **1**.

 |
|PageSize|Integer|No|30| Number of records per page. Valid values:

 -   **30**
-   **50**
-   **100**

 Default value: 30.

 |
|DBInstanceId|String|No|rm-uf6wjk5xxxxxxxxxx| The IDs of the RDS instances. Up to 30 instance IDs can be entered at a time. You must separate the instance IDs by using commas \(,\).

 |

## Response parameters {#resultMapping .section}

|ID|Type|Example value|Description|
|--|----|-------------|-----------|
|RegionId|String|cn-hangzhou| The ID of the region to which the RDS instances belong.

 |
|TotalRecords|Interger|100| The total number of records.

 |
|ItemsNumbers|Integer|1| The number of items in the cross-region backup settings list.

 |
|PageNumber|Integer|1| The page number, which must be an integer greater than 0 within the allowed integer range.

 Default value: **1**.

 |
|PageSize|Integer|30| The number of records per page. Valid values:

 -   **30**
-   **50**
-   **100**

 Default value: 30.

 |
|RequestId|String|33517002-182D-40BE-93EC-610BD3381045| The ID of the request.

 |
|Items|N/A| | The list that contains the cross-region backup settings of the RDS instances in the specified region.

 |
|└BackupEnabled|String|Enable| The status of the switch that controls the cross-region backup function. Valid values:

 -   **Disable**: The function is disabled.
-   **Enable**: The function is enabled.

 |
|└BackupEnabledTime|String|2019-06-12T05:44:21Z| The time when cross-region data backup is enabled. Format: *yyyy-MM-dd*T*HH:mm:ss*Z \(UTC time\).

 |
|└CrossBackupRegion|String|cn-shanghai| The ID of the destination region for cross-region backup.

 |
|└CrossBackupType|String|1| The storage type used for saving cross-region backup files. Default value: **1**. The value 1 indicates that all cross-region backup files are saved.

 |
|└DBInstanceDescription|String|Test Database| The name of an RDS instance. The instance name must start with a letter and can contain 2 to 256 characters including letters, digits, hyphens \(-\), and underscores \(\_\). do not translate

 **Note:** The instance name cannot start with http:// or https://.

 |
|└DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx| The IDs of the RDS instances.

 |
|└DBInstanceStatus|String|Running|The status of an RDS instance. For more information, see [Instance status table](intl.en-US/API Reference/Appendix/Instance status table.md#).|
|└Engine|String|MySQL| The used database type.

 |
|└EngineVersion|String|5.6| The used database version.

 |
|└LockMode|String|Unlock| The lock status of an RDS instance. Valid values:

 -   **Unlock**. The RDS instance is running properly without being locked.
-   **ManualLock**: The RDS instance is locked manually.
-   **LockByExpiration**: The RDS instance is locked automatically upon expiration.
-   **LockByRestoration**: The RDS instance is locked automatically before a rollback.
-   **LockByDiskQuota**: The RDS instance is locked automatically because its storage capacity is used up.

 |
|└LogBackupEnabled|String|Enable| The status of the switch that controls the cross-region log backup function. Valid values:

 -   **Disable**: The function is disabled.
-   **Enable**: The function is enabled.

 |
|└LogBackupEnabledTime|String|2019-06-12T05:44:21Z| The time when cross-region log backup is enabled. Format: *yyyy-MM-dd*T*HH:mm:ss*Z \(UTC time\).

 |
|└RetentType|Integer|1| The method of retaining cross-region backup files. Currently, cross-region backup files can be retained only based on a specified duration. Default value: **1**.

 |
|└Retention|Integer|15| The number of days for retaining cross-region backup files. Value range: **7 to 1825**.

 |

## Examples {#demo .section}

Request example:

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeCrossRegionBackupDBInstance
&RegionId=cn-hangzhou
&<Common request parameters>

```

Response example:

`XML` format:

``` {#xml_return_success_demo}
<DescribeCrossRegionBackupDBInstanceResponse>
  <Items>
    <Item>
      <LockMode>Unlock</LockMode>
      <CrossBackupType>1</CrossBackupType>
      <LogBackupEnabled>Enable</LogBackupEnabled>
      <BackupEnabledTime>2019-06-12T05:44:21Z</BackupEnabledTime>
      <BackupEnabled>Enable</BackupEnabled>
      <RetentType>1</RetentType>
      <DBInstanceId>rm-bpxxxxx</DBInstanceId>
      <Retention>15</Retention>
      <DBInstanceDescription>Test Database</DBInstanceDescription>
      <Engine>MySQL</Engine>
      <LogBackupEnabledTime>2019-06-12T05:44:21Z</LogBackupEnabledTime>
      <CrossBackupRegion>cn-shanghai</CrossBackupRegion>
      <EngineVersion>5.6</EngineVersion>
      <DBInstanceStatus>Running</DBInstanceStatus>
    </Item>
  </Items>
  <PageNumber>1</PageNumber>
  <RegionId>cn-hangzhou</RegionId>
  <RequestId>33517002-182D-40BE-93EC-610BD3381045</RequestId>
  <ItemsNumbers>1</ItemsNumbers>
  <TotalRecords>1</TotalRecords>
</DescribeCrossRegionBackupDBInstanceResponse>

```

`JSON` format:

``` {#json_return_success_demo}
{
	"Items":{
		"Item":[
			{
				"LockMode":"Unlock",
				"CrossBackupType":"1",
				"LogBackupEnabled":"Enable",
				"BackupEnabledTime":"2019-06-12T05:44:21Z",
				"BackupEnabled":"Enable",
				"RetentType":1,
				"DBInstanceId":"rm-bpxxxxx",
				"Retention":15,
				"DBInstanceDescription":"Test Database",
				"Engine":"MySQL",
				"LogBackupEnabledTime":"2019-06-12T05:44:21Z",
				"CrossBackupRegion":"cn-shanghai",
				"EngineVersion":"5.6",
				"DBInstanceStatus":"Running"
			}
		]
	},
	"PageNumber":1,
	"RequestId":"33517002-182D-40BE-93EC-610BD3381045",
	"RegionId":"cn-hangzhou",
	"ItemsNumbers":1,
	"TotalRecords":1
}
```

## Errors {#section_tsh_tl2_64m .section}

For a list of error codes, visit the [API Error Center](https://error-center.aliyun.com/status/product/Rds).

