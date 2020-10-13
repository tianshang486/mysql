# Query performance metrics of a dedicated proxy

Queries performance metrics of the dedicated proxy for an ApsaraDB for RDS instance.

The Dedicated Proxy feature of ApsaraDB for RDS offers functions such as read/write splitting and short-lived connection optimization. For more information, see [Dedicated proxy](~~138705~~).

Before you call this operation, make sure that the following requirements are met:

-   The Dedicated Proxy feature must be enabled for the instance.
-   The instance must run one of the following MySQL versions and RDS editions:
    -   MySQL 8.0 with a minor engine version of 20191204 or later in the RDS Enterprise Edition
    -   MySQL 8.0 with a minor engine version of 20190915 or later in the RDS High-availability Edition
    -   MySQL 5.7 with a minor engine version of 20191128 or later in the RDS Enterprise Edition
    -   MySQL 5.7 with a minor engine version of 20190925 or later in the RDS High-availability Edition
    -   MySQL 5.6 with a minor engine version of 20200229 or later in the RDS High-availability Edition

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeDBProxyPerformance&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBProxyPerformance|The operation that you want to perform. Set the value to **DescribeDBProxyPerformance**. |
|DBInstanceId|String|Yes|rm-t4n3axxxxx|The ID of the instance. |
|EndTime|String|Yes|2019-09-21T18:00:00Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|MetricsName|String|Yes|Maxscale\_CpuUsage|The performance metrics to query. The **DBProxyInstanceType** parameter determines which performance metrics can be queried.

 If you set the **DBProxyInstanceType** parameter to **DedicatedProxy**, you can query only the **Maxscale\_CpuUsage** performance metric, which indicates CPU utilization. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|StartTime|String|Yes|2019-09-19T01:00:00Z|The start of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|DBProxyInstanceType|String|No|DedicatedProxy|The type of the proxy. Only a dedicated proxy is supported. Set the value to **DedicatedProxy**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|lsmexxxxxxx|The ID of the instance. |
|EndTime|String|2019-09-21T18:00:00Z|The end of the time range to query. |
|PerformanceKeys|Array| |An array that consists of performance metrics. |
|PerformanceKey| | | |
|Key|String|cpu\_ratio|The name of the performance metric. |
|ValueFormat|String|docker\_container\_cpu|The format of the performance metric value. |
|Values|Array| |An array that consists of performance metric values in the following format: \{value1, value2, ...\}. |
|PerformanceValue| | | |
|Date|String|2019-10-10T09:00:00Z|The date and time when the value of the performance metric was recorded. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Value|String|2.83|The value of the performance metric. |
|RequestId|String|DD31056F-A0CE-41D7-AD39-689B6ABAE982|The ID of the request. |
|StartTime|String|2019-09-19T01:00:00Z|The start of the time range to query. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeDBProxyPerformance
&RegionId=cn-hangzhou
&DBInstanceId=rm-t4n3axxxxx
&MetricsName=Maxscale_CpuUsage
&StartTime=2019-09-19T01:00:00Z
&EndTime=2019-09-21T18:00:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDBProxyPerformanceResponse>
  <DBInstanceId>lsmexxxxxxx</DBInstanceId>
  <RequestId>DD31056F-A0CE-41D7-AD39-689B6ABAE982</RequestId>
  <PerformanceKeys>
        <PerformanceKey>
              <Values>
                    <PerformanceValue>
                          <Value>2.83</Value>
                          <Date>2019-10-10T09:00:00Z</Date>
                    </PerformanceValue>
              </Values>
              <Key>cpu_ratio</Key>
              <ValueFormat>docker_container_cpu</ValueFormat>
        </PerformanceKey>
  </PerformanceKeys>
  <EndTime>2019-10-10T09:39:28Z</EndTime>
  <StartTime>2019-10-01T09:39:28Z</StartTime>
</DescribeDBProxyPerformanceResponse>
```

`JSON` format

```
{
	"DBInstanceId": "lsmexxxxxxx",
	"RequestId": "DD31056F-A0CE-41D7-AD39-689B6ABAE982",
	"PerformanceKeys": {
		"PerformanceKey": [
			{
				"Values": {
					"PerformanceValue": [
						{
							"Value": "2.83",
							"Date": "2019-10-10T09:00:00Z"
						}
					]
				},
				"Key": "cpu_ratio",
				"ValueFormat": "docker_container_cpu"
			}
		]
	},
	"EndTime": "2019-10-10T09:39:28Z",
	"StartTime": "2019-10-01T09:39:28Z"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

