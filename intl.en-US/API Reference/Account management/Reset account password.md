# Reset account password

You can call the ResetAccountPassword operation to reset the password of an account on an ApsaraDB RDS instance.

Before you call this operation, make sure that the instance must be in the Running state.

**Note:** This operation is not supported for accounts that are created by using SQL statements. This applies to instances that run SQL Server 2017 EE, PostgreSQL, or PPAS.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ResetAccountPassword&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ResetAccountPassword|The operation that you want to perform. Set the value to **ResetAccountPassword**. |
|AccountName|String|Yes|test1|The name of the account. |
|AccountPassword|String|Yes|Test123456|The new password of the account.

 **Note:**

-   The password must be 8 to 32 characters in length.
-   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters.
-   Special characters include ! @\#$&amp;%^\*\(\)\_+-= |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ResetAccountPassword
&DBInstanceId=rm-uf6wjk5xxxxxxx
&AccountName=test1
&AccountPassword=Test123456
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ResetAccountPasswordResponse>
	  <RequestId>D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD</RequestId>
</ResetAccountPasswordResponse>
```

`JSON` format

```
{
       "RequestId":"D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

