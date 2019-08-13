# ModifyDBInstanceConnectionMode {#doc_api_1094269 .reference}

You can call this operation to enable or disable the database proxy.

**Note:** This operation is deprecated.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceConnectionMode) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceConnectionMode| The operation that you want to perform. Set this parameter to ModifyDBInstanceConnectionMode.

 |
|ConnectionMode|String|Yes|Performance| The access mode of the instance. Valid values:

-   Performance: standard mode.
-   Safe: safe mode.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxx| The name of the instance.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID that Alibaba Cloud issues to a user for service access.

 |
|OwnerAccount|String|No|testuser@aliyun.com| The Apsara Stack tenant account.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=ModifyDBInstanceConnectionMode
&ConnectionMode=Performance 
&DBInstanceId=rm-uf6wjk5xxxxxx 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_3e6_jec_rfy}
<ModifyDBInstanceConnectionModeResponse>
	  <RequestId>D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD</RequestId></ModifyDBInstanceConnectionModeResponse>
```

`JSON` format

``` {#codeblock_93t_iz0_rsz}
{
	"RequestId":"D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD"
}
```

## Error codes {#section_zyf_vqp_y2c .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

