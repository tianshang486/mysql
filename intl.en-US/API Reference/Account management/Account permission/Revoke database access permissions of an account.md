# Revoke database access permissions of an account

Revokes database access permissions of an account.

Before you call this operation, make sure that the following requirements are met:

-   The ApsaraDB for RDS instance is in the running state.
-   The database is in the running state.

**Note:**

-   The permissions that can be revoked include SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, REFERENCES, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, EVENT, and TRIGGER.
-   If the instance runs SQL Server 2017 EE, PostgreSQL, or PPAS, this operation is not supported.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=RevokeAccountPrivilege&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RevokeAccountPrivilege|The operation that you want to perform. Set the value to **RevokeAccountPrivilege**. |
|AccountName|String|Yes|test1|The name of the account. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|DBName|String|Yes|testDB|The name of the database. You can revoke all permissions of the account on this database. Separate multiple databases with commas \(,\). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|E22099CA-A61E-4992-A0B7-CE82DC175626|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=RevokeAccountPrivilege
&DBInstanceId=rm-uf6wjk5xxxxxxx
&AccountName=test1
&DBName=testDB
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RevokeAccountPrivilegeResponse>
      <RequestId>E22099CA-A61E-4992-A0B7-CE82DC175626</RequestId>
</RevokeAccountPrivilegeResponse>
```

`JSON` format

```
{
       "RequestId":"E22099CA-A61E-4992-A0B7-CE82DC175626"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

