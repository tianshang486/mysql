# CalculateDBInstanceWeight {#doc_api_Rds_CalculateDBInstanceWeight .reference}

You can call this operation to query the read weights distributed by the system.

If [read/write splitting](~~51073~~) is enabled, you can call this operation to query the read weights specified by the system. To query custom read weights, see [DescribeDBInstanceNetInfo](~~26237~~).

This operation is applicable to the following instances:

-   MySQL 5.7 High-availability Edition \(based on local SSDs\)
-   MySQL 5.6
-   SQL Server 2017 Cluster Edition

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=CalculateDBInstanceWeight) to perform debugging.

API Explorer provides various functions to simplify API usage. For example, you can search APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CalculateDBInstanceWeight| The operation that you want to perform. Set the value to**CalculateDBInstanceWeight**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the master instance.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Items| | | The list of weights specified by the system.

 |
|└DBInstanceId|String|rm-uf6wjk5xxxxxxx| The ID of an instance.

 |
|└DBInstanceType|String|Master| The type of the instance. Valid values:

 -   **Master**.
-   **Readonly**.

 |
|└Weight|String|100| The instance weight calculated by the system in real time.

 |
|└ReadonlyInstanceSQLDelayedTime|String|30| The latency for read-only instances to synchronize the data of the master instance. After a latency of **ReadonlyInstanceSQLDelayedTime** seconds, the read-only instances synchronize the data of the master instance. Unit: seconds.

 |
|RequestId|String|C816A4BF-A6EC-4722-95F9-2055859CCFD2| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CalculateDBInstanceWeight
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Normal response example

`XML` format

``` {#xml_return_success_demo}
<CalculateDBInstanceWeightResponse>
  <items>
    <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
    <DBInstanceType>Master</DBInstanceType>
    <Weight/>
    <Availability/>
  </items> 
  <requestId>C816A4BF-A6EC-4722-95F9-2055859CCFD2</requestId>
</CalculateDBInstanceWeightResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"requestId":"C816A4BF-A6EC-4722-95F9-2055859CCFD2",
	"items":[
		{
			"Weight":"",
			"Availability":"",
			"DBInstanceType":"Master",
			"DBInstanceId":"rm-uf6wjk5xxxxxxx"
		}
	]
}
```

## Error codes {#section_kkp_aqp_o4a .section}

[View error codes](https://error-center.alibabacloud.com/status/product/Rds)

