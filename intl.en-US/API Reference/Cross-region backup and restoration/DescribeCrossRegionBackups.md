# DescribeCrossRegionBackups {#doc_api_Rds_DescribeCrossRegionBackups .reference}

Lists the cross-region data backup files of an RDS instance.

To list the cross-region log backup files of an RDS instance, you can call the [DescribeCrossRegionLogBackupFiles](~~121734~~) API action.

This API action is applicable only to the following DB engine versions and editions:

-   MySQL 5.7 High-availability Edition \(with local SSDs\)
-   MySQL 5.6

## Debug {#api_explorer .section}

[Use OpenAPI Explorer to perform debug operations and generate SDK code examples. do not translate](https://api.aliyun.com/#product=Rds&api=DescribeCrossRegionBackups&type=RPC&version=2014-08-15)

## Request parameters {#parameters .section}

|ID|Type|Required|Example value|Description|
|--|----|--------|-------------|-----------|
|Action|String|Yes|DescribeCrossRegionBackups| The name of this API action. Set this parameter to **DescribeCrossRegionBackups**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx| The ID of the RDS instance whose cross-region data backup files you want to list.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the RDS instance belongs.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |
|CrossBackupId|Integer|No|14562| The ID of a cross-region backup file.

 **Note:** You must set at least the **CrossBackupId** parameter, the **StartTime** and **EndTime** parameters, or all the three parameters.

 |
|StartTime|String|No|2019-05-30T12:10Z| The start time of the query. Format: *yyyy-MM-dd*T*HH:mm*Z \(UTC time \).

 |
|EndTime|String|No|2019-06-15T12:10Z| The end time of the query. Format: *yyyy-MM-dd*T*HH:mm*Z \(UTC time \).

 |
|PageNumber|Integer|No|1| The page number, which must be an integer greater than 0 within the allowed integer range.

 Default value: **1**.

 |
|CrossBackupRegion|String|No|cn-shanghai| The ID of the destination region for cross-region backup.

 |
|PageSize|Integer|No|30| The number of records per page. Valid values:

 -   **30**
-   **50**
-   **100**

 Default value: 30.

 |

## Response parameters {#resultMapping .section}

|ID|Type|Example value|Description|
|--|----|-------------|-----------|
|RegionId|String|cn-hangzhou| The ID of the region to which the RDS instance belongs.

 |
|StartTime|String|2019-05-30T12:10Z| The start time of the query. Format: *yyyy-MM-dd*T*HH:mm*Z \(UTC time \).

 |
|EndTime|String|2019-06-15T12:10Z| The end time of the query. Format: *yyyy-MM-dd*T*HH:mm*Z \(UTC time \).

 |
|TotalRecordCount|Integer|100| The total number of records.

 |
|PageNumber|Integer|1| The page number, which must be an integer greater than 0 within the allowed integer range.

 Default value: **1**.

 |
|PageRecordCount|Integer|30| The number of cross-region data backup files displayed on a specified page.

 |
|RequestId|String|60912B41-7579-4B5D-B289-8856030F0A6A| The ID of the request.

 |
|Items| | | The list of cross-region data backup files.

 |
|BackupEndTime|String|2019-06-15T12:10Z| The end time of cross-region backup. Format: *yyyy-MM-dd*T*HH:mm*Z \(UTC time \).

 |
|BackupMethod|String|P| The cross-region backup method. Valid values:

 -   **L**: logical backup.
-   **P**: physical backup.

 |
|BackupSetScale|Integer|0| The data backup policy. Valid values:

 -   **0**: Data is backed up by instance.
-   **1**: Data is backed up by database.

 |
|BackupSetStatus|Integer|0| The status of a cross-region data backup file. Valid values:

 -   **0**: The backup is completed.
-   **1**: The backup failed.

 |
|BackupStartTime|String|2019-05-30T12:10Z| The start time of cross-region backup. Format: *yyyy-MM-dd*T*HH:mm*Z \(UTC time \).

 |
|BackupType|String|F| The cross-region backup type. Valid values:

 -   **F**: full backup.
-   **I**: incremental backup.

 |
|Category|String|HighAvailability| The edition of the RDS instance. Valid values:

 -   **Basic**: Basic Edition.
-   **HighAvailability**: High-availability Edition.
-   **Finance**: Finance Edition, which is available only in the China Mainland.

 |
|ConsistentTime|String|2019-06-12T05:44:46Z| The time point of data in a cross-region data backup file.

 |
|CrossBackupDownloadLink|String|http://rdsddrbak-shanghai.oss-cn-shanghai.aliyuncs.com/xxxxx| The URL from which you can download a cross-region data backup file.

 |
|CrossBackupId|Integer|14377| The ID of a cross-region data backup file.

 |
|CrossBackupRegion|String|cn-shanghai| The ID of the destination region for cross-region backup.

 |
|CrossBackupSetFile|String|cn-hangzhou\_rm-xxxxx\_hins81xxx\_data\_20190612134426\_qp.xb| The name of the compressed package for a cross-region data backup file.

 |
|CrossBackupSetLocation|String|oss| The location where a cross-region data backup file is stored.

 |
|CrossBackupSetSize|Long|5312836| The size of a cross-region data backup file. Unit: byte.

 |
|DBInstanceStorageType|String|ssd| The storage class to use.

 |
|Engine|String|MySQL| The database type to use.

 |
|EngineVersion|String|5.6| The database version to use.

 |
|InstanceId|Integer|8161055| The ID of the RDS instance. You can determine whether a data backup set is generated from the master RDS instance or its slave RDS instance.

 |
|RestoreRegions| |"cn-hangzhou", "cn-shanghai"| The list of regions to which a cross-region backup file can be restored.

 |

## Examples {#demo .section}

Request example:

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action = describecrosregionbackups
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&CrossBackupId=14562
&<Common request parameters>

```

Response example:

`XML` format:

``` {#xml_return_success_demo}
<DescribeCrossRegionBackupsResponse>
  <Items>
		    <Item>
			      <CrossBackupSetFile>cn-hangzhou_rm-bpxxxxx_hins798xxxx_data_20190611125201.tar.gz</CrossBackupSetFile>
			      <BackupSetScale>0</BackupSetScale>
			      <BackupType>F</BackupType>
			      <InstanceId>7980000</InstanceId>
			      <CrossBackupId>14358</CrossBackupId>
			      <BackupEndTime>2019-06-11T04:55:02Z</BackupEndTime>
			      <BackupMethod>P</BackupMethod>
			      <CrossBackupSetLocation>oss</CrossBackupSetLocation>
			      <CrossBackupSetSize>2179643</CrossBackupSetSize>
			      <Engine>mysql</Engine>
			      <BackupStartTime>2019-06-11T04:52:46Z</BackupStartTime>
			      <CrossBackupDownloadLink>http://rdsddrbak-zb.oss-cn-zhangjiakou.aliyuncs.com/cn-hangzhou_rm-bpxxxxx_hins7986073_data_20190611125201.tar.gz?OSSAccessKeyId=LTAxxxxx&amp;Expires=1560501641&amp;Signature=laK0kxxxxx%3D</CrossBackupDownloadLink>
			      <Category>HighAvailability</Category>
			      <CrossBackupRegion>cn-zhangjiakou</CrossBackupRegion>
			      <RestoreRegions>
				        <RestoreRegion>cn-hangzhou</RestoreRegion>
				        <RestoreRegion>cn-zhangjiakou</RestoreRegion>
			      </RestoreRegions>
			      <EngineVersion>5.7</EngineVersion>
			      <DBInstanceStorageType>ssd</DBInstanceStorageType>
		    </Item>
	  </Items>
	  <TotalRecordCount>1</TotalRecordCount>
	  <PageNumber>1</PageNumber>
	  <RequestId>60912B41-7579-4B5D-B289-8856030F0A6A</RequestId>
	  <RegionId>cn-hangzhou</RegionId>
	  <EndTime>2019-06-11T08:00:00Z</EndTime>
	  <StartTime>2019-06-10T00:00:00Z</StartTime>
	  <PageRecordCount>30</PageRecordCount>
    </DescribeCrossRegionBackupsResponse>
```

`JSON` format:

``` {#json_return_success_demo}
{
	"Items":{
		"Item":[
			{
				"CrossBackupSetFile":"cn-hangzhou_rm-bpxxxxx_hins798xxxx_data_20190611125201.tar.gz",
				"BackupSetScale":0,
				"BackupType":"F",
				"InstanceId":7980000,
				"CrossBackupId":14358,
				"BackupEndTime":"2019-06-11T04:55:02Z",
				"BackupMethod":"P",
				"CrossBackupSetLocation":"oss",
				"CrossBackupSetSize":2179643,
				"Engine":"mysql",
				"BackupStartTime":"2019-06-11T04:52:46Z",
				"CrossBackupDownloadLink":"http://rdsddrbak-zb.oss-cn-zhangjiakou.aliyuncs.com/cn-hangzhou_rm-bpxxxxx_hins7986073_data_20190611125201.tar.gz?OSSAccessKeyId=LTAxxxxx&Expires=1560501641&Signature=laK0kxxxxx%3D",
				"Category":"HighAvailability",
				"CrossBackupRegion":"cn-zhangjiakou",
				"RestoreRegions":{
					"RestoreRegion":[
						"cn-hangzhou",
						"cn-zhangjiakou"
					]
				},
				"EngineVersion":"5.7",
				"DBInstanceStorageType":"ssd"
			}
		]
	},
	"PageNumber":1,
	"TotalRecordCount":1,
	"RegionId":"cn-hangzhou",
	"RequestId":"60912B41-7579-4B5D-B289-8856030F0A6A",
	"EndTime":"2019-06-11T08:00:00Z",
	"StartTime":"2019-06-10T00:00:00Z",
	"PageRecordCount":30
}
```

## Errors {#section_ky4_7jr_f7j .section}

For a list of error codes, visit the [错误中心](https://error-center.alibabacloud.com/status/product/Rds).

