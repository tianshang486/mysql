# DescribeAvailableRecoveryTime {#doc_api_Rds_DescribeAvailableRecoveryTime .reference}

Queries the time range from which you can restore the data of an RDS instance by using a specified cross-region backup file.

To query the time range from which you can restore the data of an RDS instance by using a specified common backup file, you can call the [DescribeBackups](~~26273~~) API action.

This API action is applicable only to the following DB engine versions and editions:

-   MySQL 5.7 High-availability Edition \(with local SSDs\)
-   MySQL 5.6

## Debug {#api_explorer .section}

Use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeAvailableRecoveryTime&type=RPC&version=2014-08-15) to perform debug operations and generate SDK code examples.

## Request parameters {#parameters .section}

|ID|Type|Required|Example value|Description|
|--|----|--------|-------------|-----------|
|Action|String|Yes|DescribeAvailableRecoveryTime| The name of this API action. Value: **DescribeAvailableRecoveryTime**.

 |
|CrossBackupId|Integer|Yes|14377| The ID of the cross-region backup file to use. You can call the [DescribeCrossRegionBackups](~~121733~~) API action to obtain this file ID.

 |
|RegionId|String|No|cn-hangzhou| The ID of the region to which the RDS instance belongs.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|ID|Type|Example value|Description|
|--|----|-------------|-----------|
|CrossBackupId|Integer|14377| The ID of the cross-region backup file to use.

 |
|RecoveryBeginTime|String|2019-06-12T05:22:29Z| The start time of data that can be restored by using the cross-region backup file. Format: *yyyy-MM-dd*T*HH:mm:ss*Z \(UTC time\).

 |
|RecoveryEndTime|String|2019-06-12T07:33:12Z| The end time of data that can be restored by using the cross-region backup file. Format: *yyyy-MM-dd*T*HH:mm:ss*Z \(UTC time\).

 |
|RegionId|String|cn-hangzhou| The ID of the region to which the RDS instance belongs.

 |
|RequestId|String|8CCBF4BA-7CE1-47E1-B49F-E97EA200A40D| The ID of the request.

 |

## Examples {#demo .section}

Request example:

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeAvailableRecoveryTime
&CrossBackupId=14377
&<Common request parameters>

```

Response example:

`XML` format:

``` {#xml_return_success_demo}
<DescribeAvailableRecoveryTimeResponse>
  <RecoveryEndTime>2019-06-12T07:33:12Z</RecoveryEndTime>
	  <RecoveryBeginTime>2019-06-12T05:22:29Z</RecoveryBeginTime>
	  <RequestId>8CCBF4BA-7CE1-47E1-B49F-E97EA200A40D</RequestId>
	  <RegionId>cn-hangzhou</RegionId>
	  <CrossBackupId>14377</CrossBackupId>
    </DescribeAvailableRecoveryTimeResponse>
```

`JSON` format:

``` {#json_return_success_demo}
{
	"RecoveryEndTime":"2019-06-12T07:33:12Z",
	"RecoveryBeginTime":"2019-06-12T05:22:29Z",
	"CrossBackupId":14377,
	"RegionId":"cn-hangzhou",
	"RequestId":"8CCBF4BA-7CE1-47E1-B49F-E97EA200A40D"
}
```

## Errors {#section_cxy_99h_oed .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidBackupSetID.NotFound|Specified backup set ID does not exist.|The error message returned when the specified backup file ID does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

