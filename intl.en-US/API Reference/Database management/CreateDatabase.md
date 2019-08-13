# CreateDatabase {#doc_api_1063908 .reference}

You can call this operation to create a database under an instance.

This operation must meet the following requirements:

-   The instance is in the running state.
-   The number of databases in the instance does not exceed the maximum number. You can call the [DescribeDBInstanceAttribute](intl.en-US/API Reference/Instance management/DescribeDBInstanceAttribute.md#) API to view the maximum number of databases.
-   The instance cannot be read-only.

**Note:** This operation is not applicable to ApsaraDB RDS for PostgreSQL, PPAS, or SQL Server 2017 Cluster Edition. You can run `CREATE DATABASE` SQL statement to create databases.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=CreateDatabase) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateDatabase| The operation that you want to perform. Set this parameter to CreateDatabase.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx| The ID of the instance.

 |
|DBName|String|Yes|rds\_mysql| The name of the database.

 **Note:** 

-   It must be 2 to 64 characters in length.
-   It must start with a lowercase letter and end with a lowercase letter or digit.
-   It can contain lowercase letters, digits, underscores \(\_\), and hyphens \(-\).
-   The database name must be unique whithin the instance.
-   For more information about invalid characters, see [Forbidden keywords table](intl.en-US/API Reference/Appendix/Forbidden keywords table.md#).

 |
|CharacterSetName|String|Yes|gbk| The character set. Valid values:

 -   MySQL or MariaDB: utf8 | gbk | latin1 | utf8mb4.
-   SQL Server: Chinese\_PRC\_CI\_AS | Chinese\_PRC\_CS\_AS | SQL\_Latin1\_General\_CP1\_CI\_AS | SQL\_Latin1\_General\_CP1\_CS\_AS | Chinese\_PRC\_BIN.

 |
|DBDescription|String|No|Test database| The description of the database. It must be 2 to 256 characters in length. It can contain letters, digits, underscores \(\_\), and hyphens \(-\), and must start with a letter.

 **Note:** It cannot start with http:// or https://.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID that Alibaba Cloud issues to a user for service access.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|5A77D650-27A1-4E08-AD9E-59008EDB6927| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=CreateDatabase
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx 
&DBName=rds_mysql 
&CharacterSetName=gbk
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#codeblock_563_og2_klu}
<CreateDatabaseResponse>
           <RequestId>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestId>
</CreateDatabaseResponse>
```

`JSON` format

``` {#codeblock_000_rsi_dvm}
{
	"RequestID":"5A77D650-27A1-4E08-AD9E-59008EDB6927"
}
```

## Error codes {#section_ll2_6i1_wfv .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

