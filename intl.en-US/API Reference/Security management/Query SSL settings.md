# Query SSL settings

Queries Secure Sockets Layer \(SSL\) settings of an ApsaraDB for RDS instance.

**Note:** This operation is applicable to instances that run MySQL 5.6, MySQL 5.7, and MySQL 8.0 in the High-availability Edition with local SSDs and instances that run SQL Server.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceSSL&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceSSL|The operation that you want to perform. Set the value to **DescribeDBInstanceSSL**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ConnectionString|String|rm-uf6wjk5xxxxxx.mysql.rds.aliyuncs.com|The endpoint protected by the SSL certificate. |
|SSLExpireTime|String|2018-01-17T12:18:15Z|The time when the SSL certificate expires. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|RequireUpdate|String|Yes|Indicates whether the SSL certificate needs to be updated. Valid values: **Yes \| No**. |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|The ID of the request. |
|RequireUpdateReason|String|-|The reason why an update is needed. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeDBInstanceSSL
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDBInstanceSSLResponse>
	  <items>
		    <ConnectionString>rm-uf6wjk5xxxxxx.mysql.rds.aliyuncs.com</ConnectionString>
		    <SSLExpireTime>2018-01-17T12:18:15Z</SSLExpireTime>
		    <RequireUpdate>Yes</RequireUpdate>
		    <RequireUpdateReason></RequireUpdateReason>
	  </items>
	  <requestId>1AD222E9-E606-4A42-BF6D-8A4442913CEF</requestId>
</DescribeDBInstanceSSLResponse>
```

`JSON` format

```
{
    "items": [
        {
            "ConnectionString": "rm-uf6wjk5xxxxxx.mysql.rds.aliyuncs.com",
            "SSLExpireTime": "2018-01-17T12:18:15Z",
            "RequireUpdate": "Yes",
            "RequireUpdateReason": ""
        }
    ],
    "requestId": "1AD222E9-E606-4A42-BF6D-8A4442913CEF"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

