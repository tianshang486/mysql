# Modify the endpoint and port of an ApsaraDB for RDS instance

Modifies the endpoint and port of an ApsaraDB for RDS instance.

ApsaraDB for RDS provides the internal and public endpoints. It allows hybrid access by using both a VPC endpoint and a classic network endpoint.

**Note:**

-   You can modify only the prefix of an endpoint.
-   The read/write splitting endpoint cannot be modified.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceConnectionString&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceConnectionString|The operation that you want to perform. Set the value to **ModifyDBInstanceConnectionString**. |
|ConnectionStringPrefix|String|Yes|rm-xxxxxx|The prefix of the endpoint. Only the prefix of the **CurrentConnectionString** parameter value can be modified.

 **Note:** The prefix must be 8 to 64 characters in length and can contain letters, digits, and hyphens \(-\). It cannot contain Chinese characters and special characters ~!\#%^&\*=+\\\|\{\};:'",<\>/? |
|CurrentConnectionString|String|Yes|rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com|The endpoint of the instance. It can be an internal endpoint, a public endpoint, or a classic network endpoint in the hybrid access mode.

 **Note:** The read/write splitting endpoint cannot be modified. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|Port|String|Yes|3306|The port of the database service. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyDBInstanceConnectionString
&DBInstanceId=rm-uf6wjk5xxxxxxx
&CurrentConnectionString=rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com
&ConnectionStringPrefix=rm-xxxxxx
&Port=3306
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBInstanceConnectionStringResponse>
         <RequestId>65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</ModifyDBInstanceConnectionStringResponse>
```

`JSON` format

```
{
  "RequestId": " 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

