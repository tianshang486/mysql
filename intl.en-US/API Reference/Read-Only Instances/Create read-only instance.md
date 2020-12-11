# Create read-only instance

You can call the CreateReadOnlyDBInstance operation to create a read-only instance for a primary ApsaraDB RDS instance.

**Before you call this operation, make sure that the following requirements are met:**

-   The primary instance must not belong to a dedicated cluster and must run one of the following database engine versions and RDS editions:
    -   MySQL 8.0 on RDS High-availability or Enterprise Edition
    -   MySQL 5.7 on RDS High-availability or Enterprise Edition
    -   MySQL 5.6
    -   SQL Server 2017 on RDS Cluster Edition
    -   PostgreSQL 10, 11, or 12 with local SSDs
-   If the primary instance runs MySQL, the number of existing read-only instances does not reach the specified limit:
    -   If the memory capacity of the primary instance is greater than or equal to 64 GB, up to 10 read-only instances are allowed.
    -   If the memory capacity of the primary instance is less than 64 GB, up to 5 read-only instances are allowed.
-   If the primary instance runs SQL Server, the number of existing read-only instances does not reach 7.
-   If the primary instance runs PostgreSQL with local SSDs, the number of existing read-only instances does not reach 5. If the primary instance runs PostgreSQL with standard or enhanced SSDs, the number of existing read-only instances does not reach 32.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=CreateReadOnlyDBInstance&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateReadOnlyDBInstance|The operation that you want to perform. Set the value to **CreateReadOnlyDBInstance**. |
|DBInstanceClass|String|Yes|rds.mys2.small|The type of the read-only instance. For more information, see [Primary instance types](~~26312~~). We recommend that the specifications of the read-only instance be higher than or equal to those of the primary instance. If the specifications of the read-only instance are lower than those of the primary instance, the read-only instance may encounter high latency or heavy load issues. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the primary instance. |
|DBInstanceStorage|Integer|Yes|20|The storage capacity of the read-only instance. Valid values: **5 to 3000**. The value of this parameter must be a multiple of 5. Unit: GB.

**Note:** The supported storage capacity range varies based on the used RDS edition. For more information, go to the ApsaraDB RDS console. |
|EngineVersion|String|Yes|5.6|The version of the database engine that the read-only instance runs. The read-only instance must use the same database engine version as the primary instance.

-   If the read-only instance runs MySQL, set the value to one of the following values:
    -   **5.6**
    -   **5.7**
    -   **8.0**
-   If the read-only instance runs SQL Server, set the value to **2017\_ent**. |
|PayType|String|Yes|Postpaid|The billing method of the read-only instance. Valid value:

-   **Postpaid**: pay-as-you-go
-   **Prepaid**: subscription |
|RegionId|String|Yes|cn-hangzhou|The region ID of the read-only instance. The read-only instance must reside in the same region as the primary instance. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|ZoneId|String|Yes|cn-hangzhou-b|The zone ID of the read-only instance. You can call the [DescribeRegions](~~26243~~) operation to query the most recent zone list. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|DBInstanceDescription|String|No|Read-only instance for test|The description of the read-only instance. The description must be 2 to 256 characters in length. It can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter.

**Note:** The description cannot start with http:// or https://. |
|InstanceNetworkType|String|No|Classic|The network type of the read-only instance. Valid values:

-   **VPC**
-   **Classic**

Default value: VPC. If you set this parameter to VPC, you must also specify the **VPCId** and **VSwitchId** parameters. |
|VPCId|String|No|vpc-uf6f7l4fg90xxxxxxxxxx|The ID of the VPC to which the read-only instance belongs. |
|VSwitchId|String|No|vsw-uf6adz52c2pxxxxxxxxxx|The ID of the vSwitch associated with the specified VPC. |
|PrivateIpAddress|String|No|172.16.201.69|The private IP address of the read-only instance. The private IP address must fall within the Classless Inter-Domain Routing \(CIDR\) block that is supported by the specified vSwitch. The system automatically assigns a private IP address based on the **VPCId** and **VSwitchId** parameters. |
|ResourceGroupId|String|No|rg-acfmyxxxxxxxxxx|The ID of the resource group to which the read-only instance belongs. |
|Category|String|No|HighAvailability|The RDS edition of the read-only instance. Valid values:

