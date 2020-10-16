# Query databases

You can call the DescribeDatabases operation to query information about the databases of an ApsaraDB for RDS instance.

**Note:** If the request parameters are incorrectly specified, the response is null.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeDatabases&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDatabases|The operation that you want to perform. Set the value to **DescribeDatabases**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|DBName|String|No|testDB01|The names of the databases whose information you want to query. |
|DBStatus|String|No|Creating|The status of the databases whose information you want to query. Valid values:

-   **Creating**
-   **Running**
-   **Deleting** |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values:

-   **30**
-   **50**
-   **100**

Default value: 30. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Databases|Array of Database| |An array that consists of information about databases. |
|Database| | | |
|DBName|String|testDB01|The name of the database. |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance to which the database belongs. |
|Engine|String|MySQL|The database engine of the instance to which the database belongs. |
|DBStatus|String|Creating|The status of the database. Valid values:

-   **Creating**
-   **Running**
-   **Deleting** |
|CharacterSetName|String|utf8|The character set that is used by the database. |
|DBDescription|String|testdatabase|The description of the database. |
|Accounts|Array of AccountPrivilegeInfo| |An array that consists of information about accounts. These accounts have specific permissions on the database. |
|AccountPrivilegeInfo| | | |
|Account|String|test|The name of the account that has permissions on the database. |
|AccountPrivilege|String|DMLOnly|The permissions that the account has on the database. Valid values:

-   **ReadWrite**: The account has the read/write permissions on the database.
-   **ReadOnly**: The account has the read-only permissions on the database.
-   **DMLOnly**: The account has the DML-only permissions on the database.
-   **DDLOnly**: The account has the DDL-only permissions on the database. |
|AccountPrivilegeDetail|String|SELECT|The permissions that the account has on the database. |
|RequestId|String|2603CA96-B17D-4903-BC04-61A2C829CD94|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeDatabases
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDatabasesResponse>
      <RequestId>2603CA96-B17D-4903-BC04-61A2C829CD94</RequestId>
      <Databases>
            <Database>
                  <Engine>MySQL</Engine>
                  <CharacterSetName>utf8</CharacterSetName>
                  <DBStatus>Creating</DBStatus>
                  <DBDescription></DBDescription>
                  <DBInstanceId>rdsaiiabnaiiabn</DBInstanceId>
                  <Accounts></Accounts>
                  <DBName>testdb</DBName>
            </Database>
            <Database>
                  <Engine>MySQL</Engine>
                  <CharacterSetName>gbk</CharacterSetName>
                  <DBStatus>Creating</DBStatus>
                  <DBDescription></DBDescription>
                  <DBInstanceId>rdsaiiabnaiiabn</DBInstanceId>
                  <Accounts></Accounts>
                  <DBName>testdb2</DBName>
            </Database>
      </Databases></DescribeDatabasesResponse>
```

`JSON` format

```
{
    "RequestId": "2603CA96-B17D-4903-BC04-61A2C829CD94",
    "Databases": {
        "Database": [
            {
                "Engine": "MySQL",
                "CharacterSetName": "utf8",
                "DBStatus": "Creating",
                "DBDescription": "",
                "DBInstanceId": "rdsaiiabnaiiabn",
                "Accounts": {
                    " AccountPrivilegeInfo": []
                },
                "DBName": "testdb"
            },
            {
                "Engine": "MySQL",
                "CharacterSetName": "gbk",
                "DBStatus": "Creating",
                "DBDescription": "",
                "DBInstanceId": "rdsaiiabnaiiabn",
                "Accounts": {
                    " AccountPrivilegeInfo": []
                },
                "DBName": "testdb2"
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

