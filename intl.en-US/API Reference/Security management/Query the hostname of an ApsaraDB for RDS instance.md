# Query the hostname of an ApsaraDB for RDS instance

Queries the hostname of an ApsaraDB for RDS instance.

RDS instances are deployed based on ECS instances. This operation is used to query the hostname of an RDS instance. The hostname is required when you [configure a distributed transaction whitelist](~~124321~~).

The RDS instance is in the High-availability Edition and runs one of the following SQL Server editions: 2012 SE, 2012 EE, 2014 SE, 2016 SE, 2016 EE, and 2017 SE.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceIpHostname&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceIpHostname|The operation that you want to perform. Set the value to **DescribeDBInstanceIpHostname**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the RDS instance. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the RDS instance. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the RDS instance. |
|IpHostnameInfos|String|172.16.xx.xx,sdxxxxxxxxB;172.16.xx.xx,sdxxxxxxxxA|The private IP addresses and hostnames of the primary and standby RDS instances. Format: IP address 1,Hostname 1;IP address 2,Hostname 2. |
|RequestId|String|67CD4719-51E3-4A76-A38C-02F45FAE7E36|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeDBInstanceIpHostname
&DBInstanceId=rm-uf6wjk5xxxxxxx	
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDBInstanceIpHostnameResponse>
  <IpHostnameInfos>172.16.xx.xx,sdxxxxxxxxB;172.16.xx.xxx,sdxxxxxxxxA</IpHostnameInfos>
	  <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
	  <RequestId>67CD4719-51E3-4A76-A38C-02F45FAE7E36</RequestId>
</DescribeDBInstanceIpHostnameResponse>
```

`JSON` format

```
{
	"IpHostnameInfos": "172.16.xx.xx,sdxxxxxxxxB;172.16.xx.xx,sdxxxxxxxxA",
	"DBInstanceId": "rm-uf6wjk5xxxxxxx",
	"RequestId": "67CD4719-51E3-4A76-A38C-02F45FAE7E36"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

