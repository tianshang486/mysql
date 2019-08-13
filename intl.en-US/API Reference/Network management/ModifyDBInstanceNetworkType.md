# ModifyDBInstanceNetworkType {#doc_api_1091246 .reference}

You can call this operation to switch the network type of an RDS instance.

This operation is used to switch the network type of an instance between a VPC and a classic network.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceNetworkType) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceNetworkType| The operation that you want to perform. Set this parameter to ModifyDBInstanceNetworkType.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|InstanceNetworkType|String|Yes|Classic| The type of the target network. Valid values:

 -   VPC
-   Classic

 |
|RetainClassic|String|No|True| Indicates whether to retain the classic network address. Valid values:

 -   True
-   False

 Default value: False.

 **Note:** This parameter is valid when a classic network is switched to a VPC.

 |
|ClassicExpiredDays|String|No|7| The retention days of the classic network. Value range: 1 to 120. Unit: day. Default value: 7.

 **Note:** If the RetainClassic parameter is set to True, this parameter is required.

 |
|ReadWriteSplittingClassicExpiredDays|Integer|No|7| The retention days of the read/write splitting address for a classic network. Value range: 1 to 120. Unit: day. Default value: 7.

 **Note:** When an instance has the read/write splitting address of a classic network, and the RetainClassic parameter is set to True, this parameter is valid.

 |
|VPCId|String|No|vpc-uf6f7l4fg90xxxxxx| The ID of the VPC.

 |
|VSwitchId|String|No|vsw-uf6adz52c2pxxxxx| The ID of the VSwitch. If the VPCId is entered, this parameter is required.

 |
|PrivateIpAddress|String|No|172.10.40.25| The private IP address of the instance. It must be within the IP address range of the specified VSwitch. The system automatically allocates the private IP addresses through the VPCId and VSwitchId parameters by default.

 |
|ReadWriteSplittingPrivateIpAddress|String|No|192.168.0.22| The read/write splitting private IP address of the instance. It must be within the IP address range of the specified VSwitch. The system automatically allocates the private IP addresses through the VPCId and VSwitchId parameters by default.

 **Note:** When the current instance has the read/write splitting address of a classic network, this parameter is valid.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF| The ID of the request.

 |
|TaskId|String|1025486523574| The ID of the task.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=ModifyDBInstanceNetworkType
&DBInstanceId=rm-uf6wjk5xxxxxxx 
&InstanceNetworkType=Classic 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_w2d_u0x_rl3}
<ModifyDBInstanceNetworkTypeResponse>
	  <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId></ModifyDBInstanceNetworkTypeResponse>
```

`JSON` format

``` {#codeblock_d77_zij_j9m}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## Error codes {#section_2a6_r8r_4bk .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|NetTypeExists|Specified network type already exists.|The error message returned when the network type already exists. Check whether this parameter is correct.|
|403|OperationDenied.DBInstanceConnType|The current DB instance connection type does not support this operation.|The error message returned when the network connection type is not supported.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

