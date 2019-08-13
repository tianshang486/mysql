# ReleaseInstancePublicConnection {#doc_api_1075637 .reference}

You can call this operation to release the public IP address of an instance.

To guarantee data security, you can release the public IP address through this operation when you do not need to access the database from the public IP address.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ReleaseInstancePublicConnection) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|ReleaseInstancePublicConnection| The operation that you want to perform. Set this parameter to ReleaseInstancePublicConnection.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|CurrentConnectionString|String|Yes|rm-uf6wjk5xxxx.mysql.rds.aliyuncs.com| The public IP address.

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

http(s)://rds.aliyuncs.com/? Action=ReleaseInstancePublicConnection
&DBInstanceId=rm-uf6wjk5xxxxxxx
&CurrentConnectionString=rm-uf6wjk5xxxx.mysql.rds.aliyuncs.com 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_rmu_6gs_mlz}
<ReleaseInstancePublicConnectionResponse>  
         <RequestId>65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</ReleaseInstancePublicConnectionResponse>
```

`JSON` format

``` {#codeblock_mff_vgb_837}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## Error codes {#section_8jg_yws_h8d .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

