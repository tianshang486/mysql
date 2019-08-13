# ImportDatabaseBetweenInstances {#doc_api_1091655 .reference}

You can call this operation to migrate data from other RDS instances.

During migration, the source instance is in the **Migrating** state, and the target instance is in the **Importing** state.

This operation must meet the following requirements:

-   Only the dedicated CPU instances and dedicated hosts of MySQL and SQL Server are supported. For more information about the instance type, see [Instance type list](../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md#).
-   Only the database migration between different instances that belong to the same user is allowed.
-   The instance is in the running state.
-   The database is in the running state.
-   The remaining storage space of the target instance must be larger than that of the source instance.
-   For MySQL instances, the database to be migrated must exist in both the source and target instances. It also must be in the running state.

**Note:** 

-   SQL Server 2017 Cluster Edition instances are not supported.
-   The database migration in batch mode is supported.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ImportDatabaseBetweenInstances) to perform debugging. OpenAPI Explorer allows you to perform various API operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|ImportDatabaseBetweenInstances| The operation that you want to perform. Set this parameter to ImportDatabaseBetweenInstances.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the target instance.

 |
|SourceDBInstanceId|String|Yes|rm-g4a1jk8xxxxxxx| The ID of the source instance. It cannot be the same as that of the target instance.

 |
|DBInfo|String|Yes|\{“DBNames”:\[“mydb”,”mydb2”\]\}| The database information of instances to be migrated. The format is a JSON string:

 -   For MySQL instances, the parameter value is an array. The source database must have the same name as the target database. In the following example, a database named mydb and a database named mydb2 are migrated from the source instance to the target instance:

    ``` {#codeblock_01y_ogc_wtx}
{“DBNames”:[“mydb”,”mydb2”]}
    ```

-   The value of the SQL Server instance is a key-value pair. Key represents the name of the source database. Value represents the name of the target database. The SQL Server instance allows the source database to have a different name from the target database. In the following example, srcdb is migrated to destdb and srcdb2 is migrated to destmydb2. However, neither multiple source databases nor multiple target databases are allowed to have the same name.

    ``` {#codeblock_6dy_3eh_som}
{“DBNames”:{“srcdb”:”destdb”,”srcdb2”:”destmydb2”}}
    ```


 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ImportId|String|85265475235| The ID of the import task.

 |
|RequestId|String|5A77D650-27A1-4E08-AD9E-59008EDB6927| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=ImportDatabaseBetweenInstances
&DBInstanceId=rm-uf6wjk5xxxxxxx 
&SourceDBInstanceId=rm-g4a1jk8xxxxxxx
&DBInfo={“DBNames”:[“mydb”,”mydb2”]}
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_j84_o6e_v32}
<ImportDatabaseBetweenInstancesResponse>
           <ImportId>2122321</ImportId>
         <RequestId>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestId>
</ImportDatabaseBetweenInstancesResponse>
```

`JSON` format

``` {#codeblock_jxp_zm5_cmy}
{
	"ImportId":2122321,
	"RequestId":"5A77D650-27A1-4E08-AD9E-59008EDB6927"
}
```

## Error codes {#section_l6m_tek_rzx .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

