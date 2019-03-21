# MigrateSecurityIPMode {#doc_api_1106076 .reference}

调用MigrateSecurityIPMode接口把白名单从通用模式切换为高安全模式。

-   在通用模式下，白名单中的IP地址不区分经典网络和VPC网络，有安全风险，建议切换为高安全模式；
-   在高安全模式下，白名单中的IP地址分为两类：VPC的IP地址、经典网络及外网的IP地址。

**说明：** 

-   高安全模式无法切换回通用模式；
-   不支持SQL Server、MariaDB实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=MigrateSecurityIPMode)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|MigrateSecurityIPMode|系统规定参数，取值为**MigrateSecurityIPMode**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|实例ID。

 |
|RequestId|String|EF1E53AB-5625-49C7-ADF1-FBD0B6640D19|请求ID。

 |
|SecurityIPMode|String|safety|切换后的白名单模式，取值：**safety**。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=MigrateSecurityIPMode
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<MigrateSecurityIPModeResponse>
  <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
  <RequestId>EF1E53AB-5625-49C7-ADF1-FBD0B6640D19</RequestId>
  <SecurityIPMode>safety</SecurityIPMode>
</MigrateSecurityIPModeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"EF1E53AB-5625-49C7-ADF1-FBD0B6640D19",
	"DBInstanceId":"rm-uf6wjk5xxxxxxx",
	"SecurityIPMode":"safety"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

