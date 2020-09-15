# Create disaster recovery instance

Restores the data of an RDS instance to a new RDS instance in a different region.

Before the data restoration, you can call the [CheckCreateDdrDBInstance](~~121721~~) API action to check whether the source RDS instance supports cross-region backup and restoration.

This API action is applicable only to the following DB engine versions and editions:

-   MySQL 8.0 High-availability Edition \(with local SSDs\)
-   MySQL 5.7 High-availability Edition \(with local SSDs\)
-   MySQL 5.6

## Debug

Use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=CreateDdrInstance&type=RPC&version=2014-08-15) to perform debug operations and generate SDK code examples.

## Request parameters

|ID|Type|Required|Example value|Description|
|--|----|--------|-------------|-----------|
|Action|String|Yes|CreateDdrInstance|The name of this API action. Value: **CreateDdrInstance**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region to which the destination RDS instance belongs. You can call the [DescribeRegions](~~26243~~) API action to obtain this region ID. |
|Engine|String|Yes|MySQL|The type of the DB engine used by the destination RDS instance. Value: **MySQL**. |
|EngineVersion|String|Yes|5.6|The version of the DB engine used by the destination RDS instance. Valid values:

-   **5.6**
-   **5.7**
-   **8.0** |
|DBInstanceClass|String|Yes|rds.mysql.s1.small|The specifications of the destination RDS instance. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).|
|DBInstanceStorage|Integer|Yes|20|The storage capacity of the destination RDS instance. Value range: **5 to 2000**.

The value is incremented by a step of 5. Unit: GB. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). |
|DBInstanceNetType|String|Yes|Intranet|The type of network connection to be used by the destination RDS instance. Valid values:

-   **Internet**
-   **Intranet** |
|PayType|String|Yes|Prepaid|The billing method to be used by the destination RDS instance. Valid values:

-   **Postpaid**: to use the Pay-As-You-Go billing method.
-   **Prepaid**: to use the Subscription billing method. |
|RestoreType|String|Yes|0|The restoration method to use. Valid values:

-   **0**: to restore data based on a specified backup set. You also need to set the **BackupSetId** parameter.
-   **1**: to restore data based on a specified time point. You also need to set the **RestoreTime**, **SourceRegion**, and **SourceDBInstanceName** parameters. |
|SecurityIPList|String|Yes|127.0.0.1|The [IP address whitelist](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.md) of the destination RDS instance. If the IP address whitelist contains more than one IP address, separate these IP addresses by using commas \(,\). Duplicate IP addresses are not allowed. Up to 1,000 IP addresses can be entered. Formats: -   IP address, for example, 10.23.12.24.
-   CIDR, for example, 10.23.12.24/24 \(24 indicates the length of the prefix in the IP address, and the prefix length ranges from 1 to 32\). |
|InstanceNetworkType|String|No|Classic|The type of network to which the destination RDS instance belongs. Valid values:

-   **VPC**
-   **Classic**

By default, the destination RDS instance is created on a classic network.

**Note:** When you set this parameter to **VPC**, you also need to set the **VpcId** and **VSwitchId** parameters. |
|ZoneId|String|No|cn-hangzhou-b|The ID of the zone to which the destination RDS instance belongs. If the destination RDS instance belongs to more than one zone, separate these zones by using colon \(:\).

**Note:** When you specify a VPC and a VSwitchd, you must also set this parameter to match the zone to which the VSwitch belongs. |
|VPCId|String|No|vpc-xxxxxxxxxxxx|The ID of the VPC to which the destination RDS instance belongs. This parameter is available when you set the **InstanceNetworkType** parameter to **VPC**.

**Note:** If you set this parameter, you must also set the **ZoneId** parameter. |
|DBInstanceStorageType|String|No|local\_ssd|The storage class of the destination RDS instance. Currently, only local SSDs are supported. Default value: **local\_ssd**. |
|VSwitchId|String|No|vsw-xxxxxxxxxxx|The ID of the VSwitch to be used by the destination RDS instance. If the destination RDS instance is to connect more than one VSwitch, separate these VSwitches by using commas \(,\). This parameter is available when you set the **InstanceNetworkType** parameter to **VPC**.

