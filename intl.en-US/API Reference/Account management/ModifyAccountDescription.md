# ModifyAccountDescription {#doc_api_1064592 .reference}

You can call this operation to modify the description of an RDS database account.

**Note:** This operation is not applicable to SQL Server 2017 Cluster Edition, PostgreSQL, and PPAS instances.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifyAccountDescription) to perform debugging.

OpenAPI Explorer provides various functions to simplify API usage. For example, you can retrieve APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyAccountDescription| The operation that you want to perform. Set this parameter to ModifyAccountDescription.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|AccountName|String|Yes|test1| The name of the account.

 |
|AccountDescription|String|Yes|Test account A| The description of the account. The description starts with a letter and contains 2 to 256 characters, including letters, digits, underscores \(\_\), or hyphens \(-\).

 **Note:** It cannot start with http:// or https://.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameter {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|17F57FEE-EA4F-4337-8D2E-9C23CAA63D74| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyAccountDescription
&AccountDescription=Test account A
&AccountName=test1
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<Common request parameters>
```

Normal response examples

`XML` format

``` {#codeblock_cqc_2wf_79d}
<ModifyAccountDescriptionResponse>
	  <RequestId> 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74</RequestId></ModifyAccountDescriptionResponse>
```

`JSON` format

``` {#codeblock_bat_muw_ek2}
{
	"RequestId":" 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74"
}
```

## Error codes {#section_uo9_r0y_asu .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

