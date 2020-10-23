# Apply for public endpoint

You can call the AllocateInstancePublicConnection operation to apply for a public endpoint for an ApsaraDB RDS instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=AllocateInstancePublicConnection&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AllocateInstancePublicConnection|The operation that you want to perform. Set the value to **AllocateInstancePublicConnection**. |
|ConnectionStringPrefix|String|Yes|test1234|The prefix of the public endpoint. A complete public endpoint is in the following format: <Prefix\>. <Database engine name\>.rds.aliyuncs.com. Example: test1234.mysql.rds.aliyuncs.com.

 **Note:** The prefix must be 5 to 40 characters in length. The prefix can contain letters, digits, and hyphens \(-\). However, the prefix cannot contain special characters. Special characters include ~ ! \# % ^ & \* = + \| \{ \} ; : ' " , < \> / ? |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|Port|String|Yes|3306|The public endpoint of the instance. Valid values: **1000 to 5999**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=AllocateInstancePublicConnection
&ConnectionStringPrefix=test1234
&DBInstanceId=rm-uf6wjk5xxxxxxx
&Port=3306
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AllocateInstancePublicConnectionResponse>
         <RequestId>65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</AllocateInstancePublicConnectionResponse>
```

`JSON` format

```
{
  "RequestId": " 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

