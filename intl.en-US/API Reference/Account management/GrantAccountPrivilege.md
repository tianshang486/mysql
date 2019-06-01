# GrantAccountPrivilege {#doc_api_1064586 .reference}

You can call this operation to grant privileges to an RDS database account so that it can access one or more databases.

When you call this operation, the instance must be in the running state.

**Note:** This operation is not applicable to SQL Server 2017 Cluster Edition, PostgreSQL, and PPAS instances.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=GrantAccountPrivilege) to perform debugging.

API Explorer provides various functions to simplify API usage. For example, you can search APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GrantAccountPrivilege| The operation that you want to perform. Set the value to **GrantAccountPrivilege**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx| The ID of the instance.

 |
|AccountName|String|Yes|test1| The name of the account.

 |
|DBName|String|Yes|testDB| The name of the database that the account needs to access.

 |
|AccountPrivilege|String|Yes|ReadWrite| The account privilege. Valid values:

 -   **ReadWrite**
-   **ReadOnly**
-   **DDLOnly**: This value is only for MySQL and MariaDB.
-   **DMLOnly**: This value is only for MySQL and MariaDB.
-   **DBOwner**: This value is only for SQL Server.

 |

## Response parameter {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|81BC9559-7B22-4B7F-B705-5F56DEECDEA7| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=GrantAccountPrivilege
&DBInstanceId=rm-uf6wjk5xxxxxxx 
&AccountName=test1 
&DBName=test
&AccountPrivilege=ReadWrite
&<Common request parameters>
```

Normal response examples

`XML` format

``` {#xml_return_success_demo}
<GrantAccountPrivilegeResponse> 
  <RequestId>81BC9559-7B22-4B7F-B705-5F56DEECDEA7</RequestId>
</GrantAccountPrivilegeResponse> 
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"81BC9559-7B22-4B7F-B705-5F56DEECDEA7"
}
```

## Error codes { .section}

[View error codes](https://error-center.alibabacloud.com/status/product/Rds)

