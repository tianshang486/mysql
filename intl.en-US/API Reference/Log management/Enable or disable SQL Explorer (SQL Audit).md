# Enable or disable SQL Explorer \(SQL Audit\)

You can call the ModifySQLCollectorPolicy operation to enable or disable the SQL Explorer \(SQL Audit\) feature of an ApsaraDB for RDS instance.

Before you call this operation, make sure that the instance must run one of the following database engines:

-   MySQL
-   -   PostgreSQL
-   PPAS

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifySQLCollectorPolicy&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifySQLCollectorPolicy|The operation that you want to perform. Set the value to **ModifySQLCollectorPolicy**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|SQLCollectorStatus|String|Yes|Enable|Specifies to enable or disable the SQL Explorer \(SQL Audit\) feature. Valid values: **Enable and Disabled**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifySQLCollectorPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxx
&SQLCollectorStatus=Enable
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifySQLCollectorPolicyResponse>
      <requestId>C3565F9F-76E9-4F7E-A662-D1B2488EC2FC</requestId>
</ModifySQLCollectorPolicyResponse>
```

`JSON` format

```
{
    "requestId": "C3565F9F-76E9-4F7E-A662-D1B2488EC2FC", 
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

