# DescribeDatabases {#doc_api_1063920 .reference}

You can call this operation to view the database information under an instance.

**Note:** 

-   If the request parameters are entered incorrectly, the response is null.
-   This operation is not applicable to ApsaraDB RDS for PostgreSQL or PPAS.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDatabases) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDatabases| The operation that you want to perform. Set this parameter to DescribeDatabases.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|DBName|String|No|testDB01| The name of the database.

 |
|DBStatus|String|No|Creating| The status of the database. Valid values:

 -   Creating
-   Running
-   Deleting

 |
|PageSize|Integer|No|30| The number of records on each page. Valid values:

 -   30
-   50
-   100

 Default value: 30.

 |
|PageNumber|Integer|No|1| The page number. It must be greater than 0 and cannot exceed the maximum value of the given Integer.

 Default value: 1.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID that Alibaba Cloud issues to a user for service access.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Databases|N/A|N/A| A collection of database information.

 |
|DBName|String|testDB01| The name of the database.

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx| The name of the instance to which the database belongs.

 |
|Engine|String|MySQL| The type of the database instance.

 |
|DBStatus|String|Creating| The status of the database. Valid values:

 -   Creating
-   Running
-   Deleting

 |
|CharacterSetName|String|utf8| The character set. Valid values:

 -   MySQL or MariaDB: utf8 | gbk | latin1 | utf8mb4.
-   SQL Server: Chinese\_PRC\_CI\_AS | Chinese\_PRC\_CS\_AS | SQL\_Latin1\_General\_CP1\_CI\_AS | SQL\_Latin1\_General\_CP1\_CS\_AS | Chinese\_PRC\_BIN.

 |
|DBDescription|String|Test database| The description of the database.

 |
|Accounts|N/A|N/A| The information of accounts that have database permissions.

 |
|Account|String|test| The name of the account.

 |
|AccountPrivilege|String|DMLOnly| The database permissions of the account. Valid values:

 -   ReadWrite
-   ReadOnly
-   DDLOnly
-   DMLOnly

 |
|AccountPrivilegeDetail|String|SELECT| The detailed permissions that the account has on the database.

 |
|RequestId|String|2603CA96-B17D-4903-BC04-61A2C829CD94| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeDatabases
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_w8q_w3f_l0m}
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

``` {#codeblock_iw0_jez_pb5}
{
	"Databases":{
		"Database":[
			{
				"Accounts":{
					" AccountPrivilegeInfo":[]
				},
				"DBStatus":"Creating",
				"DBInstanceId":"rdsaiiabnaiiabn",
				"DBDescription":"",
				"DBName":"testdb",
				"CharacterSetName":"utf8",
				"Engine":"MySQL"
			},
			{
				"Accounts":{
					" AccountPrivilegeInfo":[]
				},
				"DBStatus":"Creating",
				"DBInstanceId":"rdsaiiabnaiiabn",
				"DBDescription":"",
				"DBName":"testdb2",
				"CharacterSetName":"gbk",
				"Engine":"MySQL"
			}
		]
	},
	"RequestId":"2603CA96-B17D-4903-BC04-61A2C829CD94"
}
```

## Error codes {#section_aq5_5id_ctm .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