**Note:** If you set this parameter, you must also set the **ZoneId** parameter. |
|AccessKeyId|String|No|LTAIfCxxxxxxx|The AccessKey ID issued by Alibaba Cloud for users to access services. |
|ConnectionMode|String|No|Standard|The access mode to be used by the destination RDSinstance. Valid values:

-   **Standard**: the standard mode.
-   **Safe**: the database proxy mode.

Default value: **Standard**. |
|SystemDBCharset|String|No|uft8|The character set to be used by the destination RDS instance. Valid values:

-   **utf8**
-   **gbk**
-   **latin1**
-   **utf8mb4** |
|DBInstanceDescription|String|No|Test Database|The name of the destination RDS instance. The name must start with a letter and can contain 2 to 256 characters, including letters, digits, hyphens \(-\), and underscores \(\_\).

**Note:** It cannot start with http:// or https://. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to guarantee the idempotency of requests. The client token is generated by the client and is unique among different requests. It is a string of up to 64 ASCII characters. |
|PrivateIpAddress|String|No|172.16.201.69|The private IP address of the destination RDS instance. This private IP address must be within the IP address range of a specified VSwitch. By default, this private IP address is assigned by the system according to the values of the **VPCId** and **VSwitchId** parameters. |
|Period|String|No|Year|The duration of purchase if the destination RDS instance uses the Subscription billing method. Valid values:

-   **Year**: one year.
-   **Month**: one month.

**Note:** This parameter is required when the PayType parameter is set to **Prepaid**. |
|BackupSetId|String|No|14358|The ID of the backup set used for data restoration. You can call the [DescribeCrossRegionBackups](~~121733~~) API action to obtain this backup set ID.

**Note:** This parameter is required when you set the **RestoreType** parameter to **0**. |
|SourceDBInstanceName|String|No|rm-uf6wjk5xxxxxxx|The ID of the source RDS instance when you choose to restore data by time.

**Note:** This parameter is required when you set the **RestoreType** parameter to **1**. |
|SourceRegion|String|No|cn-hangzhou|The ID of the region to which the source RDS instance belongs when you choose to restore data by time.

**Note:** This parameter is required when you set the **RestoreType** parameter to **1**. |
|RestoreTime|String|No|2019-05-30T03:29:10Z|The time point from which you want to restore data. This time point must be earlier than the current time. Format: *yyyy-MM-dd*T*HH:mm:ss*Z \(UTC time\).

**Note:** This parameter is required when you set the **RestoreType** parameter to **1**. |
|UsedTime|String|No|2|The duration of purchase. Valid values:

-   When you set the **Period** parameter to **Year**, the value of the UsedTime parameter ranges from **1 to 3**.
-   When you set the **Period** parameter to **Month**, the value of the UsedTime parameter ranges from **1 to 9**.

**Note:** This parameter is required when you set the PayType parameter to **Prepaid**. |
|ResourceGroupId|String|No|Rg-acfmyxxxxxxxxxx|The ID of the resource group to use. |

## Response parameters

|ID|Type|Example value|Description|
|--|----|-------------|-----------|
|DBInstanceId|String|rm-xxxxx|The ID of the destination RDS instance. |
|ConnectionString|String|rm-xxxxx.mysql.rds.aliyuncs.com|The endpoint for connecting the destination RDS instance.

**Note:** The **DBInstanceNetType** parameter determines whether you enter an internal or public endpoint. |
|OrderId|String|2038691xxxxx|The ID of the order for purchasing the destination RDS instance. |
|Port|String|3306|The port for connecting the destination RDS instance instance.

**Note:** The **DBInstanceNetType** parameter determines whether you enter an internal or public port. |
|RequestId|String|E52666CC-330E-418A-8E5B-A19E3FB42D13|The ID of the request. |

## Examples

Request example:

```

http(s)://rds.aliyuncs.com/? Action==CreateDdrInstance
&RegionId=cn-hangzhou
&Engine=MySQL
&EngineVersion=5.6
&DBInstanceClass=rds.mysql.s1.small
&DBInstanceStorage=20
&DBInstanceNetType=Intranet
&PayType=Prepaid
&RestoreType=0
&SecurityIPList=127.0.0.1
&BackupSetId=14358
&<Common request parameters>

```

