# Query latency between a primary ApsaraDB for RDS instance and its read-only instance

Queries the latency between a primary ApsaraDB for RDS instance and its read-only instance.

When you call this operation, make sure that the following requirements are met:

-   The instance runs the MySQL, PostgreSQL or PPAS database engine.
-   The instance has a read-only instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeReadDBInstanceDelay&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeReadDBInstanceDelay|The operation that you want to perform. Set the value to **DescribeReadDBInstanceDelay**. |
|DBInstanceId|String|Yes|rm-bpxxxxxxx|The ID of the primary RDS instance. |
|ReadInstanceId|String|Yes|rr-bpxxxxxxx|The ID of the read-only instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-bpxxxxxxx|The ID of the primary RDS instance. |
|DelayTime|Integer|0|The latency between the primary RDS instance and the read-only instance. |
|Items|Array| |A list of latency items. |
|Items| | | |
|DBInstanceId|String|rm-bpxxxxxxx|The ID of the primary RDS instance. |
|ReadDBInstanceNames|List|"ReadDBInstanceName": \["rr-bpxxxxx"\]|A list of information about the read-only instance.

 **Note:** This parameter is returned only when the primary RDS instance runs the MySQL database engine. |
|ReadDelayTimes|List|"ReadDelayTime": \["0"\]|A list of latency time.

 **Note:** This parameter is returned only when the primary RDS instance runs the MySQL database engine. |
|ReadonlyInstanceDelay|Array| |A list of Write Ahead Log \(WAL\) latency information.

 **Note:** This parameter is returned only when the primary RDS instance runs the PostgreSQL or PPAS database engine. |
|ReadonlyInstanceDelay| | | |
|FlushLag|String|0|The duration of delay in the persistence of WAL logs. Unit: seconds. |
|FlushLatency|String|0|The data size allowed for delay in the persistence of WAL logs. Unit: MB. |
|ReadDBInstanceName|String|rr-bpxxxxxxx|The ID of the read-only instance. |
|ReplayLag|String|0|The duration of delay in the playback of WAL logs. Unit: seconds. |
|ReplayLatency|String|0|The data size allowed for delay in the playback of WAL logs. Unit: MB. |
|SendLatency|String|0|The data size allowed for delay in the sending of WAL logs. Unit: MB. |
|WriteLag|String|0|The duration of delay in the write-back of WAL logs. Unit: seconds. |
|WriteLatency|String|0|The data size allowed for delay in the write-back of WAL logs. Unit: MB. |
|ReadDBInstanceId|String|rr-bpxxxxxxx|The ID of the read-only instance. |
|RequestId|String|F1BDDEA8-452D-450B-AB10-CD5C5BAFC5DF|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeReadDBInstanceDelay
&DBInstanceId=rm-bpxxxxxxx
&ReadInstanceId=rr-bpxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeReadDBInstanceDelayResponse>
  <Items>
        <Items>
              <ReadDelayTimes>
                    <ReadDelayTime>0</ReadDelayTime>
              </ReadDelayTimes>
              <ReadonlyInstanceDelay>
        </ReadonlyInstanceDelay>
              <DBInstanceId>rm-bpxxxxxxx</DBInstanceId>
              <ReadDBInstanceNames>
                    <ReadDBInstanceName>rr-bpxxxxxxx</ReadDBInstanceName>
              </ReadDBInstanceNames>
        </Items>
  </Items>
  <DelayTime>0</DelayTime>
  <DBInstanceId>rm-bpxxxxxxx</DBInstanceId>
  <RequestId>F1BDDEA8-452D-450B-AB10-CD5C5BAFC5DF</RequestId>
</DescribeReadDBInstanceDelayResponse>
```

`JSON` format

```
{
	"Items": {
		"Items": [
			{
				"ReadDelayTimes": {
					"ReadDelayTime": [
						"0"
					]
				},
				"ReadonlyInstanceDelay": {
					"ReadonlyInstanceDelay": []
				},
				"DBInstanceId": "rm-bpxxxxxxx",
				"ReadDBInstanceNames": {
					"ReadDBInstanceName": [
						"rr-bpxxxxxxx"
					]
				}
			}
		]
	},
	"DelayTime": "0",
	"DBInstanceId": "rm-bpxxxxxxx",
	"RequestId": "F1BDDEA8-452D-450B-AB10-CD5C5BAFC5DF"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

