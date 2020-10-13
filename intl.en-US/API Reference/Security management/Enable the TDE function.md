# Enable the TDE function

Enables the Transparent Data Encryption \(TDE\) function for an ApsaraDB for RDS instance.

TDE performs real-time I/O encryption and decryption on data files. Data can be encrypted before being written to a disk and decrypted when read to memory. For more information, see [TDE](~~96121~~).

Before you call this operation, make sure that the following requirements are met:

-   Alibaba Cloud Key Management Service \(KMS\) is activated. If KMS is not activated, you can activate it when you enable TDE.
-   The instance runs one of the following database engines and RDS editions:
    -   MySQL 5.6
    -   MySQL 5.7 in the High-availability Edition \(with local SSDs\)
    -   SQL Server in the Enterprise Edition

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceTDE&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceTDE|The operation that you want to perform. Set the value to **ModifyDBInstanceTDE**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|TDEStatus|String|Yes|Enabled|Specifies whether to enable the TDE function. Valid values: **Enabled \| Disabled** |
|DBName|String|No|testDB|The name of the database for which you want to enable the TDE function. A maximum of 50 database names can be entered in a single request. The names must be separated with commas \(,\).

**Note:** This parameter can be specified only for instances that run SQL Server in the Enterprise Edition. |
|EncryptionKey|String|No|749c1df7-xxxx-xxxx-xxxx-xxxxxxxxxxxx|The ID of the custom key.

**Note:** This parameter can be specified only for instances that run MySQL. |
|RoleArn|String|No|acs:ram::1406926xxxxx:role/aliyunrdsinstanceencryptiondefaultrole|The Alibaba Cloud Resource Name \(ARN\) of the role. An ARN is the global resource identifier of a role. For more information, see [RAM role overview](~~93689~~).

**Note:** This parameter can be specified only for instances that run MySQL. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|777C4593-8053-427B-99E2-105593277CAB|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyDBInstanceTDE
&DBInstanceId=rm-uf6wjk5xxxxxxx
&TDEStatus=Enabled
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBInstanceTDEResponse>
      <requestId>777C4593-8053-427B-99E2-105593277CAB</requestId>
</ModifyDBInstanceTDEResponse>
```

`JSON` format

```
{
    "requestId": "777C4593-8053-427B-99E2-105593277CAB"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

