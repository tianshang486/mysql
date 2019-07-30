# UpgradeDBInstanceEngineVersion {#doc_api_1105914 .reference}

You can call this operation to upgrade the database version of the instance.

**Note:** The price for the upgrade is calculated based on the new and old instance types and storage types.

If the primary instance is attached with a read-only or disaster recovery instance, first upgrade the database version of the attached instance.

This operation must meet the following requirements:

-   The instance is in the running state.
-   You can upgrade a database from MySQL 5.5 to MySQL 5.6.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=UpgradeDBInstanceEngineVersion) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpgradeDBInstanceEngineVersion| The operation that you want to perform. Set the value to **UpgradeDBInstanceEngineVersion**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|EngineVersion|String|Yes|5.6| The version of the target database. Valid values:**5.6**.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxxxxx| The AccessKey ID that Alibaba Cloud issues to a user for service access.

 |
|EffectiveTime|String|No|Immediate| The time when the upgrade takes effect. Valid values:

 -   **Immediate**: The upgrade takes effect immediately.
-   **MaintainTime**: The upgrade takes effect during the maintenance period. You can call [ModifyDBInstanceMaintainTime](~~26249~~) to view the information about the maintenance period.

 Default value: **Immediate**.

 |
|DBInstanceClass|String|No|mssql.x4.medium.s2| The type of the target instance. For more information, see [Instance types](~~26312~~). MySQL is optional, and SQL Server is required.

 |
|DBInstanceStorageType|String|No|cloud\_ssd| The type of the target storage. MySQL is optional, and SQL Server is required. Valid values:

 -   **local\_ssd/ephemeral\_ssd**: local SSD
-   **cloud\_ssd**: cloud SSD
-   **cloud\_essd**: cloud ESSD

 |
|ZoneId|String|No|cn-hangzhou-b| The ID of the target zone. The target zone has the same ID as the zone where the instance is located by default.

 |
|InstanceNetworkType|String|No|VPC| The target network type. MySQL is optional, and SQL Server is required. Valid values:

 -   **VPC**
-   **Classic**

 |
|VpcId|String|No|vpc-xxxxxxxxxxxx| The ID of the target VPC. MySQL is optional, and SQL Server is required.

 |
|VSwitchId|String|No|vsw-xxxxxxxxxxx| The ID of the target VSwitch. MySQL is optional, and SQL Server is required.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|TaskId|String|10254125| The ID of the task.

 |
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=UpgradeDBInstanceEngineVersion
&DBInstanceId=rm-uf6wjk5xxxxxxx
&EngineVersion=5.6 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<UpgradeDBInstanceEngineVersionResponse> 
  <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
  <TaskId>10254125</TaskId>
</UpgradeDBInstanceEngineVersionResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64",
	"TaskId":"10254125"
}
```

## Error codes {#section_n4m_6y7_z8c .section}

[View error codes](https://error-center.aliyun.com/status/product/Rds)

