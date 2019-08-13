# ModifyDBInstanceDescription {#doc_api_1063661 .reference}

You can call this operation to modify the description of the instance.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceDescription) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceDescription| The operation that you want to perform. Set this parameter to ModifyDBInstanceDescription.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx| The ID of the instance.

 |
|DBInstanceDescription|String|Yes|Alibaba Cloud instance in test environment| The description of the instance.

 **Note:** It must be 2 to 64 characters in length.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxxxxx| The AccessKey ID that Alibaba Cloud issues to a user for service access.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|17F57FEE-EA4F-4337-8D2E-9C23CAA63D74| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=ModifyDBInstanceDescription
&DBInstanceDescription=Alibaba Cloud instance in test environment
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_5oi_2qt_c13}
< ModifyDBInstanceDescriptionResponse>
         <RequestId>17F57FEE-EA4F-4337-8D2E-9C23CAA63D74</RequestId>
</ModifyDBInstanceDescriptionResponse>
```

`JSON` format

``` {#codeblock_zbp_beq_ryw}
{
	"RequestId":" 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74"
}
```

## Error codes {#section_klc_pnj_kil .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

