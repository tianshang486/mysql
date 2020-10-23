# Create database

You can call the CreateDatabase operation to create a database on an ApsaraDB RDS instance.

Before you call this operation, make sure that the following requirements are met:

-   The instance must be in the Running state.
-   The number of databases on the instance cannot exceed the upper limit. You can call the [DescribeDBInstanceAttribute](~~26231~~) operation to query the upper limit.
-   The instance cannot be a read-only instance.

**Note:** This operation is not supported for instances that run PostgreSQL \(with local SSDs\), PPAS, or SQL Server 2017 EE. To create a database on such an instance, you can execute the CREATE DATABASE statement.


## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=CreateDatabase&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateDatabase|The operation that you want to perform. Set the value to **CreateDatabase**. |
|CharacterSetName|String|Yes|gbk|The character set that is supported by the database. Valid values:

 -   MySQL or MariaDB: **utf8, gbk, latin1, and utf8mb4**
-   SQL Server: **Chinese\_PRC\_CI\_AS, Chinese\_PRC\_CS\_AS, SQL\_Latin1\_General\_CP1\_CI\_AS, SQL\_Latin1\_General\_CP1\_CS\_AS, and Chinese\_PRC\_BIN**
-   PostgreSQL: **KOI8U, UTF8, WIN866, WIN874, WIN1250, WIN1251, WIN1252, WIN1253, WIN1254, WIN1255, WIN1256, WIN1257, WIN1258, EUC\_CN, EUC\_KR, EUC\_TW, EUC\_JP, EUC\_JIS\_2004, KOI8R, MULE\_INTERNAL, LATIN1, LATIN2, LATIN3, LATIN4, LATIN5, LATIN6, LATIN7, LATIN8, LATIN9, LATIN10, ISO\_8859\_5, ISO\_8859\_6, ISO\_8859\_7, ISO\_8859\_8, and SQL\_ASCII** |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx|The ID of the instance. |
|DBName|String|Yes|rds\_mysql|The name of the database.

 **Note:**

-   The name must be 2 to 64 characters in length.
-   The name must start with a lowercase letter and end with a lowercase letter or digit.
-   The name can contain lowercase letters, digits, underscores \(\_\), and hyphens \(-\).
-   The name must be unique on the instance.
-   The name cannot contain invalid characters. For more information, see [Forbidden keywords table](~~26317~~). |
|DBDescription|String|No|testdatabase|The description of the database. The description must be 2 to 256 characters in length. The description must start with a letter and can contain letters, digits, underscores \(\_\), and hyphens \(-\).

 **Note:** The description cannot start with http:// or https://. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|5A77D650-27A1-4E08-AD9E-59008EDB6927|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=CreateDatabase
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&DBName=rds_mysql
&CharacterSetName=gbk
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateDatabaseResponse>
    <RequestId>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestId>
</CreateDatabaseResponse>
```

`JSON` format

```
{
    "RequestID":"5A77D650-27A1-4E08-AD9E-59008EDB6927"
  }
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

