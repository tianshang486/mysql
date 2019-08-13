# CancelImport {#doc_api_1091640 .reference}

You can call this operation to cancel the migration task of RDS instances.

This operation is applicable to the dedicated CPU instances and dedicated hosts of MySQL and SQL Server. For more information about the migration task, see [ImportDatabaseBetweenInstances](intl.en-US/API Reference/Data migration/ImportDatabaseBetweenInstances.md#).

**Note:** This operation is not applicable to SQL Server 2017 Cluster Edition instances.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=CancelImport) to perform debugging. OpenAPI Explorer allows you to perform various API operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|CancelImport| The operation that you want to perform. Set this parameter to CancelImport.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|ImportId|Integer|Yes|8562584| The ID of the migration task.

 **Note:** This parameter is returned when the migration task is initiated. For more information, see [ImportDatabaseBetweenInstances](intl.en-US/API Reference/Data migration/ImportDatabaseBetweenInstances.md#).

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|17F57FEE-EA4F-4337-8D2E-9C23CAA63D74| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=CancelImport
&DBInstanceId=rm-uf6wjk5xxxxxxx
&ImportId=8562584
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_sk1_77j_95t}
<CancelImportResponse>
         <RequestId>17F57FEE-EA4F-4337-8D2E-9C23CAA63D74</RequestId>
</CancelImportResponse>
```

`JSON` format

``` {#codeblock_3m9_4pi_4e6}
{
	"RequestId":" 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74"
}
```

## Error codes {#section_cm9_768_88k .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

