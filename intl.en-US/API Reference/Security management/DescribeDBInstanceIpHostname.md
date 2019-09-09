# DescribeDBInstanceIpHostname {#doc_api_Rds_DescribeDBInstanceIpHostname .reference}

Obtains the hostname of the ECS instance connected to an RDS instance.

RDS instances are deployed on ECS instances. You can call this API action to obtain the hostname of the ECS instance on which an RDS instance is deployed.

This API action is applicable only to the following DB engine versions and editions:

-   SQL Server 2012/2016 Enterprise High-availability Edition
-   SQL Server 2012/2016 Standard Edition

## Debug {#api_explorer .section}

Use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceIpHostname&type=RPC&version=2014-08-15) to perform debug operations and generate SDK code examples.

## Request parameters {#parameters .section}

|ID|Type|Required|Example value|Description|
|--|----|--------|-------------|-----------|
|Action|String|Yes|DescribeDBInstanceIpHostname| The name of this API action. Value: DescribeDBInstanceIpHostname.

 |
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
|IpHostnameInfos|String|172.16.xx.xx,sdxxxxxxxxB;172.16.xx.xx,sdxxxxxxxxA| The internal IP address and hostname of the ECS instance where the RDS instance is deployed, including the corresponding master and slave instances. Format: ip1,hostname1;ip2,hostname2.

 |
|RequestId|String|67CD4719-51E3-4A76-A38C-02F45FAE7E36| The ID of the request.

 |

## Examples {#demo .section}

Request example:

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeDBInstanceIpHostname
&DBInstanceId=rm-uf6wjk5xxxxxxx	
&RegionId=cn-hangzhou
&<Common request parameters>

```

Response example:

`XML` format:

``` {#xml_return_success_demo}
<DescribeDBInstanceIpHostnameResponse>
  <IpHostnameInfos>172.16.xx.xx,sdxxxxxxxxB;172.16.xx.xxx,sdxxxxxxxxA</IpHostnameInfos>
	  <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
	  <RequestId>67CD4719-51E3-4A76-A38C-02F45FAE7E36</RequestId>
</DescribeDBInstanceIpHostnameResponse>
```

`JSON` format:

``` {#json_return_success_demo}
{
	"IpHostnameInfos":"172.16.xx.xx,sdxxxxxxxxB;172.16.xx.xx,sdxxxxxxxxA",
	"RequestId":"67CD4719-51E3-4A76-A38C-02F45FAE7E36",
	"DBInstanceId":"rm-uf6wjk5xxxxxxx"
}
```

## Errors {#section_9r4_9vj_iqp .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

