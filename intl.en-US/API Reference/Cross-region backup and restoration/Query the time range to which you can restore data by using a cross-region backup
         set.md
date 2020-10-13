# Query the time range to which you can restore data by using a cross-region backup set

Queries the time range to which you can restore data by using a cross-region backup set.

To view the time range to which you can restore data by using a common backup set, see [DescribeBackups](~~26273~~).

Before you call this operation, make sure that the instance runs one of the following database engine versions and RDS editions:

-   MySQL 8.0 in the High-availability Edition \(with local SSDs\)
-   MySQL 5.7 in the High-availability Edition \(with local SSDs\)
-   MySQL 5.6

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeAvailableRecoveryTime&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAvailableRecoveryTime|The operation that you want to perform. Set the value to **DescribeAvailableRecoveryTime**. |
|CrossBackupId|Integer|Yes|14377|The ID of the cross-region backup set. You can call the [DescribeCrossRegionBackups](~~121733~~) operation to query backup set IDs. |
|RegionId|String|No|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CrossBackupId|Integer|14377|The ID of the cross-region backup set. |
|RecoveryBeginTime|String|2019-06-12T05:22:29Z|The start time to which data can be restored. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|RecoveryEndTime|String|2019-06-12T07:33:12Z|The end time to which data can be restored. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|RegionId|String|cn-hangzhou|The region ID of the source instance. |
|RequestId|String|8CCBF4BA-7CE1-47E1-B49F-E97EA200A40D|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeAvailableRecoveryTime
&CrossBackupId=14377
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeAvailableRecoveryTimeResponse>
  <RecoveryEndTime>2019-06-12T07:33:12Z</RecoveryEndTime>
	  <RecoveryBeginTime>2019-06-12T05:22:29Z</RecoveryBeginTime>
	  <RequestId>8CCBF4BA-7CE1-47E1-B49F-E97EA200A40D</RequestId>
	  <RegionId>cn-hangzhou</RegionId>
	  <CrossBackupId>14377</CrossBackupId>
</DescribeAvailableRecoveryTimeResponse>
```

`JSON` format

```
{
	"RecoveryEndTime": "2019-06-12T07:33:12Z",
	"RecoveryBeginTime": "2019-06-12T05:22:29Z",
	"RequestId": "8CCBF4BA-7CE1-47E1-B49F-E97EA200A40D",
	"RegionId": "cn-hangzhou",
	"CrossBackupId": 14377
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|404|InvalidBackupSetID.NotFound|Specified backup set ID does not exist.|The error message returned because the specified backup set ID does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

