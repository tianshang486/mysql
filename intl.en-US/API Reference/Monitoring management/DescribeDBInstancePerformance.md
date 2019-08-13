# DescribeDBInstancePerformance {#doc_api_1106175 .reference}

You can call this operation to view the performance data of an instance.

You can view the performance data of an instance over a specified period of time based on the performance parameters. Based on different editions, [monitoring frequencies](../../../../intl.en-US/User Guide/Monitoring and Alarming/Set the monitoring frequency.md#) \([ModifyDBInstanceMonitor](intl.en-US/API Reference/Monitoring management/ModifyDBInstanceMonitor.md#)\), and query time ranges, three output formats are provided as follows:

-   For editions excluding MySQL 5.7 High-availability Edition \(with SSDs\) and MariaDB editions
    -   The monitoring frequency is 5 seconds:
        -   When the query time range is greater than 7 days, the performance data is collected at 1-day intervals.
        -   When the query time range is greater than 1 day but less than or equal to 7 days, the performance data is collected at 1-hour intervals.
        -   When the query time range is greater than 1 hour but less than or equal to 1 day, the performance data is collected at 1-minute intervals.
        -   When the query time range is less than or equal to 1 hour, the performance data is collected at 5-minute intervals.
    -   The monitoring frequency is 60 seconds:
        -   When the query time range is greater than 30 days, the performance data is collected at 1-day intervals.
        -   When the query time range is greater than 7 days but less than or equal to 30 days, the performance data is collected at 1-hour intervals.
        -   When the query time range is less than or equal to 7 days, the performance data is collected at 1-minute intervals.
    -   The monitoring frequency is 300 seconds.
        -   When the query time range is greater than 30 days, the performance data is collected at 1-day intervals.
        -   When the query time range is greater than 7 days but less than or equal to 30 days, the performance data is collected at 1-hour intervals.
        -   When the query time range is less than or equal to 7 days, the performance data is collected at 5-minute intervals.
-   For MySQL 5.7 High-availability Edition \(with SSDs\) and MariaDB editions
    -   When the query time range is greater than 30 days, the performance data is collected at 1-day intervals.
    -   When the query time range is greater than 7 days but less than or equal to 30 days, the performance data is collected at 1-hour intervals.
    -   When the query time range is less than or equal to 7 days, the performance data is collected at 1-minute intervals.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstancePerformance) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|DescribeDBInstancePerformance| The operation that you want to perform. Set this parameter to DescribeDBInstancePerformance.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|Key|String|Yes|MySQL\_Sessions| The performance metrics you want to query. Multiple metrics are separated by commas \(,\). For more information, see [Performance parameter table](intl.en-US/API Reference/Appendix/Performance parameter table.md#).

 **Note:** When the key parameter is set to MySQL\_SpaceUsage or SQLServer\_SpaceUsage, the performance metrics can be queried only when the query time range is less than or equal to one day.

 |
|StartTime|String|Yes|2012-06-08T15:00Z| The start time of the query. Format: yyyy-MM-ddTHH:mm:ssZ.

 |
|EndTime|String|Yes|2012-06-18T15:00Z| The end time of the query. Format: yyyy-MM-ddTHH:mm:ssZ.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx| The ID of the instance.

 |
|Engine|String|MySQL| The type of the database.

 |
|StartTime|String|2012-06-10T15:00Z| The start time of the query. Format: yyyy-MM-ddTHH:mm:ssZ.

 |
|EndTime|String|2012-06-19T15:00Z| The end time of the query. Format: yyyy-MM-ddTHH:mm:ssZ.

 |
|PerformanceKeys| | | The performance parameters of the instance.

 |
|Key|String|MySQL\_Sessions| The performance parameters.

 |
|Unit|String|KB| The unit of the performance data.

 |
|ValueFormat|String|recv\_k&sent\_k| The format of the performance value. If the performance value is composed of multiple parameters, separate them with ampersands \(&\). For example, com\_delete&com\_insert&com\_insert\_select&com\_replace.

 |
|Values| | | The format of the array, such as \{value1, value2, …\}.

 |
|Value|String|0.0&13.6| The performance value.

 |
|Date|String|2011-05-30T03:29:00Z| The date of the record. Format: yyyy-MM-ddTHH:mm:ssZ.

 |
|RequestId|String|A5409D02-D661-4BF3-8F3D-0A814D0574E7| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeDBInstancePerformance
&DBInstanceId= rm-uf6wjk5xxxxxxx 
&Key=MySQL_Sessions
&StartTime=2012-06-08T15:00Z 
&EndTime=2012-06-18T15:00Z 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_osf_se6_h3w}
<DescribeDBInstancePerformanceResponse>
	  <RequestId>A5409D02-D661-4BF3-8F3D-0A814D0574E7</RequestId>
	  <DBInstanceID> rm-uf6wjk5xxxxxxx</DBInstanceID>
	  <StartTime>2012-06-11T15:00Z</StartTime>
	  <EndTime>2013-10-17T15:00Z</EndTime>
	  <Engine>MySQL</Engine>
	  <PerformanceKeys>
		    <PerformanceKey>
			      <Key>MySQL_NetworkTraffic</Key>
			      <Unit>KB</Unit>
			      <ValueFormat>recv_k&amp;sent_k</ValueFormat>
			      <Values></Values>
		    </PerformanceKey>
	  </PerformanceKeys></DescribeDBInstancePerformanceResponse>
```

`JSON` format

``` {#codeblock_xy9_n0q_auk}
{
	"DBInstanceID":" rm-uf6wjk5xxxxxxx",
	"RequestId":"A5409D02-D661-4BF3-8F3D-0A814D0574E7",
	"PerformanceKeys":{
		"PerformanceKey":[
			{
				"Values":{
					"PerformanceValue":[]
				},
				"Key":"MySQL_NetworkTraffic",
				"Unit":"KB",
				"ValueFormat":"recv_k&sent_k"
			}
		]
	},
	"EndTime":"2013-10-17T15:00Z",
	"StartTime":"2012-06-11T15:00Z",
	"Engine":"MySQL"
}
```

## Error codes { .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

