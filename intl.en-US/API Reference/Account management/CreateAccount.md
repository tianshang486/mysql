# CreateAccount {#doc_api_1105955 .reference}

You can call this operation to create an RDS database account.

When you call this operation, the instance must meet the following requirements:

-   The instance is in the running state.
-   The database is in the running state.
-   The maximum number of accounts for a single instance is not exceeded.

**Note:** 

-   This operation is applicable to MySQL, MariaDB, and SQL Server instances \(excluding SQL Server 2017 Cluster Edition\).
-   PostgreSQL, PPAS, and SQL Server 2017 Cluster Edition instances have a superuser account. Other accounts are created through SQL by the superuser account.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=CreateAccount) to perform debugging.

API Explorer provides various functions to simplify API usage. For example, you can search APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateAccount| The operation that you want to perform. Set the value to **CreateAccount**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|AccountName|String|Yes|test1| The name of the database account.

 **Note:** 

-   The name must be unique.
-   It must start with a letter and end with a letter or digit.
-   It consits of lowercase letters, digits, or underscores \(\_\).
-   It contains 2 to 16 characters.
-   For information about invalid characters, see [Forbidden keywords](~~26317~~).

 |
|AccountPassword|String|Yes|Test123456| The password of the database account.

 **Note:** 

-   It contains 8 to 32 characters.
-   It contains at least three of the four character types: uppercase letters, lowercase letters, digits, and special characters.
-   The special characters are !@\#$&%^\*\(\)\_+-=

 |
|AccountDescription|String|No|Test account A| The description of the account. The description starts with a letter and contains 2 to 256 characters, including letters, digits, underscores \(\_\), or hyphens \(-\).

 **Note:** It cannot start with http:// or https://.

 |
|AccountType|String|No|Normal| The type of the account. Valid values:

 -   **Normal**.
-   **Super**.

 Default value: **Normal**.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CreateAccount
&DBInstanceId=rm-uf6wjk5xxxxxxx
&AccountName=test1
&AccountPassword=Test123456
&<Common request parameters>
```

Normal response examples

`XML` format

``` {#xml_return_success_demo}
<CreateAccountResponse> 
  <RequestId>D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD</RequestId> 
</CreateAccountResponse> 
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD"
}
```

## Error codes {#section_kjh_i6q_yb3 .section}

[View error codes](https://error-center.alibabacloud.com/status/product/Rds)

