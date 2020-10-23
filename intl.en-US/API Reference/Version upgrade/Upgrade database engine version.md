# Upgrade database engine version

You can call the UpgradeDBInstanceEngineVersion operation to upgrade the database engine version of an ApsaraDB RDS instance.

**Note:** The fee that you must pay after the upgrade varies based on the new and old instance types and storage types.

If the instance is a primary instance that is attached with a read-only or disaster recovery instance, you must upgrade the database engine version of the read-only or disaster recovery instance before you upgrade the database engine version of the primary instance.

Before you call this operation, make sure that the following requirements are met:

-   The instance must be in the Running state.
-   The source database engine version must be MySQL 5.5, and the destination database engine version must be MySQL 5.6.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=UpgradeDBInstanceEngineVersion&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpgradeDBInstanceEngineVersion|The operation that you want to perform. Set the value to **UpgradeDBInstanceEngineVersion**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|EngineVersion|String|Yes|5.6|The destination database engine version to which you want to upgrade the instance. Valid values: **5.6**. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|EffectiveTime|String|No|Immediate|The time when you want the upgrade to take effect. Valid values:

-   **Immediate**: The upgrade takes effect immediately.
-   **MaintainTime**: The upgrade takes effect during the specified maintenance window. For more information, see [ModifyDBInstanceMaintainTime](~~26249~~).

Default value: **Immediate**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|TaskId|String|10254125|The ID of the upgrade task. |
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=UpgradeDBInstanceEngineVersion
&DBInstanceId=rm-uf6wjk5xxxxxxx
&EngineVersion=5.6
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpgradeDBInstanceEngineVersionResponse>
      <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
      <TaskId>10254125</TaskId></UpgradeDBInstanceEngineVersionResponse>
```

`JSON` format

```
{
    "RequestId": " 65BDA532-28AF-4122-AA39-B382721EEE64",
    "TaskId": "10254125"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

