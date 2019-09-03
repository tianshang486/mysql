# CheckCreateDdrDBInstance {#doc_api_Rds_CheckCreateDdrDBInstance .reference}

Checks whether the data of an RDS instance can be restored to a new RDS instance in a different region by using a cross-region backup set.

This API action is applicable only to the following DB engine versions and editions:

-   MySQL 5.7 High-availability Edition \(with local SSDs\)
-   MySQL 5.6

## Debug {#api_explorer .section}

Use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=CheckCreateDdrDBInstance&type=RPC&version=2014-08-15) to perform debug operations and generate SDK code examples.

## Request parameters {#parameters .section}

|ID|Type|Required|Example value|Description|
|--|----|--------|-------------|-----------|
|Action|String|Yes|CheckCreateDdrDBInstance|The name of this API action. Value: CheckCreateDdrDBInstance.|
|RegionId|String|Yes|cn-hangzhou|The ID of the region to which the destination RDS instance belongs. You can call the [DescribeRegions](~~26243~~) API action to obtain this region ID.|
|Engine|String|Yes|MySQL|The type of the DB engine used by the destination RDS instance. Value: MySQL **Note:** Currently, only the MySQL engine supports cross-region backup.

 |
|DBInstanceClass|String|Yes|rds.mysql.s1.small|The specifications of the destination RDS instance. For more information, see [Instance types](../../../../intl.en-US/Product Introduction/Instance types/Instance types.md#).|
|DBInstanceStorage|Integer|Yes|20| The storage capacity of the destination RDS instance. Value range: **5 to 2000**.

 The parameter value is incremented at a step of 5. Unit: GB. For more information, see [Instance types](../../../../intl.en-US/Product Introduction/Instance types/Instance types.md#).

 |
|EngineVersion|String|Yes|5.6| The version of the DB engine used by the destination RDS instance. Valid values:

 -   **5.6**
-   **5.7**

 |
|RestoreType|String|Yes|0| The restoration method to use. Valid values:

 -   **0**: to restore data based on a specified backup set. You also need to set the **BackupSetID** parameter.
-   **1**: to restore data based on a specified time point. You also need to set the **RestoreTime**, **SourceRegion**, and **SourceDBInstanceName** parameters.

 Default value: **0**.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |
|BackupSetId|String|No|14358| The ID of the backup set used for restoration. You can call the [DescribeCrossRegionBackups](~~121733~~) API action to obtain this backup set ID.

 **Note:** This parameter is required when the **RestoreType**parameter is set to **0**.

 |
|RestoreTime|String|No|2019-05-30T03:29:10Z| The time point from which you want to restore data. This time point must be earlier than the current time. Format: *yyyy-MM-dd*T*HH:mm:ss*Z \(UTC time\).

 **Note:** This parameter is required when the **RestoreType** parameter is set to **1**.

 |
|SourceRegion|String|No|cn-hangzhou| The ID of the region to which the source RDS instance belongs.

 **Note:** This parameter is required when the **RestoreType** parameter is set to **1**.

 |
|SourceDBInstanceName|String|No|rm-uf6wjk5xxxxxxx| The ID of the source RDS instance.

 **Note:** This parameter is required when the **RestoreType** is set to **1**.

 |

## Response parameters {#resultMapping .section}

|ID|Type|Example value|Description|
|--|----|-------------|-----------|
|IsValid|String|true| Whether the destination RDS instance can be created. Valid values: **true | false**.

 |
|RequestId|String|1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC| The ID of the request.

 |

## Examples {#demo .section}

Request example:

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=CheckCreateDdrDBInstance
&RegionId=cn-hangzhou
&Engine=MySQL
&DBInstanceClass=rds.mysql.s1.small
&DBInstanceStorage=20
&EngineVersion=5.6
&RestoreType=0
&BackupSetId=14358
&<CommonParameters>

```

Response example:

`XML` format:

``` {#xml_return_success_demo}
<CheckCreateDdrDBInstanceResponse>
    <IsValid>true</IsValid>
	  <RequestId>346C62D7-8BB9-4516-93E7-25A469EAABCB</RequestId>
</CheckCreateDdrDBInstanceResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"IsValid":"true",
	"RequestId":"346C62D7-8BB9-4516-93E7-25A469EAABCB"
}
```

## Errors {#section_b74_dj6_g3t .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|IncorrectDBInstanceType|Current DB instance engine and type does not support operations.|The error message returned when the current DB engine does not support this API action.|
|400|InvalidRestoreType.Format|Specified restore type is not valid.|The error message returned when the specified restoration method is invalid.|
|400|InvalidBackupType.Format|Specified backup type is not valid.|The error message returned when the specified backup type is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

