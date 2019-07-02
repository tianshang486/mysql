# MigrateSecurityIPMode {#doc_api_1106076 .reference}

You can call this operation to switch a whitelist from normal mode to safe mode.

-   In normal mode, IP addresses in the whitelist apply to both classic networks and VPCs. In case of security risks, we recommend that you switch to safe mode.
-   In safe mode, IP addresses in the whitelist are divided into VPC IP addresses and the IP addresses of classic networks and public networks.

**Note:** 

-   Safe mode cannot be switched to normal mode.
-   This operation is not applicable to SQL Server and MariaDB instances.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=MigrateSecurityIPMode) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|MigrateSecurityIPMode|The operation that you want to perform. Set the value to **MigrateSecurityIPMode**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx|The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance.

 |
|RequestId|String|EF1E53AB-5625-49C7-ADF1-FBD0B6640D19|The ID of the request.

 |
|SecurityIPMode|String|safety|The mode of the whitelist after the switch. Valid values: **safety**.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=MigrateSecurityIPMode
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<MigrateSecurityIPModeResponse>
  <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
  <RequestId>EF1E53AB-5625-49C7-ADF1-FBD0B6640D19</RequestId> 
  <SecurityIPMode>safety</SecurityIPMode>
</MigrateSecurityIPModeResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"EF1E53AB-5625-49C7-ADF1-FBD0B6640D19",
	"DBInstanceId":"rm-uf6wjk5xxxxxxx",
	"SecurityIPMode":"safety"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Rds)

