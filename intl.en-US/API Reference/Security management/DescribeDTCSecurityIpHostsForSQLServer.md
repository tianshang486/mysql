# DescribeDTCSecurityIpHostsForSQLServer {#doc_api_Rds_DescribeDTCSecurityIpHostsForSQLServer .reference}

Obtains the distributed transaction whitelist information of an RDS instance.

This API action is applicable only to the following DB engine versions and editions:

-   SQL Server 2012/2016 Enterprise High-availability Edition
-   SQL Server 2012/2016 Standard Edition

## Debug {#api_explorer .section}

Use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDTCSecurityIpHostsForSQLServer&type=RPC&version=2014-08-15) to perform debug operations and generate SDK code examples.

## Request parameters {#parameters .section}

|ID|Type|Required|Example value|Description|
|--|----|--------|-------------|-----------|
|Action|String|Yes|DescribeDTCSecurityIpHostsForSQLServer|The name of this API action. Value: DescribeDTCSecurityIpHostsForSQLServer.|
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the specified RDS instance.

 |
|RegionId|String|Yes|cn-hangzhou|The ID of the region to which the specified RDS instance belongs. You can call the [DescribeRegions](intl.en-US/API Reference/Instance management/DescribeRegions.md#) API action to obtain this region ID.|
|AccessKeyId|String|No|LTAIfCxxxxxxxxxx| The AccessKey ID that Alibaba Cloud issues to a user for service access.

 |

## Response elements {#resultMapping .section}

|ID|Type|Example value|Description|
|--|----|-------------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx| The ID of the specified RDS instance.

 |
|IpHostPairNum|String|1| The number of distributed transaction whitelists.

 |
|Items|N/A|N/A| The list of distributed transaction whitelist groups.

 |
|SecurityIpHosts|String|192.168.1.100,k3ecstest| The IP address of the ECS instance connected to the specified RDS instance, and the device name of the Windows-based system where the ECS instance is located. Format: ip,hostname. If the RDS instance is connected to more than one ECS instance, separate their information by using semicolons \(;\).

 |
|WhitelistGroupName|String|test1| The name of a distributed transaction whitelist group.

 |
|RequestId|String|2CA62A70-2203-45C6-8E90-8971D5ACC0C2| The ID of the request.

 |

## Examples {#demo .section}

Request example:

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeDTCSecurityIpHostsForSQLServer
&DBInstanceId=rm-uf6wjk5xxxxxxx
&RegionId=cn-hangzhou
&<Common request parameters>

```

Response example:

`XML` format:

``` {#xml_return_success_demo}
<DescribeDTCSecurityIpHostsForSQLServerResponse>
  <Items>
		    <WhiteListGroups>
			      <WhitelistGroupName>test1</WhitelistGroupName>
			      <SecurityIpHosts>192.168.1.100,k3ecstest</SecurityIpHosts>
		    </WhiteListGroups>
	  </Items>
	  <IpHostPairNum>1</IpHostPairNum>
	  <RequestId>2CA62A70-2203-45C6-8E90-8971D5ACC0C2</RequestId>
</DescribeDTCSecurityIpHostsForSQLServerResponse>
```

`JSON` format:

``` {#json_return_success_demo}
{
	"IpHostPairNum":1,
	"Items":{
		"WhiteListGroups":[
			{
				"WhitelistGroupName":"test1",
				"SecurityIpHosts":"192.168.1.100,k3ecstest"
			}
		]
	},
	"RequestId":"2CA62A70-2203-45C6-8E90-8971D5ACC0C2"
}
```

## Errors {#section_pjp_fbi_e4j .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

