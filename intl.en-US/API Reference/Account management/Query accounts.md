# Query accounts

You can call the DescribeAccounts operation to query information about the accounts that are created on an ApsaraDB RDS instance.

**Note:** This operation is not supported for instances that run SQL Server 2017 EE, PostgreSQL, or PPAS.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeAccounts&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAccounts|The operation that you want to perform. Set the value to **DescribeAccounts**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|AccountName|String|No|test1|The name of the account. |
|PageSize|Integer|No|30|The number of entries to return on each page. Default value: **30**. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

 Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Accounts|Array| |An array that consists of accounts. |
|DBInstanceAccount| | | |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance to which the account belongs. |
|AccountName|String|test1|The name of the account. |
|AccountStatus|String|Available|The status of the account. Valid values:

 -   **Unavailable**
-   **Available** |
|AccountDescription|String|Test account|The description of the account. |
|DatabasePrivileges|Array| |An array that consists of the permissions that are granted to the account. |
|DatabasePrivilege| | | |
|DBName|String|test1|The name of the database. |
|AccountPrivilege|String|ReadWrite|The type of permission that is granted to the account. Valid values:

 -   **ReadWrite**: read and write permissions
-   **ReadOnly**: read-only permission
-   **DDLOnly**: DDL-only permissions
-   **DMLOnly**: DML-only permissions
-   **Custom**: custom permissions \(You can modify the permissions of the account by using SQL commands.\) |
|AccountPrivilegeDetail|String|SELECT,INSERT|The permissions that are granted to the account. For more information, see [Account permissions](~~146395~~). |
|AccountType|String|Normal|The type of the account. Valid values:

 -   **Normal**: standard account
-   **Super**: privileged account
-   **Sysadmin**: superuser account that has the system administrator permissions |
|PrivExceeded|String|0|Indicates whether the number of databases that are managed by the account exceeds the specified limit. Valid values:

 -   **1**: The number of databases that are managed by the account exceeds the specified limit.
-   **0**: The number of databases that are managed by the account does not exceed the specified limit. |
|RequestId|String|A2E94301-D07F-4457-9B49-6AA2BB388C85|The ID of the request. |
|SystemAdminAccountFirstActivationTime|String|2020-02-06T11:00:00Z|The first time when superuser accounts were enabled. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC.

 **Note:** This parameter is returned only when you set the SysadminAccount parameter to True. |
|SystemAdminAccountStatus|String|True|Indicates whether superuser accounts are enabled. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeAccounts
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeAccountsResponse>
	  <Accounts>
		    <DBInstanceAccount>
			      <DatabasePrivileges>
				        <DatabasePrivilege>
					          <AccountPrivilege>ReadWrite</AccountPrivilege>
					          <AccountPrivilegeDetail>SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,REFERENCES,INDEX,ALTER,CREATE TEMPORARY TABLES,LOCK TABLES,CREATE VIEW,SHOW VIEW,CREATE ROUTINE,ALTER ROUTINE,EXECUTE,EVENT,TRIGGER</AccountPrivilegeDetail>
					          <DBName>testdb</DBName>
				        </DatabasePrivilege>
			      </DatabasePrivileges>
			      <AccountStatus>Available</AccountStatus>
			      <AccountDescription></AccountDescription>
			      <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
			      <AccountName>testacc02</AccountName>
			      <PrivExceeded>0</PrivExceeded>
			      <AccountType>Normal</AccountType>
		    </DBInstanceAccount>
	  </Accounts>
	  <RequestId>A2E94301-D07F-4457-9B49-6AA2BB388C85</RequestId>
</DescribeAccountsResponse>
```

`JSON` format

```
{
    "Accounts": {
        "DBInstanceAccount": [
            {
                "DatabasePrivileges": {
                    "DatabasePrivilege": [
                        {
                            "AccountPrivilege": "ReadWrite",
                            "AccountPrivilegeDetail": "SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,REFERENCES,INDEX,ALTER,CREATE TEMPORARY TABLES,LOCK TABLES,CREATE VIEW,SHOW VIEW,CREATE ROUTINE,ALTER ROUTINE,EXECUTE,EVENT,TRIGGER",
                            "DBName": "testdb"
                        }
                    ]
                },
                "AccountStatus": "Available",
                "AccountDescription": "",
                "DBInstanceId": "rm-uf6wjk5xxxxxxx",
                "AccountName": "testacc02",
                "PrivExceeded": "0",
                "AccountType": "Normal"
            }
        ]
    },
    "RequestId": "A2E94301-D07F-4457-9B49-6AA2BB388C85"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

