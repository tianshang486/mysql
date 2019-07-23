# DescribeDTCSecurityIpHostsForSQLServer {#doc_api_Rds_DescribeDTCSecurityIpHostsForSQLServer .reference}

调用DescribeDTCSecurityIpHostsForSQLServer接口查询RDS实例的分布式事务白名单信息。

关于分布式事务白名单请参见[设置分布式事务白名单](~~124321~~)。

仅适用于如下版本实例：

-   SQL Server 2012/2016企业版高可用版
-   SQL Server 2012/2016标准版

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DescribeDTCSecurityIpHostsForSQLServer&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDTCSecurityIpHostsForSQLServer|系统规定参数，取值：**DescribeDTCSecurityIpHostsForSQLServer**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|RegionId|String|是|cn-hangzhou|地域ID，可以通过接口[DescribeRegions](~~26243~~)查看。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|实例ID。

 |
|IpHostPairNum|String|1|分布式事务白名单条目数。

 |
|Items| | |分布式事务白名单分组列表。

 |
|SecurityIpHosts|String|192.168.1.100,k3ecstest|ECS实例的IP地址和Windows系统的计算机名。格式：ip,hostname。多个实例之间以英文分号（;）隔开。

 |
|WhitelistGroupName|String|test1|分布式事务白名单分组名称。

 |
|RequestId|String|2CA62A70-2203-45C6-8E90-8971D5ACC0C2|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDTCSecurityIpHostsForSQLServer
&DBInstanceId=rm-uf6wjk5xxxxxxx
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

