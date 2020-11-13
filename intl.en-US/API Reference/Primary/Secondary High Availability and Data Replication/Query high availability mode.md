# Query high availability mode

You can call this operation to view the high availability modes and data replication modes of the instance.

## Debugging

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceHAConfig) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceHAConfig|The operation that you want to perform. Set this parameter to DescribeDBInstanceHAConfig. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxx|The ID of the instance. |
|AccessKeyId|String|No|LTAIfCxxxxxx|The AccessKey ID that Alibaba Cloud issues to a user for service access. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxx|The ID of the instance. |
|HAMode|String|RPO|The high availability mode. Valid values:

-   RPO: Data persistence is preferred. The instance preferentially guarantees data reliability to minimize data loss. This is best for users whose highest priority is data consistency.
-   RTO: Instance availability is preferred. The instance must restore services as soon as possible. This is best for users who require their databases to provide uninterrupted online service. |
|SyncMode|String|Sync|[The data replication mode](~~96055~~). Valid values:

-   Sync
-   Semi-sync
-   Async

**Note:**

-   For ApsaraDB RDS for SQL Server 2012 or 2016 High-availability Edition, the value is Sync or Async.
-   For ApsaraDB RDS for SQL Server 2017 Cluster Edition, the value is Async |
|HostInstanceInfos|N/A|N/A|The list of master and slave instances. |
|NodeId|String|3397027|The unique ID of the instance. |
|NodeType|String|Master|The type of the node. Valid values:

-   Master
-   Slave |
|RegionId|String|cn-hangzhou|The ID of the region. |
|ZoneId|String|cn-hangzhou-b|The ID of the zone. |
|SyncStatus|String|NotAvailable|The status of the synchronization. Valid values:

-   NotAvailable: Data cannot be synchronized due to faults.
-   Syncing: Data is being synchronized and a switchover may cause data loss.
-   Synchronized: Data has been synchronized.
-   NotSupport: The database engine or version does not support data synchronization. |
|LogSyncTime|String|2018-05-05T15:15:00Z|The time when the slave instance receives the logs. The time is in the following UTC format: yyyy-MM-ddTHH:mm:ssZ. |
|DataSyncTime|String|2018-05-05T15:15:00Z|The time when the slave instance finishes data synchronization. The time is in the following UTC format: yyyy-MM-ddTHH:mm:ssZ. |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|The ID of the request. |

## Examples

Sample requests

```

http(s)://rds.aliyuncs.com/? Action=DescribeDBInstanceHAConfig
&DBInstanceId=rm-uf6wjk5xxxxxx 
&<Common request parameters>

```

Successful response examples

`XML` format

```
<DescribeDBInstanceHAConfigResponse>
	  <dBInstanceId>rm-uf6wjk5xxxxxx</dBInstanceId>
	  <hAMode>RPO</hAMode>
	  <hostInstanceInfos>
		    <logSyncTime>2018-01-19T12:33:06Z</logSyncTime>
		    <nodeId>3397027</nodeId>
		    <nodeType>Slave</nodeType>
		    <regionId>cn-shenzhen</regionId>
		    <syncStatus>Syncing</syncStatus>
		    <zoneId>cn-shenzhen-b</zoneId>
	  </hostInstanceInfos>
	  <hostInstanceInfos>
		    <logSyncTime>2018-01-19T12:33:06Z</logSyncTime>
		    <nodeId>3397029</nodeId>
		    <nodeType>Master</nodeType>
		    <regionId>cn-shenzhen</regionId>
		    <syncStatus>Syncing</syncStatus>
		    <zoneId>cn-shenzhen-a</zoneId>
	  </hostInstanceInfos>
	  <requestId>F051AEB2-7655-4F0A-BC46-7E0C18A7910C</requestId>
	  <syncMode>Semi-sync</syncMode></DescribeDBInstanceHAConfigResponse>
```

`JSON` format

```
{
	"hostInstanceInfos":[
		{
			"nodeId":"3397027",
			"syncStatus":"Syncing",
			"logSyncTime":"2018-01-19T12:33:06Z",
			"nodeType":"Slave",
			"zoneId":"cn-shenzhen-b",
			"regionId":"cn-shenzhen"
		},
		{
			"nodeId":"3397029",
			"syncStatus":"Syncing",
			"logSyncTime":"2018-01-19T12:33:06Z",
			"nodeType":"Master",
			"zoneId":"cn-shenzhen-a",
			"regionId":"cn-shenzhen"
		}
	],
	"requestId":"F051AEB2-7655-4F0A-BC46-7E0C18A7910C",
	"syncMode":"Semi-sync",
	"hAMode":"RPO",
	"dBInstanceId":"rm-uf6wjk5xxxxxx"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

