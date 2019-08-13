# RevokeAccountPrivilege {#doc_api_1064591 .reference}

You can call this operation to remove privileges of an RDS database account on a database.

When you perform this operation, the instance must meet the following requirements:

-   The instance is in the running state.
-   The database is in the running state.

**Note:** 

-   The removed privileges are as follows: SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, REFERENCES, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, EVENT, and TRIGGER.
-   This operation is not applicable to SQL Server 2017 Cluster Edition, PostgreSQL, and PPAS instances.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=RevokeAccountPrivilege) to perform debugging.

OpenAPI Explorer provides various functions to simplify API usage. For example, you can retrieve APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RevokeAccountPrivilege| The operation that you want to perform. Set this parameter to RevokeAccountPrivilege.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|AccountName|String|Yes|test1| The name of the database account.

 |
|DBName|String|Yes|testDB| The name of a database. This API revokes all privileges of the account on the database.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameter {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|E22099CA-A61E-4992-A0B7-CE82DC175626| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=RevokeAccountPrivilege
&DBInstanceId=rm-uf6wjk5xxxxxxx
&AccountName=test1
&DBName=testDB
&<Common request parameters>
```

Normal response examples

`XML` format

``` {#codeblock_wqd_25y_qcj}
<RevokeAccountPrivilegeResponse>
	  <RequestId>E22099CA-A61E-4992-A0B7-CE82DC175626</RequestId></RevokeAccountPrivilegeResponse>
```

`JSON` format

``` {#codeblock_k8s_r2f_rxr}
{
	"RequestId":"E22099CA-A61E-4992-A0B7-CE82DC175626"
}
```

## Error codes {#section_7ot_7ui_ndw .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

