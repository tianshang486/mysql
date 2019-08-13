# DescribeAccounts {#doc_api_1105966 .reference}

You can call this operation to view the database accounts of an RDS instance.

**Note:** This operation is not applicable to SQL Server 2017 Cluster Edition, PostgreSQL, and PPAS instances.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeAccounts) to perform debugging.

OpenAPI Explorer provides various functions to simplify API usage. For example, you can retrieve APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAccounts| The operation that you want to perform. Set this parameter to DescribeAccounts.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|AccountName|String|No|test1| The name of a database account.

 |
|PageSize|Integer|No|30| The number of records on each page. Valid values:

 -   30
-   50
-   100

 Default value: 30.

 |
|PageNumber|Integer|No|1| The page number. It must be greater than 0 and cannot exceed the maximum value of the Integer data type.

 Default value: 1.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Accounts|N/A|N/A| The account information list.

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx| The ID of the instance to which the account belongs.

 |
|AccountName|String|test1| The name of the database account.

 |
|AccountStatus|String|Available | The status of the account. Valid values:

 -   Unavailable
-   Available

 |
|AccountDescription|String|The account of the test database.| The description of the account.

 |
|DatabasePrivileges|N/A|N/A| The list of database privileges granted to the account.

 |
|DBName|String|test1| The name of the database.

 |
|AccountPrivilege|String|ReadWrite| The privileges of the account. Valid values:

 -   ReadWrite
-   ReadOnly
-   DDLOnly
-   DMLOnly
-   Custom

 |
|AccountPrivilegeDetail|String|SELECT,INSERT| The specific privileges of the account.

 |
|AccountType|String|Normal| The type of the account. Valid values:

 -   Normal
-   Super

 |
|PrivExceeded|String|0| Indicates whether authorization limits are exceeded. Valid values:

 -   1: Yes.
-   0: No.

 |
|RequestId|String|A2E94301-D07F-4457-9B49-6AA2BB388C85| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeAccounts
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Normal response examples

`XML` format

``` {#codeblock_xcz_ml1_h8f}
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
	  <RequestId>A2E94301-D07F-4457-9B49-6AA2BB388C85</RequestId></DescribeAccountsResponse>
```

`JSON` format

``` {#codeblock_8bo_3hi_s0o}
{
	"Accounts":{
		"DBInstanceAccount":[
			{
				"AccountStatus":"Available",
				"DatabasePrivileges":{
					"DatabasePrivilege":[
						{
							"AccountPrivilege":"ReadWrite",
							"AccountPrivilegeDetail":"SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,REFERENCES,INDEX,ALTER,CREATE TEMPORARY TABLES,LOCK TABLES,CREATE VIEW,SHOW VIEW,CREATE ROUTINE,ALTER ROUTINE,EXECUTE,EVENT,TRIGGER",
							"DBName":"testdb"
						}
					]
				},
				"AccountDescription":"",
				"DBInstanceId":"rm-uf6wjk5xxxxxxx",
				"AccountName":"testacc02",
				"PrivExceeded":"0",
				"AccountType":"Normal"
			}
		]
	},
	"RequestId":"A2E94301-D07F-4457-9B49-6AA2BB388C85"
}
```

## Error codes {#section_gwr_ypu_l9y .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

