# ModifyDBDescription {#doc_api_1063927 .reference}

You can call this operation to modify the database description.

**Note:** This operation is not applicable to ApsaraDB RDS for PostgreSQL or PPAS.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBDescription) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBDescription| The operation that you want to perform. Set this parameter to ModifyDBDescription.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|DBName|String|Yes|testDB01| The name of the database.

 |
|DBDescription|String|Yes|Test database A| The description of the database.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID that Alibaba Cloud issues to a user for service access.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|17F57FEE-EA4F-4337-8D2E-9C23CAA63D74| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=ModifyDBDescription
&DBDescription=Test database A
&DBInstanceId=rm-uf6wjk5xxxxxxx 
&DBName=testDB01
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_gok_yn2_7yr}
<ModifyDBDescriptionResponse>
	  <RequestId> 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74</RequestId></ModifyDBDescriptionResponse>
```

`JSON` format

``` {#codeblock_ssz_l0w_x21}
{
	"RequestId":" 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74"
}
```

## Error codes {#section_109_9b5_u5n .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

