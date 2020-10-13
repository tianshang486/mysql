# Clear logs

Clears logs of an ApsaraDB for RDS instance.

-   For an RDS for MySQL instance, this operation uploads binlogs to an OSS bucket and then clears the local binlogs to release space.
-   For an RDS for SQL Server instance, this operation generates a temporary backup and then compresses transaction logs to release space.

**Note:** This operation is applicable to RDS for MySQL and RDS for SQL Server instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=PurgeDBInstanceLog&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|PurgeDBInstanceLog|The operation that you want to perform. Set the value to **PurgeDBInstanceLog**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotency of requests. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=PurgeDBInstanceLog
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<PurgeDBInstanceLogResponse>
	  <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId></PurgeDBInstanceLogResponse>
```

`JSON` format

```
{
  "RequestId": " 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

