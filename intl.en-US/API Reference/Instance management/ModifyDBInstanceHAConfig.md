# ModifyDBInstanceHAConfig {#doc_api_1063673 .reference}

You can call this operation to modify the high availability mode and data replication mode for the instance.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceHAConfig) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceHAConfig| The operation that you want to perform. Set this parameter to ModifyDBInstanceHAConfig.

 |
|DbInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|HAMode|String|Yes|RPO| The high availability mode. Valid values:

 -   RPO: Data persistence is preferred. The instance preferentially guarantees data reliability to minimize data loss. This is best for users whose highest priority is data consistency.
-   RTO: Instance availability is preferred. The instance must restore services as soon as possible. This is best for users who require their databases to provide uninterrupted online service.

 |
|SyncMode|String|Yes|Sync| The [data replication mode](../../../../intl.en-US/User Guide/Instance management/Modify the data replication mode.md#). Valid values:

 -   Sync
-   Semi-sync
-   Async

 **Note:** 

-   For ApsaraDB RDS for SQL Server 2012 or 2016 High-Availability Edition, the value is Sync or Async.
-   For ApsaraDB RDS for SQL Server 2017 Cluster Edition, the value is Semi-sync.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID that Alibaba Cloud issues to a user for service access.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=ModifyDBInstanceHAConfig
&DbInstanceId=rm-uf6wjk5xxxxxxx
&HAMode=RPO
&SyncMode=Sync
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_106_754_qoz}
<ModifyDBInstanceHAConfigResponse>
	  <RequestId>D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD</RequestId></ModifyDBInstanceHAConfigResponse>
```

`JSON` format

``` {#codeblock_psm_3a2_gty}
{
	"RequestId":"D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD"
}
```

## Error codes {#section_7fi_c74_tdd .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

