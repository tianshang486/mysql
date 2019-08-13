# ResetAccount {#doc_api_1105983 .reference}

You can call this operation to reset the permissions of a superuser account.

**Note:** This operation is not applicable to SQL Server 2008 R2 instances that do not have superuser accounts.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ResetAccount) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|ResetAccount| The operation that you want to perform. Set this parameter to ResetAccount.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|AccountName|String|Yes|test1| The name of the superuser account.

 |
|AccountPassword|String|Yes|Test123456| The password of the superuser account.

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
|RequestId|String|81BC9559-7B22-4B7F-B705-5F56DEECDEA7| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=ResetAccount
&AccountName=test1
&AccountPassword=Test123456
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_q5r_2fc_jtx}
<ResetAccountResponse>
	  <RequestId>81BC9559-7B22-4B7F-B705-5F56DEECDEA7</RequestId></ResetAccountResponse>
```

`JSON` format

``` {#codeblock_d2i_wip_pgj}
{
	"RequestId":"81BC9559-7B22-4B7F-B705-5F56DEECDEA7"
}
```

## Error codes {#section_hph_uo4_bac .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

