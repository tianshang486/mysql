# DescribeCrossRegionLogBackupFiles {#doc_api_Rds_DescribeCrossRegionLogBackupFiles .reference}

Lists the cross-region log backup files of an RDS instance.

To list the data backup files of an RDS instance, you can call the [DescribeCrossRegionBackups](~~121733~~) API action.

This API action is applicable only to the following DB engine versions and editions:

-   MySQL 5.7 High-availability Edition \(with local SSDs\)
-   MySQL 5.6

## Debug {#api_explorer .section}

Use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeCrossRegionLogBackupFiles&type=RPC&version=2014-08-15) to perform debug operations and generate SDK code examples.

## Request parameters {#parameters .section}

|ID|Type|Required|Example value|Description|
|--|----|--------|-------------|-----------|
|Action|String|Yes|DescribeCrossRegionLogBackupFiles| The name of this API action. Value: **DescribeCrossRegionLogBackupFiles**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx| The ID of the RDS instance whose log backup files you want to list.

 |
|StartTime|String|Yes|2019-05-30T12:10Z| The start time of the query. Format: *yyyy-MM-dd*T*HH:mm*Z \(UTC time\).

 |
|EndTime|String|Yes|2019-06-15T12:10Z| The end time of the query. Format: *yyyy-MM-dd*T*HH:mm*Z \(UTC time\).

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the RDS instance belongs. You can call the [DescribeRegions](~~26243~~) API action to obtain this region ID.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |
|PageNumber|Integer|No|1| The page number, which must be an integer greater than 0 within the allowed integer range.

 Default value: **1**.

 |
|PageSize|Integer|No|30| The number of records per page. Valid values:

 -   **30**
-   **50**
-   **100**

 Default value: 30.

 |
|CrossBackupRegion|String|No|cn-shanghai| The ID of the destination region for cross-region backup. You can call the [DescribeCrossRegionBackupDBInstance](~~121737~~) API action to obtain this region ID.

 |

## Response parameters {#resultMapping .section}

|ID|Type|Example value|Description|
|--|----|-------------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx| The ID of the RDS instance.

 |
|StartTime|String|2019-05-30T12:10Z| The start time of the query. Format: *yyyy-MM-dd*T*HH:mm*Z \(UTC time\).

 |
|EndTime|String|2019-06-15T12:10Z| The end time of the query. Format: *yyyy-MM-dd*T*HH:mm*Z \(UTC time\).

 |
|TotalRecordCount|Integer|100| The total number of records.

 |
|PageNumber|Integer|1| The page number, which must be an integer greater than 0 within the allowed integer range.

 Default value: **1**.

 |
|PageRecordCount|Integer|30| The number of log backup files displayed on a specified page.

 |
|RegionId|String|cn-hangzhou| The ID of the region to which the RDS instance belongs.

 |
|RequestId|String|DAC241E8-28E6-49DA-BFB0-B2DD090885C1| The ID of the request.

 |
|Items| | | The list of cross-region log backup files.

 |
|CrossBackupRegion|String|cn-shanghai| The ID of the destination region for cross-region backup.

 |
|CrossDownloadLink|String|"http://rdsddrlog-zb.oss-cn-zhangjiakou.aliyuncs.com/xxxxx| The external link from which you can download a cross-region log backup file.

 |
|CrossIntranetDownloadLink|String|http://rdsddrlog-zb.oss-cn-zhangjiakou-internal.aliyuncs.com/xxxxx| The internal link from which you can download a cross-region log backup file.

 |
|CrossLogBackupId|Integer|14567| The ID of a cross-region log backup file.

 |
|CrossLogBackupSize|Long|5312836| The maximum size that a cross-region log backup file can reach. Unit: byte.

 |
|InstanceId|Integer|8161055| The ID of the RDS instance

 |
|LinkExpiredTime|String|2019-06-30T15:00:00Z| The time when a download link is to expire. Format: *yyyy-MM-dd*T*HH:mm:ss*Z \(UTC time\).

 |
