# ModifyDBInstanceTDE {#doc_api_Rds_ModifyDBInstanceTDE .reference}

You can call this operation to modify the data encryption status of an instance.

This operation is used to configure [TDE](../../../../intl.en-US/User Guide/Security/Set TDE.md#) for an instance.

-   Encryption keys are created and managed by the Key Management Service \(KMS\). RDS does not provide the keys and certificates needed for encryption. After enabling TDE, you must decrypt the data through RDS if you want to restore the data to the local server.
-   Before enabling TDE, you must activate KMS. If you do not activate KMS, you can activate it as instructed when enabling TDE.
-   For SQL Server Enterprise Edition, TDE can be enabled and disabled only at the database level.
-   For MySQL 5.6, TDE cannot be disabled after being enabled.
-   After TDE is enabled, CPU usage increases.

**Note:** This operation is applicable only to MySQL 5.6 and SQL Server Enterprise Edition instances.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceTDE) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceTDE| The operation that you want to perform. Set this parameter to ModifyDBInstanceTDE.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|TDEStatus|String|Yes|Enabled| The TDE status. Valid values: Enabled | Disabled.

 |
|DBName|String|No|testDB| The name of the database with TDE enabled. Up to 50 database names can be entered in a single request. These names must be separated with commas \(,\).

 **Note:** This parameter is required only for SQL Server Enterprise Edition instances.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|777C4593-8053-427B-99E2-105593277CAB| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=ModifyDBInstanceTDE
&DBInstanceId=rm-uf6wjk5xxxxxxx
&TDEStatus=Enabled
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_8k5_h3c_v5t}
<ModifyDBInstanceTDEResponse>
	  <requestId>777C4593-8053-427B-99E2-105593277CAB</requestId></ModifyDBInstanceTDEResponse>
```

`JSON` format

``` {#codeblock_p3a_571_gvk}
{
	"requestId":"777C4593-8053-427B-99E2-105593277CAB"
}
```

## Error codes {#section_m88_f7i_937 .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

