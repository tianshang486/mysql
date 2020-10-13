# Change the monitoring frequency

Changes the monitoring frequency of an ApsaraDB for RDS instance.

Before you call this operation, make sure that you fully understand the billing methods and pricing of ApsaraDB for RDS. For more information, visit the [ApsaraDB for RDS pricing page](https://www.alibabacloud.com/product/apsaradb-for-rds#pricing).

Alibaba Cloud provides different monitoring frequencies for different instances. For more information, see [Set monitoring frequencies](~~26200~~).

**Note:** If your want to set the monitoring frequency to every few seconds, you must pay additional fees. For more information, see [Pricing, billing items, and billing methods](~~45020~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceMonitor&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceMonitor|The operation that you want to perform. Set the value to **ModifyDBInstanceMonitor**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|Period|String|Yes|60|The monitoring frequency. Valid values:

 -   **5**
-   **60**
-   **300**

 Unit: seconds. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxx|The client token that is used to ensure the idempotency of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can contain only ASCII characters and cannot exceed 64 characters in length. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|52B9805C-432C-4ED1-83FD-2F916B6D2733|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyDBInstanceMonitor
&DBInstanceId=rm-uf6wjk5xxxxxxx
&Period=60
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBInstanceMonitorResponse>
	  <requestId>52B9805C-432C-4ED1-83FD-2F916B6D2733</requestId>
</ModifyDBInstanceMonitorResponse>
```

`JSON` format

```
{
    "requestId": "52B9805C-432C-4ED1-83FD-2F916B6D2733"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|404|InvalidDBInstanceId.NotFound|The DBInstanceId provided does not exist in our records.|The error message returned when the instance ID does not exist. Confirm that the instance ID has not been deleted from the current account.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

