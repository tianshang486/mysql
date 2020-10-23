# Release instance

You can call the DeleteDBInstance operation to release an ApsaraDB RDS instance.

Before you call this operation, make sure that the following requirements are met:

-   The instance must be in the Running state.
-   The read/write splitting function is disabled for the instance.
-   The instance is a primary, read-only, disaster recovery, or temporary instance. If the instance is a primary instance, it must use the pay-as-you-go billing method.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DeleteDBInstance&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteDBInstance|The operation that you want to perform. Set the value to **DeleteDBInstance**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx|The ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DeleteDBInstance
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteDBInstanceResponse>
      <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</DeleteDBInstanceResponse>
```

`JSON` format

```
{
    "RequestId": " 65BDA532-28AF-4122-AA39-B382721EEE64"
  }
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