|LogBeginTime|String|2019-05-30T12:10Z| The start time of a cross-region log backup file. Format: *yyyy-MM-dd*T*HH:mm*Z \(UTC time\).

 |
|LogEndTime|String|2019-05-30T20:10Z| The end time of a cross-region log backup file. Format: *yyyy-MM-dd*T*HH:mm*Z \(UTC time\).

 |
|LogFileName|String|Cn-hangzhou\_rm-bpxxxxx\_7198739\_mysql-bin.000230| The name of a cross-region log backup file.

 |

## Examples {#demo .section}

Request example:

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeCrossRegionLogBackupFiles
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&StartTime=2019-05-30T12:10Z
&EndTime=2019-06-15T12:10Z
&<CommonParameters>

```

Response example:

`XML` format:

``` {#xml_return_success_demo}
<DescribeCrossRegionLogBackupFilesResponse>
  <Items>
		    <Item>
			      <LinkExpiredTime>2019-06-02T07:36:18Z</LinkExpiredTime>
			      <CrossBackupRegion>cn-zhangjiakou</CrossBackupRegion>
			      <LogEndTime>2019-06-01T06:11:49Z</LogEndTime>
			      <LogBeginTime>2019-06-01T00:11:44Z</LogBeginTime>
			      <InstanceId>7198743</InstanceId>
			      <CrossLogBackupSize>770014</CrossLogBackupSize>
			      <CrossDownloadLink>http://rdsddrlog-zb.oss-cn-zhangjiakou.aliyuncs.com/xxxxxx</CrossDownloadLink>
			      <CrossIntranetDownloadLink>http://rdsddrlog-zb.oss-cn-zhangjiakou-internal.aliyuncs.com/xxxxx</CrossIntranetDownloadLink>
		    </Item>
	  </Items>
	  <PageNumber>1</PageNumber>
	  <TotalRecordCount>52</TotalRecordCount>
	  <DBInstanceId>rm-xxxxx</DBInstanceId>
	  <RegionId>cn-hangzhou</RegionId>
	  <RequestId>A9723BCE-F32F-4F05-9922-8371C0842FA7</RequestId>
	  <EndTime>EndTime=2019-06-15T12:10Z</EndTime>
	  <StartTime>2019-05-30T12:10Z</StartTime>
	  <PageRecordCount>10</PageRecordCount>
    </DescribeCrossRegionLogBackupFilesResponse>
```

`JSON` format:

``` {#json_return_success_demo}
{
	"Items":{
		"Item":[
			{
				"LinkExpiredTime":"2019-06-02T07:36:18Z",
				"CrossBackupRegion":"cn-zhangjiakou",
				"LogBeginTime":"2019-06-01T00:11:44Z",
				"LogEndTime":"2019-06-01T06:11:49Z",
				"InstanceId":7198743,
				"CrossLogBackupSize":770014,
				"CrossDownloadLink":"http://rdsddrlog-zb.oss-cn-zhangjiakou.aliyuncs.com/xxxxxx",
				"CrossIntranetDownloadLink":"http://rdsddrlog-zb.oss-cn-zhangjiakou-internal.aliyuncs.com/xxxxx"
			}
		]
	},
	"TotalRecordCount":52,
	"PageNumber":1,
	"RequestId":"A9723BCE-F32F-4F05-9922-8371C0842FA7",
	"RegionId":"cn-hangzhou",
	"DBInstanceId":"rm-xxxxx",
	"EndTime":"EndTime=2019-06-15T12:10Z",
	"StartTime":"2019-05-30T12:10Z",
	"PageRecordCount":10
}
```

## Errors {#section_z7m_gbz_xpr .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidStartTime.Format|Specified start time is not valid.|The error message returned when the specified start time is invalid.|
|400|InvalidEndTime.Format|Specified end time is not valid.|The error message returned when the specified end time is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

