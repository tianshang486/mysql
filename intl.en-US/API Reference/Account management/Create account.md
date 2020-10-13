# Create account

You can call the CreateAccount operation to create an account that is used to manage databases on an ApsaraDB for RDS instance.

Before you call this operation, make sure that the following requirements are met:

-   The instance must be in the Running state.
-   The databases must be in the Running state.
-   The number of accounts that are created on the instance cannot exceed the maximum number of accounts that are allowed per instance.

**Note:**

-   This operation is supported only for instances that run MySQL, MariaDB, or SQL Server. However, this operation is not supported for instances that run SQL Server 2017 EE.
-   You can create only one privileged account for the instance. However, this does not apply if the instance runs PostgreSQL with standard or enhanced SSDs.
-   You can log on to the instance by using its privileged account. Then, you can create standard accounts by using SQL statements.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates a sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=CreateAccount&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateAccount|The operation that you want to perform. Set the value to **CreateAccount**. |
|AccountName|String|Yes|test1|The username of the account.

**Note:**

-   The username must be unique.
-   The username must start with a lowercase letter and end with a lowercase letter or digit.
-   The username can contain lowercase letters, digits, and underscores \(\_\).
-   The username must be 2 to 16 characters in length.
-   For more information about invalid characters, see [Forbidden keywords table](~~26317~~). |
|AccountPassword|String|Yes|Test123456|The password of the account.

**Note:**

-   The password must be 8 to 32 characters in length.
-   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters.
-   Special characters include: ! @ \# $ % ^ & \* \(\)\_+-= |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|AccountDescription|String|No|Test account A|The description of the account. The description can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter.

**Note:** The description cannot start with http:// or https://. |
|AccountType|String|No|Normal|The type of the account. Valid values:

-   **Normal:** The account is a standard account.
-   **Super:** The account is a privileged account.

Default value: **Normal**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=CreateAccount
&DBInstanceId=rm-uf6wjk5xxxxxxx
&AccountName=test1
&AccountPassword=Test123456
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateAccountResponse>
         <RequestId>D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD</RequestId>
</CreateAccountResponse>
```

`JSON` format

```
{
    "RequestId":"D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