Response example:

`XML` format:

```
<CreateDdrInstanceResponse>
  <ConnectionString>rm-xxxxx.mysql.rds.aliyuncs.com</ConnectionString>
	  <Port>3306</Port>
	  <RequestId>E52666CC-330E-418A-8E5B-A19E3FB42D13</RequestId>
	  <DBInstanceId>rm-xxxxx</DBInstanceId>
	  <OrderId>2038691xxxxx</OrderId>
</CreateDdrInstanceResponse>
```

`JSON` format:

```
{
	"Port":"3306",
	"ConnectionString":"rm-xxxxx.mysql.rds.aliyuncs.com",
	"OrderId":"2038691xxxxx",
	"DBInstanceId":"rm-xxxxx",
	"RequestId":"E52666CC-330E-418A-8E5B-A19E3FB42D13"
}
```

## Errors

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidZoneId.NotSupported|The Specified vpc Zone not supported.|The error message returned when the specified zone does not support RDS instances that run in VPCs. You can try another zone.|
|400|InvalidDBInstanceName.Format|Specified DB instance name is not valid.|The error message returned when the specified RDS instance name is incorrect.|
|400|InvalidServiceType.Format|Specified service type is not valid.|The error message returned when the specified service type is invalid.|
|400|InvalidEngine.Malformed|Specified engine is not valid.|The error message returned when the specified DB engine is invalid.|
|400|InvalidEngineVersion.Malformed|Specified engine version is not valid.|The error message returned when the specified DB engine version is invalid.|
|400|InvalidConnectionString.Format|Specified connection string is not valid.|The error message returned when the specified endpoint is invalid.|
|400|InvalidConnectionString.Duplicate|Specified connection string already exists in the Aliyun RDS.|The error message returned when the specified endpoint already exists in Alibaba Cloud ApsaraDB for RDS.|
|400|InvalidCharacterSetName.Format|Specified character set name is not valid.|The error message returned when the specified character set name is invalid.|
|400|InvalidDBInstanceType.Format|Specified instance type is not valid.|The error message returned when the specified instance type is invalid.|
|400|InvalidPort.Malformed|Specified port is not valid.|The error message returned when the specified port number is invalid.|
|400|InvalidBackupRetentionPeriod.Malformed|Specified backup retention period is not valid.|The error message returned when the specified backup set retention period is invalid.|
|400|InvalidPreferredBackupTime.Format|Specified preferred backup time is not valid.|The error message returned when the specified backup time point is invalid.|
|400|InvalidPreferredBackupPeriod.Malformed|Specified backup period is not valid.|The error message returned when the specified backup time point is invalid.|
|404|InvalidDBInstanceClass.NotFound|Specified DB instance class is not found.|The error message returned when the specified instance specifications are invalid. Check whether the DBInstanceClass parameter is correctly set.|
|404|InvalidDBInstanceNetType.NotFound|Specified DB instance net type is not found.|The error message returned when the specified network type does not exist.|
|400|InvalidOptmizationService|Specified optmization service is not valid.|The error message returned when the OptmizationService parameter is invalid.|
|400|InvalidExpiredTime.Format|Specified expired time is not valid.|The error message returned when the specified expiration time is invalid.|
|400|InvalidSecurityIPList.Format|Specified security IP list format is not valid.|The error message returned when the format of the specified IP address whitelist is invalid.|
|400|InvalidSecurityIPList.QuotaExceeded|Specified security IP list is not valid: Exceeding the allowed amount of IP address in the list.|The error message returned when the number of IP addresses in the specified IP address whitelist exceeds the upper limit.|
|400|InvalidDBInstanceDescription.Format|Specified Bgp Group description is not valid.|The error message returned when the description of the destination RDS instance is invalid.|
|400|InvalidStorage.Format|Specified Storage is not valid.|The error message returned when the Storage parameter is invalid.|
|400|IncorrectDBInstanceType|Current DB instance engine and type does not support operations.|The error message returned when the specified DB engine type does not support this API action.|
|400|InvalidRestoreType.Format|Specified restore type is not valid.|The error message returned when the specified restoration type is invalid.|
|400|InvalidBackupType.Format|Specified backup type is not valid.|The error message returned when the specified backup type is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

