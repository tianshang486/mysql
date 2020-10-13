# Modify the description of a database account

Modifies the description of a database account.

**Note:** This operation is not applicable to ApsaraDB for RDS instances that run SQL Server 2017 EE, PostgreSQL, and PPAS.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyAccountDescription&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyAccountDescription|The operation that you want to perform. Set the value to **ModifyAccountDescription**. |
|AccountDescription|String|Yes|Test account A|The description of the account. It must be 2 to 256 characters in length, can contain letters, digits, underscores \(\_\), and hyphens \(-\), and must start with a letter.

 **Note:** The description cannot start with http:// or https://. |
|AccountName|String|Yes|test1|The name of the account. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|17F57FEE-EA4F-4337-8D2E-9C23CAA63D74|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyAccountDescription
&AccountDescription=Test account A
&AccountName=test1
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyAccountDescriptionResponse>
	  <RequestId> 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74</RequestId>
</ModifyAccountDescriptionResponse>
```

`JSON` format

```
{
  "RequestId": " 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

