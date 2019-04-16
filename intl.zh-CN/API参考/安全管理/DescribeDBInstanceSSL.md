# DescribeDBInstanceSSL {#doc_api_Rds_DescribeDBInstanceSSL .reference}

调用DescribeDBInstanceSSL接口查询实例SSL设置。

**说明：** 该接口支持MySQL 5.6、MySQL 5.7高可用本地盘版和SQL Server所有版本。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceSSL)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstanceSSL|系统规定参数，取值：**DescribeDBInstanceSSL**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ConnectionString|String|rm-uf6wjk5xxxxxx.mysql.rds.aliyuncs.com|受SSL保护的连接地址。

 |
|SSLExpireTime|String|2018-01-17T12:18:15Z|SSL证书有效期。

 |
|RequireUpdate|String|Yes|是否需要更新，取值：**Yes | No**

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDBInstanceSSL
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstanceSSLResponse>
  <items>
    <ConnectionString>rm-uf6wjk5xxxxxx.mysql.rds.aliyuncs.com</ConnectionString>
    <SSLExpireTime>2018-01-17T12:18:15Z</SSLExpireTime>
    <RequireUpdate>Yes</RequireUpdate>
    <RequireUpdateReason/>
  </items>
  <requestId>1AD222E9-E606-4A42-BF6D-8A4442913CEF</requestId>
</DescribeDBInstanceSSLResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"1AD222E9-E606-4A42-BF6D-8A4442913CEF",
	"items":[
		{
			"RequireUpdate":"Yes",
			"ConnectionString":"rm-uf6wjk5xxxxxx.mysql.rds.aliyuncs.com",
			"RequireUpdateReason":"",
			"SSLExpireTime":"2018-01-17T12:18:15Z"
		}
	]
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

