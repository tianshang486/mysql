# Query read weights of an ApsaraDB for RDS instance

Queries read weights of an ApsaraDB for RDS instance.

When[read/write splitting](~~51073~~)is enabled, this operation is used to calculate the read weights specified by the system. For custom read weights, see [DescribeDBInstanceNetInfo](~~26237~~).

Before you call this operation, make sure that the instance runs one of the following database engine versions and RDS editions:

-   MySQL 5.7 in the High-availability Edition \(with local SSDs\)
-   MySQL 5.6
-   SQL Server 2017 EE

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=CalculateDBInstanceWeight&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CalculateDBInstanceWeight|The operation that you want to perform. Set the value to **CalculateDBInstanceWeight**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the primary instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Items|Array| |The list of weights specified by the system. |
|DBInstanceWeight| | | |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|DBInstanceType|String|Master|The type of the instance. Valid values:

 -   **Master:** The instance is primary.
-   **Readonly:** The instance is read-only. |
|Weight|String|100|The read weight that is calculated by the system in real time. |
|ReadonlyInstanceSQLDelayedTime|String|30|The replication latency between the read-only instance and the primary instance. The read-only instance replicates data from the primary instance based on the latency specified by the **ReadonlyInstanceSQLDelayedTime** parameter. Unit: seconds. |
|RequestId|String|C816A4BF-A6EC-4722-95F9-2055859CCFD2|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=CalculateDBInstanceWeight
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CalculateDBInstanceWeightResponse>
	  <items>
		    <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
		    <DBInstanceType>Master</DBInstanceType>
		    <Weight></Weight>
		    <Availability></Availability>
	  </items>
	  <requestId>C816A4BF-A6EC-4722-95F9-2055859CCFD2</requestId>
</CalculateDBInstanceWeightResponse>
```

`JSON` format

```
{
    "items": [
        {
            "DBInstanceId": "rm-uf6wjk5xxxxxxx",
            "DBInstanceType": "Master",
            "Weight": "",
            "Availability": ""
        }
    ],
    "requestId": "C816A4BF-A6EC-4722-95F9-2055859CCFD2"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

