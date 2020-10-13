# Clone instance

You can call the CloneDBInstance operation to restore the data of an original ApsaraDB for RDS instance to a new instance. The new instance is called a cloned instance.

Before you call this operation, make sure that the following requirements are met:

-   The original instance must be in the Running state.
-   The original instance cannot have ongoing migration tasks.
-   The log backup function must be enabled on the original instance to support point-in-time recovery \(PITR\).
-   If you want to clone the original instance by using a backup set, the instance must have at least one backup set.

**Note:** ApsaraDB for RDS allows you to create a cloned instance by using the credentials of your RAM user. Make sure that your RAM user is granted the permissions that are required to clone an instance. For more information, see [Use RAM to manage ApsaraDB for RDS permissions](~~58932~~).


Note the following information:

-   The new instance has the same IP address whitelist, security group, SQL Explorer \(SQL Audit\), alert threshold, backup, and parameter settings as the original instance.
-   The data and account information of the new instance is the same as the information that is indicated by the data or log backup file of the original instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates a sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=CloneDBInstance&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CloneDBInstance|The operation that you want to perform. Set the value to **CloneDBInstance**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx|The ID of the new instance. |
|DBInstanceStorageType|String|Yes|cloud\_essd|The storage type of the new instance. Valid values:

-   **local\_ssd**/**ephemeral\_ssd**: local SSD
-   **cloud\_ssd**: standard SSD
-   **cloud\_essd**: enhanced SSD |
|PayType|String|Yes|Postpaid|The billing method of the new instance. Valid values:

-   **Postpaid**: pay-as-you-go
-   **Prepaid**: subscription |
|RegionId|String|No|cn-hangzhou|The ID of the region to which the new instance belongs. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|ZoneId|String|No|cn-hangzhou-b|The ID of the zone to which the new instance belongs. You can call the [DescribeRegions](~~26243~~) operation to query the most recent zone list.

**Note:** The default value is the ID of the zone to which the original instance belongs. |
|DBInstanceClass|String|No|mysql.n1.micro.1|The instance type of the new instance. For more information, see [Primary instance types](~~26312~~).

**Note:** The default value is the instance type of the original instance. |
|DBInstanceStorage|Integer|No|1000|The storage capacity of the new instance. Unit: GB. The storage capacity increases in increments of 5 GB. For more information, see [Primary instance types](~~26312~~).

**Note:** The default value is the storage capacity of the original instance. |
|DbNames|String|No|testDB|The names of the databases that you want to create on the new instance. |
|InstanceNetworkType|String|No|VPC|The network type of the new instance. Valid values:

-   **VPC**
-   **Classic**

**Note:** The default value is the network type of the original instance. |
|BackupId|String|No|9026262|The ID of the backup set that you want to use.

You can call the [DescribeBackups](~~26273~~) operation to query the most recent backup set list.

**Note:** You must specify at least one of the **BackupId** and **RestoreTime** parameters. |
|RestoreTime|String|No|2011-06-11T16:00:00Z|The point in time to which you want to restore the data of the original instance. The point in time must fall within the specified log backup retention period. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

**Note:** You must specify at least one of the **BackupId** and **RestoreTime** parameters. |
|VPCId|String|No|vpc-uf6f7l4fg90xxxxxxxxxx|The ID of the VPC to which the new instance belongs.

**Note:** Make sure that the VPC resides in the specified region. |
|VSwitchId|String|No|vsw-uf6adz52c2pxxxxxxxxxx|The ID of the VSwitch associated with the specified VPC.

**Note:** Make sure that the VSwitch belongs to the specified VPC and region. |
|PrivateIpAddress|String|No|172.16.201.69|The private IP address of the new instance. The private IP address must fall within the Classless Inter-Domain Routing \(CIDR\) block that is supported by the specified VSwitch. The system automatically assigns an IP address based on the **VPCId** and **VSwitchId** parameters. |
|UsedTime|Integer|No|1|The subscription period of the new instance if the new instance uses subscription billing. Valid values:

-   If you set the **Period** parameter to **Year**, the value of the UsedTime parameter ranges from **1 to 3**.
-   If you set the **Period** parameter to **Month**, the value of the UsedTime parameter ranges from **1 to 9**.

**Note:** This parameter must be specified if the PayType parameter is set to **Prepaid**. |
|Period|String|No|Year|The renewal period of the new instance if the new instance uses subscription billing. Valid values:

-   **Year**
-   **Month**

**Note:** This parameter must be specified if the PayType parameter is set to **Prepaid**. |
|Category|String|No|HighAvailability|The RDS edition of the new instance. Valid values:

-   **Basic**: Basic Edition
-   **HighAvailability**: High-availability Edition
-   **AlwaysOn**: Cluster Edition
-   **Finance**: Enterprise Edition |
|RestoreTable|String|No|1|Specifies whether to restore specific databases and tables. The value **1** specifies to restore specific databases and tables. If you do not want to restore specific databases or tables, you can choose not to specify this parameter. |
|TableMeta|String|No|\[\{"type":"db","name":"testdb1","newname":"testdb1\_new","tables":\[\{"type":"table","name":"testdb1table1","newname":"testdb1table1\_new"\}\]\}\]|The information about the databases and tables that you want to restore. Format:

```
[{"type":"db","name":"The original name of Database 1","newname":"The new name of Database 1","tables":[{"type":"table","name":"The original name of Table 1 in Database 1","newname":"The new name of Table 1 in Database 1"},{"type":"table","name":"The original name of Table 2 in Database 1","newname":"The new name of Table 2 in Database 1"}]},{"type":"db","name":"The original name of Database 2","newname":"The new name of Database 2","tables":[{"type":"table","name":"The original name of Table 1 in Database 2","newname":"The new name of Table 1 in Database 2"},{"type":"table","name":"The original name of Table 2 in Database 2","newname":"The new name of Table 2 in Database 2"}]}]
``` |
|DedicatedHostGroupId|String|No|dhg-7a9xxxxxxxx|The ID of the dedicated cluster to which the new instance belongs if you create the new instance in a dedicated cluster. |
|BackupType|String|No|FullBackup|The type of backup used by the new instance. Valid values:

-   **FullBackup**: full backup
-   **IncrementalBackup**: incremental backup |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the new instance. |
|OrderId|String|100789370xxxxx|The ID of the order. |
|RequestId|String|1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=CloneDBInstance
&PayType=Postpaid
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&DBInstanceStorageType=cloud_essd
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CloneDBInstanceResponse>
      <OrderId>100789370xxxxx</OrderId>
      <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
      <RequestId>1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC</RequestId>
</CloneDBInstanceResponse>
```

`JSON` format

```
{
    "OrderId": "100789370xxxxx",
    "DBInstanceId": "rm-uf6wjk5xxxxxxx",
    "RequestId": "1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

