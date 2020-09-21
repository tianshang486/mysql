# Modify high availability mode

You can call this operation to modify the high availability mode and data replication mode for the instance.

## Debugging

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceHAConfig) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceHAConfig|The operation that you want to perform. Set this parameter to ModifyDBInstanceHAConfig. |
|DbInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|HAMode|String|Yes|RPO|The high availability mode. Valid values:

-   RPO: Data persistence is preferred. The instance preferentially guarantees data reliability to minimize data loss. This is best for users whose highest priority is data consistency.
-   RTO: Instance availability is preferred. The instance must restore services as soon as possible. This is best for users who require their databases to provide uninterrupted online service. |
|SyncMode|String|Yes|Sync|The [data replication mode](). Valid values:

-   Sync
-   Semi-sync
-   Async

**Note:** RDS for SQL Server 2017 Cluster Edition is not supported. |
|AccessKeyId|String|No|LTAIfCxxxxxxx|The AccessKey ID that Alibaba Cloud issues to a user for service access. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD|The ID of the request. |

## Examples

Sample requests

```

http(s)://rds.aliyuncs.com/? Action=ModifyDBInstanceHAConfig
&DbInstanceId=rm-uf6wjk5xxxxxxx
&HAMode=RPO
&SyncMode=Sync
&<Common request parameters>

```

Successful response examples

`XML` format

```
<ModifyDBInstanceHAConfigResponse>
	  <RequestId>D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD</RequestId></ModifyDBInstanceHAConfigResponse>
```

`JSON` format

```
{
	"RequestId":"D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

