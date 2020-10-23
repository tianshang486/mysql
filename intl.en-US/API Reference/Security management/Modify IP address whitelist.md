# Modify IP address whitelist

You can call the ModifySecurityIps operation to modify an IP address whitelist of an ApsaraDB RDS instance.

An IP address whitelist contains the IP addresses of the devices that are granted access to the instance. For more information, see [Control access to an ApsaraDB RDS for MySQL instance](~~96118~~).

**Note:** Before you call this operation, make sure that the instance must be in the Running state.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifySecurityIps&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifySecurityIps|The operation that you want to perform. Set the value to **ModifySecurityIps**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|SecurityIps|String|Yes|10.23.12.24|The IP address whitelist of the instance. If the IP address whitelist contains more than one IP address, separate them with commas \(,\). Each IP address in the IP address whitelist must be unique. For more information, see [Control access to an ApsaraDB RDS for MySQL instance](~~43185~~). The following two formats are supported:

-   IP addresses, such 10.23.12.24.
-   Classless Inter-Domain Routing \(CIDR\) blocks, such as 10.23.12.0/24, where 24 indicates that the prefix of each IP address is 24-bit long. You can replace 24 with a value within the range of 1 to 32.

**Note:** A maximum of 1,000 IP addresses and CIDR blocks are allowed per instance. If you want to add a large number of IP addresses, we recommend that you merge them into CIDR blocks, such as 10.23.12.0/24. |
|DBInstanceIPArrayName|String|No|test|The name of the IP address whitelist. Default value: Default.

**Note:** A maximum of 200 IP address whitelists are allowed per instance. |
|DBInstanceIPArrayAttribute|String|No|hidden|The attribute of the IP address whitelist. This parameter is empty by default.

**Note:** The IP address whitelists that have the hidden attribute are not displayed in the ApsaraDB RDS console. These IP address whitelists are used to access Alibaba Cloud services such as Data Transmission Service \(DTS\). |
|SecurityIPType|String|No|IPv4|The type of IP address in the IP address whitelist. |
|WhitelistNetworkType|String|No|Classic|The network type of the IP address whitelist. Valid values:

-   **Classic**: classic network in enhanced whitelist mode
-   **VPC**: VPC in enhanced whitelist mode
-   **MIX**: standard whitelist mode

Default value: **MIX**.

**Note:** In standard whitelist mode, the IP addresses are added only to the IP address whitelist that runs in standard whitelist mode. In enhanced whitelist mode, the IP addresses are added to both the IP address whitelist of the classic network type and that of the VPC network type. |
|ModifyMode|String|No|Cover|The method that is used to modify the IP address whitelist. Valid values:

-   **Cover**
-   **Append**
-   **Delete**

Default value: **Cover**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|The ID of the request. |
|TaskId|String|115855279|The ID of the task. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifySecurityIps
&DBInstanceId=rm-uf6wjk5xxxxxxx
&SecurityIps=10.23.12.24
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifySecurityIpsResponse>
      <RequestId> 1AD222E9-E606-4A42-BF6D-8A4442913CEF</RequestId>
      <TaskId>115855279</TaskId>
</ModifySecurityIpsResponse>
```

`JSON` format

```
{
    "RequestId": " 1AD222E9-E606-4A42-BF6D-8A4442913CEF",
    "TaskId": 115855279
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

