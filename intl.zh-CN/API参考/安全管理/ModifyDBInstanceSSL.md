# ModifyDBInstanceSSL {#doc_api_Rds_ModifyDBInstanceSSL .reference}

调用ModifyDBInstanceSSL接口修改实例SSL链路。

该接口用于为实例设置[SSL](~~32474~~)（Secure Sockets Layer）加密。

**说明：** 

-   支持MySQL 5.6、MySQL 5.7/8.0高可用本地盘版和SQL Server所有版本。
-   读写分离地址不支持SSL加密。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceSSL&type=RPC&version=2014-08-15)

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

## 返回数据 {#resultMapping .section}

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
	  <requestId>777C4593-8053-427B-99E2-105593277CAB</requestId></ModifyDBInstanceSSLResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"777C4593-8053-427B-99E2-105593277CAB"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

