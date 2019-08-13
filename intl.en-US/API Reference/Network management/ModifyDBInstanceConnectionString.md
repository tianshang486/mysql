# ModifyDBInstanceConnectionString {#doc_api_Rds_ModifyDBInstanceConnectionString .reference}

You can call this operation to modify the connection address and port of an instance.

RDS provides two types of connection addresses: private IP addresses and public IP addresses. RDS also allows a VPC and a classic network to coexist in the hybrid access mode.

**Note:** 

-   Only the prefix of the connection address can be modified.
-   The read/write splitting address cannot be modified.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceConnectionString) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceConnectionString| The operation that you want to perform. Set this parameter to ModifyDBInstanceConnectionString.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|CurrentConnectionString|String|Yes|rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com| The current connection address of an instance. It can be an internal network address, a public network address, or a classic network address in the hybrid access mode.

 **Note:** The read/write splitting address cannot be modified.

 |
|ConnectionStringPrefix|String|Yes|m-xxxxbn5c23qo| The prefix of the target connection address. Only the prefix of CurrentConnectionString can be modified.

 **Note:** It must be 5 to 30 characters in length and can contain letters, digits, and hyphens \(-\). It cannot contain Chinese characters and the following special characters:

~ ! \# % ^ & \* = + \\ | \{ \} ; : ' " , < \> / ?

 |
|Port|String|Yes|3306| The target port.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=ModifyDBInstanceConnectionString
&DBInstanceId=rm-uf6wjk5xxxxxxx
&CurrentConnectionString=rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com
&ConnectionStringPrefix=m-xxxxbn5c23qo 
&Port=3306
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_lm8_y55_ohm}
<PurgeDBInstanceLogResponse>
         <RequestId>65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</PurgeDBInstanceLogResponse>
```

`JSON` format

``` {#codeblock_4f5_5vf_yk5}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## Error codes {#section_mob_jc6_f76 .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

