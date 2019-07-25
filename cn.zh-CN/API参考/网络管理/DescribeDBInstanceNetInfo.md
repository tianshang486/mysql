# DescribeDBInstanceNetInfo {#doc_api_Rds_DescribeDBInstanceNetInfo .reference}

调用DescribeDBInstanceNetInfo接口查看实例的所有连接地址信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceNetInfo&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstanceNetInfo|系统规定参数，取值：**DescribeDBInstanceNetInfo**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|DBInstanceNetRWSplitType|String|否|Normal|连接地址类型，取值：

 -   **Normal**：普通连接地址；
-   **ReadWriteSplitting**：读写分离连接地址。

 **说明：** 默认返回所有类型连接地址。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|Flag|String|否|-|备用参数。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceNetInfos| | |实例的连接地址信息列表。

 |
|ConnectionString|String|rm-uf6wxxxxx.mysql.rds.aliyuncs.com|连接地址。

 |
|IPAddress|String|192.168.12.84|IP地址。

 |
|IPType|String|Public|网络类型。

 -   经典网络类型取值：
    -   **Inner**：内网；
    -   **Public**：外网。
-   VPC类型取值：
    -   **Private**：内网；
    -   **Public**：外网。

 |
|Port|String|3306|连接端口。

 |
|VPCId|String|vpc-uf6f7l4fg90xxxxxxxxxx|VPC ID。

 |
|VSwitchId|String|vsw-uf6adz52c2pxxxxxxxxxx|交换机ID。

 |
|ConnectionStringType|String|Normal|连接地址类型，取值：

 -   **Normal**：普通连接地址；
-   **ReadWriteSplitting**：读写分离连接地址。

 |
|MaxDelayTime|String|12|延迟阈值，只在读写分离连接地址返回该参数，单位：秒。

 **说明：** 超过该延迟阈值的只读实例不会被分配流量。

 |
|DistributionType|String|Standard|读请求分配策略，只在读写分离连接地址返回该参数，取值：

 -   **Standard**：按规格权重自动分配；
-   **Custom**：自定义分配权重。

 |
|DBInstanceWeights| | |实例权重信息列表，开通了读写分离地址的实例会返回该参数。

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|实例ID。

 |
|DBInstanceType|String|Master|实例类型，取值：

 -   **Master**：主实例；
-   **Readonly**：只读实例。

 |
|Weight|String|100|实例当前权重。

 |
|Availability|String|Unavailable|实例可用状态，取值：

 -   **Unavailable**：不可用；
-   **Available**：可用。

 |
|ExpiredTime|String|1209534|混访模式下，经典网络的剩余时间，单位：秒。

 |
|SecurityIPGroups| | |实例的IP白名单分组列表。

 |
|SecurityIPGroupName|String|Default|IP白名单分组名称。

 |
|SecurityIPs|String|127.0.0.1|白名单IP。

 |
|Upgradeable|String|Disabled|IP版本是否能够升级，取值：**true | false**

 **说明：** IPv4版本可以升级到IPv6版本。

 |
|InstanceNetworkType|String|VPC|网络类型，取值：

 -   **Classic**：经典网络；
-   **VPC**：专有网络。

 |
|RequestId|String|777C4593-8053-427B-99E2-105593277CAB|请求ID。

 |
|SecurityIPMode|String|safety|白名单模式，取值：

 -   **normal**：通用模式；
-   **safety**：高安全模式。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDBInstanceNetInfo
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstanceNetInfoResponse>
	  <dBInstanceNetInfos>
		    <connectionString>rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com</connectionString>
		    <connectionStringType>Normal</connectionStringType>
		    <iPAddress>192.168.xx.xx</iPAddress>
		    <iPType>Public</iPType>
		    <port>3306</port>
		    <upgradeable>Disabled</upgradeable>
		    <vPCId></vPCId>
	  </dBInstanceNetInfos>
	  <instanceNetworkType>Classic</instanceNetworkType>
	  <requestId>777C4593-8053-427B-99E2-105593277CAB</requestId>
</DescribeDBInstanceNetInfoResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"instanceNetworkType":"Classic",
	"requestId":"777C4593-8053-427B-99E2-105593277CAB",
	"dBInstanceNetInfos":[
		{
			"port":"3306",
			"dBInstanceWeights":[],
			"iPType":"Public",
			"connectionStringType":"Normal",
			"vPCId":"",
			"securityIPGroups":[],
			"connectionString":"rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com",
			"iPAddress":"192.168.xx.xx",
			"upgradeable":"Disabled"
		}
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

