# ResetAccountPassword {#doc_api_1105982 .reference}

You can call this operation to reset the password of an account.

When you call this operation, the instance must be in the running state.

**Note:** For SQL Server 2017 Cluster Edition instances, PostgreSQL instances, and PPAS instances, you cannot call this operation to reset the password of an account that is created through SQL.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ResetAccountPassword) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|ResetAccountPassword| The operation that you want to perform. Set the value to ResetAccountPassword.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|AccountName|String|Yes|test1| The name of the account.

 |
|AccountPassword|String|Yes|Test123456| The new password.

 **Note:** 

-   It must be 8 to 32 characters in length.
-   It must contain three of the following four character types: uppercase letters, lowercase letters, digits, and special characters.
-   The allowed special characters are as follows:

! @ \# $ & % ^ \* \( \) \_ + - =


 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=ResetAccountPassword
&DBInstanceId=rm-uf6wjk5xxxxxxx 
&AccountName=test1 
&AccountPassword=Test123456
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_yjw_v07_riz}
<ResetAccountPasswordResponse>
	  <RequestId>D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD</RequestId></ResetAccountPasswordResponse>
```

`JSON` format

``` {#codeblock_x55_mjx_5g5}
{
	"RequestId":"D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD"
}
```

## Error codes {#section_xt2_0wn_0zu .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

