# ModifyDBInstanceConnectionMode {#doc_api_1091883 .reference}

调用ModifyDBInstanceConnectionMode接口开启或关闭数据库代理，已下线。

**说明：** 该API已下线。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceConnectionMode)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceConnectionMode|系统规定参数，取值：ModifyDBInstanceConnectionMode。

 |
|ConnectionMode|String|是|Performance|Performance为标准访问模式；Safe为高安全访问模式。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxx|实例名。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|OwnerAccount|String|否|testuser@aliyun.com|用户主账号。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://rds.aliyuncs.com/?Action=ModifyDBInstanceConnectionMode
&ConnectionMode=Performance
&DBInstanceId=rdsaiiabnaiiabn
&AccessKeyId=LTAIKw8gqPc3FvOw
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceConnectionModeResponse>
  <RequestId>D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD</RequestId>
</ModifyDBInstanceConnectionModeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

