# Query SQL Explorer \(SQL Audit\) status

You can call the DescribeSQLCollectorPolicy operation to query the status of the SQL Explorer \(SQL Audit\) feature on an ApsaraDB RDS instance.

**Note:** This operation is not supported for instances that run SQL Server2017 EE.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeSQLCollectorPolicy&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSQLCollectorPolicy|The operation that you want to perform. Set the value to **DescribeSQLCollectorPolicy**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|ResourceGroupId|String|No|rg-acfmyxxxxxxxxxx|The ID of the resource group to which the instance belongs. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|SQLCollectorStatus|String|Enable|The status of the SQL Explorer \(SQL Audit\) feature. Valid values:

 -   **Enable**
-   **Disabled** |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|The ID of the request. |
|StoragePeriod|Integer|0|None |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=DescribeSQLCollectorPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeSQLCollectorPolicyResponse>
	  <requestId>C3565F9F-76E9-4F7E-A662-D1B2488EC2FC</requestId>
	  <sQLCollectorStatus>Enable</sQLCollectorStatus></DescribeSQLCollectorPolicyResponse>
```

`JSON` format

```
{
    "requestId": "C3565F9F-76E9-4F7E-A662-D1B2488EC2FC", 
    "sQLCollectorStatus": "Enable"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

