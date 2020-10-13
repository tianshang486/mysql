# Release read/write splitting endpoint

Releases the read/write splitting endpoint.

This operation is applicable to the following instances with read/write splitting enabled:

-   MySQL 5.7 in the High-availability Edition \(with local SSDs\)
-   MySQL 5.6
-   SQL Server 2017 in the Cluster Edition

**Note:** This operation is supported for instances that use a shared database proxy.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ReleaseReadWriteSplittingConnection&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ReleaseReadWriteSplittingConnection|The operation that you want to perform. Set the value to **ReleaseReadWriteSplittingConnection**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the primary instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|5A77D650-27A1-4E08-AD9E-59008EDB6927|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ReleaseReadWriteSplittingConnection
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ReleaseReadWriteSplittingConnectionResponse>
	  <RequestID>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestID>
</ReleaseReadWriteSplittingConnectionResponse>
```

`JSON` format

```
{
    "RequestID":"5A77D650-27A1-4E08-AD9E-59008EDB6927"
  }
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

