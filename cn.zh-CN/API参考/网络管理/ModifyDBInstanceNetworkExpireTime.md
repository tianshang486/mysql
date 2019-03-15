# ModifyDBInstanceNetworkExpireTime {#doc_api_1072757 .reference}

调用ModifyDBInstanceNetworkExpireTime接口修改连接地址过期时间。

**说明：** 当实例在混访模式下（同时包含VPC和经典网络两种网络类型的实例），该接口用于延长保留的经典网络地址过期时间。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceNetworkExpireTime)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceNetworkExpireTime|系统规定参数，取值：**ModifyDBInstanceNetworkExpireTime**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|ConnectionString|String|是|rm-uf6wjk5xxxxx.mysql.rds.aliyuncs.com| 

 要延期的经典网络连接地址，经典网络连接地址有两种：

 -   经典网络内网地址；
-   经典网络读写分离地址。

 |
|ClassicExpiredDays|Integer|是|7|经典网络连接地址保留天数，取值：**1-120**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|4C467B38-3910-447D-87BC-AC049166F216|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyDBInstanceNetworkExpireTime
&DBInstanceId=rm-uf6wjk5xxxxxxx
&ConnectionString=rm-uf6wjk5xxxxx.mysql.rds.aliyuncs.com
&ClassicExpiredDays=7
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceNetworkExpireTimeResponse>
  <RequestId>4C467B38-3910-447D-87BC-AC049166F216</RequestId>
</ModifyDBInstanceNetworkExpireTimeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"4C467B38-3910-447D-87BC-AC049166F216"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

