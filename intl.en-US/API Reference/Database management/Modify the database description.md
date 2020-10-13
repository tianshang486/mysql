# Modify the database description

Modifies the database description.

**Note:** This operation is not applicable to ApsaraDB for RDS instances that run PostgreSQL or PPAS.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyDBDescription&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBDescription|The operation that you want to perform. Set the value to **ModifyDBDescription**. |
|DBDescription|String|Yes|Test database A|The description of the database. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|DBName|String|Yes|testDB01|The name of the database. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|17F57FEE-EA4F-4337-8D2E-9C23CAA63D74|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyDBDescription
&DBDescription=Test database A
&DBInstanceId=rm-uf6wjk5xxxxxxx
&DBName=testDB01
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBDescriptionResponse>
      <RequestId> 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74</RequestId>
</ModifyDBDescriptionResponse>
```

`JSON` format

```
{
  "RequestId": " 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

