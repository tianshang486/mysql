# AllocateInstancePublicConnection {#doc_api_Rds_AllocateInstancePublicConnection .reference}

You can call this operation to apply for the public IP address of an instance.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=AllocateInstancePublicConnection) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|AllocateInstancePublicConnection| The operation that you want to perform. Set this parameter to AllocateInstancePublicConnection.

 |
|ConnectionStringPrefix|String|Yes|test1.mysql.rds.aliyuncs.com| The public IP address. The prefix can be customized.

 **Note:** It must be 5 to 40 characters in length. It can contain letters, digits, and hyphens \(-\). It cannot contain Chinese characters andthe following special characters:

~ ! \# % ^ & \* = + \\ | \{ \} ; : ' " , < \> / ?

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|Port|String|Yes|3306| The connection port of the public network. Valid values: 1000 to 5999

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=AllocateInstancePublicConnection
&ConnectionStringPrefix=test1.mysql.rds.aliyuncs.com
&DBInstanceId=rm-uf6wjk5xxxxxxx
&Port=3306
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_efb_5d1_uus}
<AllocateInstancePublicConnectionResponse>
         <RequestId>65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</AllocateInstancePublicConnectionResponse>
```

`JSON` format

``` {#codeblock_3vs_wrr_1yw}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## Error codes {#section_r1y_sgx_wla .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/).

