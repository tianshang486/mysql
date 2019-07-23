# DescribeDBInstanceIpHostname {#doc_api_Rds_DescribeDBInstanceIpHostname .reference}

调用DescribeDBInstanceIpHostname接口查询RDS实例的底层ECS实例的hostname。

RDS实例是基于ECS实例搭建的，本接口用于[设置分布式事务白名单](~~124321~~)时查询RDS实例的底层ECS实例的hostname。

仅适用于如下版本实例：

-   SQL Server 2012/2016企业版高可用版
-   SQL Server 2012/2016标准版

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceIpHostname&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstanceIpHostname|系统规定参数，取值：**DescribeDBInstanceIpHostname**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|RDS实例ID。

 |
|RegionId|String|是|cn-hangzhou|RDS实例的地域ID，可以通过接口[DescribeRegions](~~26243~~)查看。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|实例ID。

 |
|IpHostnameInfos|String|172.16.xx.xx,sdxxxxxxxxB;172.16.xx.xx,sdxxxxxxxxA|RDS实例所在ECS实例的内网IP和ECS主机名，包含主备实例。格式：ip1,hostname1;ip2,hostname2。

 |
|RequestId|String|67CD4719-51E3-4A76-A38C-02F45FAE7E36|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDBInstanceIpHostname
&DBInstanceId=rm-uf6wjk5xxxxxxx	
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstanceIpHostnameResponse>
  <IpHostnameInfos>172.16.xx.xx,sdxxxxxxxxB;172.16.xx.xxx,sdxxxxxxxxA</IpHostnameInfos>
	  <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
	  <RequestId>67CD4719-51E3-4A76-A38C-02F45FAE7E36</RequestId>
</DescribeDBInstanceIpHostnameResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"IpHostnameInfos":"172.16.xx.xx,sdxxxxxxxxB;172.16.xx.xx,sdxxxxxxxxA",
	"RequestId":"67CD4719-51E3-4A76-A38C-02F45FAE7E36",
	"DBInstanceId":"rm-uf6wjk5xxxxxxx"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

