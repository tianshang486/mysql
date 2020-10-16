# Migrate data across instances

You can call the ImportDatabaseBetweenInstances operation to migrate data across ApsaraDB for RDS instances.

During the migration, the source instance is in the **Migrating** state, and the destination instance is in the **Importing** state.

Before you call this operation, make sure that the following requirements are met:

-   The source and destination instances must run SQL Server and belong to the dedicated or dedicated host instance family. For more information about the instance types, see [Primary instance types](~~26312~~).
-   The source and destination instances must be created by using the same user credentials.
-   The source and destination instances must be in the Running state.
-   The source and destination databases must be in the Running state.
-   The remaining storage space of the destination instance must be larger than that of the source instance.

**Note:**

-   This operation is not supported for instances that run SQL Server 2017 EE.
-   You can migrate the data of multiple databases at a time.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer.](https://api.aliyun.com/#product=Rds&api=ImportDatabaseBetweenInstances&type=RPC&version=2014-08-15)OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ImportDatabaseBetweenInstances|The operation that you want to perform. Set the value to **ImportDatabaseBetweenInstances**. |
|DBInfo|String|Yes|\{"DBNames":\["mydb","mydb2"\]\}|The databases whose data you want to migrate. The value of this parameter is a JSON string.

 **Note:** If the source and destination instances run SQL Server, the value of this parameter consists of one or more key-value pairs. In each key-value pair, the key represents the name of the source database, and the value represents the name of the destination database. A source database can have a different name from its destination database. Example:

```
{"DBNames":{"srcdb":"destdb","srcdb2":"destmydb2"}}
```

In the preceding example, the data of the source database srcdb is migrated to the destination database destdb, and the data of the source database srcdb2 is migrated to the destination database destmydb2. Note that the name of each source or destination database must be unique. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the destination instance. |
|SourceDBInstanceId|String|Yes|rm-g4a1jk8xxxxxxx|The ID of the source instance. The source and destination instances cannot have the same ID. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ImportId|String|85265475235|The ID of the migration task. |
|RequestId|String|5A77D650-27A1-4E08-AD9E-59008EDB6927|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ImportDatabaseBetweenInstances
&DBInstanceId=rm-uf6wjk5xxxxxxx
&SourceDBInstanceId=rm-g4a1jk8xxxxxxx
&DBInfo={"DBNames":["mydb","mydb2"]}
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ImportDatabaseBetweenInstancesResponse>
           <ImportId>2122321</ImportId>
         <RequestId>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestId>
</ImportDatabaseBetweenInstancesResponse>
```

`JSON` format

```
{
       "ImportId":2122321,
       "RequestId":"5A77D650-27A1-4E08-AD9E-59008EDB6927"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

