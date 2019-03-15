# ModifyDBInstanceSSL {#doc_api_1067141 .reference}

调用ModifyDBInstanceSSL接口修改实例SSL链路。

该接口用于为实例设置[SSL](~~32474~~)（Secure Sockets Layer）加密。

**说明：** 仅支持MySQL 5.6、MySQL 5.7高可用本地盘版和SQL Server 2008 R2实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceSSL)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceSSL|系统规定参数，取值：**ModifyDBInstanceSSL**。

 |
|ConnectionString|String|是|rm-uf6wjk5xxxxx.mysql.rds.aliyuncs.com|需要创建或更新SSL证书的连接地址。

 **说明：** 每个实例只能有一个连接地址受SSL保护。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|777C4593-8053-427B-99E2-105593277CAB|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyDBInstanceSSL
&ConnectionString=rm-uf6wjk5xxxxx.mysql.rds.aliyuncs.com
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceSSLResponse>
  <requestId>777C4593-8053-427B-99E2-105593277CAB</requestId>
</ModifyDBInstanceSSLResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"777C4593-8053-427B-99E2-105593277CAB"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

