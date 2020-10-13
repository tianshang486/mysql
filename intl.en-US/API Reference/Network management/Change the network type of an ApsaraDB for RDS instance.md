# Change the network type of an ApsaraDB for RDS instance

Changes the network type of an ApsaraDB for RDS instance.

This operation is used to switch the network type of an instance between a VPC and the classic network.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceNetworkType&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceNetworkType|The operation that you want to perform. Set the value to **ModifyDBInstanceNetworkType**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|InstanceNetworkType|String|Yes|Classic|The type of the target network. Valid values:

 -   **VPC**
-   **Classic** |
|RetainClassic|String|No|True|Specifies whether to retain the classic network endpoint. Valid values:

 -   **True**
-   **False**

 Default value: **False**.

 **Note:** This parameter is valid when the classic network is switched to a VPC. |
|ClassicExpiredDays|String|No|7|The retention days of the classic network endpoint. Valid values:**1 to 120**. Unit: days. Default value: **7**.

 **Note:** If **RetainClassic** is set to **True**, this parameter is required. |
|ReadWriteSplittingClassicExpiredDays|Integer|No|7|The retention days of the read/write splitting endpoint on the classic network. Valid values: **1 to 120**. Unit: days. Default value: **7**.

 **Note:** When an instance has the read/write splitting endpoint on the classic network and the **RetainClassic** parameter is set to **True**, this parameter is valid. |
|VPCId|String|No|vpc-uf6f7l4fg90xxxxxx|The ID of the VPC. |
|VSwitchId|String|No|vsw-uf6adz52c2pxxxxx|The ID of the VSwitch. If **VPCId** is entered, this parameter is required. |
|PrivateIpAddress|String|No|172.10.40.25|The private IP address of the instance. The private IP address must be within the CIDR block supported by the specified VSwitch. The system automatically assigns a private IP address based on the **VPCId** and **VSwitchId** parameters. |
|ReadWriteSplittingPrivateIpAddress|String|No|192.168.0.22|The read/write splitting private IP address of the instance. It must be the CIDR block supported by the specified VSwitch. The system automatically assigns a private IP address based on the **VPCId** and **VSwitchId** parameters.

 **Note:** When the current instance has the read/write splitting endpoint on the classic network, this parameter is valid. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|The ID of the request. |
|TaskId|String|1025486523574|The ID of the task. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyDBInstanceNetworkType
&DBInstanceId=rm-uf6wjk5xxxxxxx
&InstanceNetworkType=Classic
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBInstanceNetworkTypeResponse>
	  <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</ModifyDBInstanceNetworkTypeResponse>
```

`JSON` format

```
{
  "RequestId": " 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|400|NetTypeExists|Specified network type already exists.|The error message returned when the network type already exists. Check whether the parameter is correct.|
|403|OperationDenied.DBInstanceConnType|The current DB instance connection type does not support this operation.|The error message returned when the network connection type is not supported.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