-   **Basic**: the RDS Basic Edition.
-   **HighAvailability**: the RDS High-availability Edition.
-   **AlwaysOn**: the RDS Cluster Edition.
-   **Finance**: the RDS Enterprise Edition.

**Note:** If the primary instance runs PostgreSQL with standard or enhanced SSDs, you must set this parameter to **Basic**. |
|DBInstanceStorageType|String|No|local\_ssd|The type of storage media that is used by the read-only instance. Valid values:

-   **local\_ssd** or **ephemeral\_ssd**: local SSD.
-   **cloud\_ssd**: standard SSD.
-   **cloud\_essd**: enhanced SSD.

**Note:** MySQL only supports local SSDs, whereas SQL Server supports both standard and enhanced SSDs. |
|DedicatedHostGroupId|String|No|dhg-4nxxxxxxx|The ID of the dedicated cluster to which the primary instance belongs if you create the read-only instance in a dedicated cluster. |
|TargetDedicatedHostIdForMaster|String|No|i-bpxxxxxxx1|The ID of the host to which the primary instance belongs if you create the read-only instance in a dedicated cluster. |
|GdnInstanceName|String|No|None|A hidden parameter. |
|TddlBizType|String|No|None|A hidden parameter. |
|TddlRegionConfig|String|No|None|A hidden parameter. |
|InstructionSetArch|String|No|None|A hidden parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rr-uf6wjk5xxxxxxx|The ID of the read-only instance. |
|OrderId|String|10078937xxxxx|The ID of the order. |
|ConnectionString|String|rr-xxxxx.mysql.rds.aliyuncs.com|The internal endpoint of the read-only instance. |
|Port|String|3306|The internal port of the read-only instance. |
|RequestId|String|1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=CreateReadOnlyDBInstance
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-b
&DBInstanceId=rm-uf6wjk5xxxxxxx
&DBInstanceClass=rds.mys2.small
&DBInstanceStorage=20
&EngineVersion=5.6
&PayType=Postpaid
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateReadOnlyDBInstanceResponse>
     <OrderId>10078937xxxxx</OrderId>
     <ConnectionString>rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com </ConnectionString>
     <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
     <port>3306</port>
     <RequestId>1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC</RequestId>
</CreateReadOnlyDBInstanceResponse>
```

`JSON` format

```
{
    "OrderId": "10078937xxxxx",
    "ConnectionString": "rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com",
    "DBInstanceId": "rm-uf6wjk5xxxxxxx",
    "Port": "3306",
    "RequestId": "1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC"
}
```

## Error codes

|HTTP Status Code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidEngineVersion.Malformed|The specified parameter "EngineVersion" is not valid.|The error message returned because the specified EngineVersion parameter is invalid.|
|400|InvalidSecurityIPList.Malformed|The specified parameter "SecurityIPList" is not valid.|The error message returned because the specified SecurityIPList parameter is invalid.|
|400|InvalidSecurityIPList.Duplicate|The Security IP address is not in the available range or occupied.|The error message returned because the specified IP address is in use or is not within the valid range.|
|400|InvalidParameter|The specified parameter "dbInstanceId" is not valid.|The error message returned because the specified DBInstanceId parameter is invalid.|
|403|OperationDenied.PrimaryDBInstanceStatus|The operation is not permitted due to status of primary instance.|The error message returned because the status of the primary instance does not support this operation. The primary instance supports this operation only when it is in the Running state.|
|400|OperationDenied|VPC IP is in use, please check.|The error message returned because the specified private IP address is in use. Change the private IP address and try again.|
|404|IncorrectDBInstanceConnType|Current DB instance conn type does not support this operation.|The error message returned because the connection type of the primary instance does not support this operation.|
|400|InvalidZoneId.NotSupported|The Specified vpc Zone not supported.|The error message returned because the specified zone does not support instances that reside in VPCs. Change the zone and try again.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

