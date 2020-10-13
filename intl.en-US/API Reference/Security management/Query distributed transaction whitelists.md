# Query distributed transaction whitelists

Queries distributed transaction whitelists of an ApsaraDB for RDS instance.

For more information, see [Configure a distributed transaction whitelist](~~124321~~).

This operation is applicable to instances that run one of the following SQL Server versions in the RDS High-Availability Edition: 2012 SE, 2012 EE, 2014 SE, 2016 SE, 2016 EE, and 2017 SE.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeDTCSecurityIpHostsForSQLServer&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDTCSecurityIpHostsForSQLServer|The operation that you want to perform. Set the value to **DescribeDTCSecurityIpHostsForSQLServer**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|IpHostPairNum|String|1|The number of distributed transaction whitelists. |
|Items|Array| |The list of distributed transaction whitelists. |
|WhiteListGroups| | | |
|SecurityIpHosts|String|192.168.1.100,k3ecstest|The IP address of the ECS instance and the hostname of the Windows computer. Format: IP address,Hostname. Multiple values are separated with semicolons \(;\). |
|WhitelistGroupName|String|test1|The name of the distributed transaction whitelist. |
|RequestId|String|2CA62A70-2203-45C6-8E90-8971D5ACC0C2|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeDTCSecurityIpHostsForSQLServer
&DBInstanceId=rm-uf6wjk5xxxxxxx
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
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

`JSON` format

```
{
	"Items": {
		"WhiteListGroups": [
			{
				"WhitelistGroupName": "test1",
				"SecurityIpHosts": "192.168.1.100,k3ecstest"
			}
		]
	},
	"IpHostPairNum": 1,
	"RequestId": "2CA62A70-2203-45C6-8E90-8971D5ACC0C2"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

