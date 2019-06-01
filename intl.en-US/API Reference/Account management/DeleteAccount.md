# DeleteAccount {#doc_api_1064578 .reference}

You can call this operation to delete an RDS database account.

When you call this operation, the instance must be in the running state.

**Note:** This operation is not applicable to SQL Server 2017 Cluster Edition, PostgreSQL, and PPAS instances.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=DeleteAccount) to perform debugging.

API Explorer provides various functions to simplify API usage. For example, you can search APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteAccount| The operation that you want to perform. Set the value to **DeleteAccount**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|AccountName|String|Yes|test1| The name of the database account to be deleted.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameter {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|91E855E5-7E80-4955-929B-C74EE1D38C66| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DeleteAccount
&DBInstanceId=rm-uf6wjk5xxxxxxx
&AccountName=test1
&<Common request parameters>
```

Normal response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteAccountResponse> 
  <RequestID>91E855E5-7E80-4955-929B-C74EE1D38C66</RequestID>
</DeleteAccountResponse> 
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestID":"91E855E5-7E80-4955-929B-C74EE1D38C66"
}
```

## Error codes { .section}

[View error codes](https://error-center.alibabacloud.com/status/product/Rds)

