# ModifyDTCSecurityIpHostsForSQLServer {#doc_api_Rds_ModifyDTCSecurityIpHostsForSQLServer .reference}

Configures a distributed transaction whitelist for an RDS instance.

The distributed transaction whitelist allows for distributed transactions between the RDS and ECS instances.

This API action is applicable only to the following DB engine versions and editions:

-   SQL Server 2012/2016 Enterprise High-availability Edition
-   SQL Server 2012/2016 Standard Edition

## Debug {#api_explorer .section}

Use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDTCSecurityIpHostsForSQLServer&type=RPC&version=2014-08-15) to perform debug operations and generate SDK code examples.

## Request parameters {#parameters .section}

|ID|Type|Required|Example value|Description|
|--|----|--------|-------------|-----------|
|Action|String|Yes|ModifyDTCSecurityIpHostsForSQLServer|The ID of this API action. Value: ModifyDTCSecurityIpHostsForSQLServer.|
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the specified RDS instance.

 |
|RegionId|String|Yes|cn-hangzhou|The ID of the region to which the specified RDS instance belongs. You can call the [DescribeRegions](intl.en-US/API Reference/Instance management/DescribeRegions.md#) API action to obtain this region ID.|
|SecurityIpHosts|String|Yes|192.168.1.100,k3ecstest| The IP address of the ECS instance connected to the specified RDS instance, and the device name of the Windows-based system where the ECS instance is located. Format: ip,hostname. If the RDS instance is connected to more than one ECS instance, separate their information by using semicolons \(;\).

 |
|WhiteListGroupName|String|Yes|test1| The name of the whitelist group.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxxxxx| The AccessKey ID that Alibaba Cloud issues to a user for service access.

 |

## Response elements {#resultMapping .section}

|ID|Type|Example value|Description|
|--|----|-------------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx| The ID of the specified RDS instance.

 |
|DTCSetResult|String|Success| Whether configuring the whitelist succeeded or failed. Valid values:

 -   Success
-   Fail

 |
|RequestId|String|671B6D32-B907-4EFF-A3B7-94D2EAD5E3A3| The ID of the request.

 |
|TaskId|String|178968983| The ID of the task for configuring the whitelist.

 |

## Examples {#demo .section}

Request example:

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=ModifyDTCSecurityIpHostsForSQLServer
&DBInstanceId=rm-uf6wjk5xxxxxxx
&RegionId=cn-hangzhou
&SecurityIpHosts=192.168.1.100,k3ecstest
&WhiteListGroupName=test1
&<Common request parameters>

```

Response example:

`XML` format:

``` {#xml_return_success_demo}
<ModifyDTCSecurityIpHostsForSQLServerResponse>
  <RequestId>671B6D32-B907-4EFF-A3B7-94D2EAD5E3A3</RequestId>
	  <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
	  <DTCSetResult>Success</DTCSetResult>
	  <TaskId>178968983</TaskId>
</ModifyDTCSecurityIpHostsForSQLServerResponse>
```

`JSON` format:

``` {#json_return_success_demo}
{
	"DBInstanceId":"rm-uf6wjk5xxxxxxx",
	"RequestId":"671B6D32-B907-4EFF-A3B7-94D2EAD5E3A3",
	"DTCSetResult":"Success",
	"TaskId":178968983
}
```

## Errors {#section_ivs_2qm_ukw .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

