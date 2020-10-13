# Switch the network isolation mode from standard whitelist to enhanced whitelist

Switches the network isolation mode from standard whitelist to enhanced whitelist.

-   In standard whitelist mode, IP addresses in the whitelist apply to both the classic network and VPCs. To minimize security risks, we recommend that you switch to the enhanced whitelist mode.
-   In enhanced whitelist mode, IP addresses in the whitelist are divided into VPC IP addresses and IP addresses of the classic network and Internet.

**Note:**

-   The enhanced whitelist mode cannot be switched back to the standard whitelist mode.
-   This operation is not applicable to instances that run SQL Server and MariaDB.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=MigrateSecurityIPMode&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|MigrateSecurityIPMode|The operation that you want to perform. Set the value to **MigrateSecurityIPMode**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|RequestId|String|EF1E53AB-5625-49C7-ADF1-FBD0B6640D19|The ID of the request. |
|SecurityIPMode|String|safety|The network isolation mode after the switching. Valid value: **safety**, which indicates the enhanced whitelist mode. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=MigrateSecurityIPMode
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<MigrateSecurityIPModeResponse>
	  <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
	  <RequestId>EF1E53AB-5625-49C7-ADF1-FBD0B6640D19</RequestId>
	  <SecurityIPMode>safety</SecurityIPMode>
</MigrateSecurityIPModeResponse>
```

`JSON` format

```
{
    "DBInstanceId": "rm-uf6wjk5xxxxxxx",
    "RequestId": "EF1E53AB-5625-49C7-ADF1-FBD0B6640D19",
    "SecurityIPMode": "safety"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

