# ModifySecurityIps {#doc_api_1106078 .reference}

You can call this operation to modify a whitelist.

When you call this operation, the instance must be in the running state.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifySecurityIps) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|ModifySecurityIps| The operation that you want to perform. Set this parameter to ModifySecurityIps.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|SecurityIps|String|Yes|10.23.12.24| The [IP address whitelist](../../../../intl.en-US/Quick Start for MySQL/Initial configuration/Configure a whitelist.md#) of the instance. Multiple IP addresses must be separated with commas \(,\), and cannot be the same. Up to 1,000 IP addresses can be entered in a single request. Two formats are supported:

 -   IP address. For example, 10.23.12.24.
-   CIDR block. For example, 10.23.12.24/24. /24 indicates the prefix length of the address is 24 bits. The prefix length varies from 1 to 32 bits.

 |
|DBInstanceIPArrayName|String|No|test| The name of the IP address whitelist to be modified. Default value: default.

 **Note:** You can create up to 50 whitelist groups for an instance.

 |
|DBInstanceIPArrayAttribute|String|No|hidden| The attribute of the whitelist group. It is empty by default.

 **Note:** The groups with hidden attribute are not displayed in the console. The groups with hidden attribute are used to access DTS and DRDS.

 |
|Modifymode|String|No|Cover| The modification method. Valid values:

 -   Cover: to overwrite the original IP address whitelist.
-   Append: to add IP addresses to the whitelist.
-   Delete: to delete IP addresses from the whitelist.

 Default value: Cover

 |
|WhitelistNetworkType|String|No|Classic| The network type of the whitelist. Valid values:

 -   Classic: classic networks in safe mode.
-   VPC: VPCs in safe mode.
-   Mix: In standard mode, the IP addresses are added to the normal group. In safe mode, the IP addresses are added to both classic network and VPC groups.

 Default value: Mix.

 |
|SecurityGroupId|String|No|rg-acfmyxxxxx| The ID of the security group.

 |
|SecurityIPType|String|No|IPv4| The type of the IP address.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF| The ID of the request.

 |
|TaskId|String|115855279| The ID of the task.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? &Action= ModifySecurityIps
&DBInstanceId=rm-uf6wjk5xxxxxxx
&SecurityIps=10.23.12.24 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_3gp_m78_spa}
<ModifySecurityIpsResponse>
	  <RequestId> 1AD222E9-E606-4A42-BF6D-8A4442913CEF</RequestId>
	  <TaskId>115855279</TaskId></ModifySecurityIpsResponse>
```

`JSON` format

``` {#codeblock_th2_040_lxk}
{
	"RequestId":" 1AD222E9-E606-4A42-BF6D-8A4442913CEF",
	"TaskId":115855279
}
```

## Error codes {#section_w37_c9t_ziz .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

