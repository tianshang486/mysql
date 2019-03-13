# ModifyDBInstanceDescription {#doc_api_1063661 .reference}

调用ModifyDBInstanceDescription接口修改RDS实例的描述。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceDescription)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceDescription|系统规定参数，取值为**ModifyDBInstanceDescription**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|DBInstanceDescription|String|是|阿里云测试环境实例|RDS实例描述。

 **说明：** 长度为2-64个字符。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|17F57FEE-EA4F-4337-8D2E-9C23CAA63D74|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyDBInstanceDescription
&DBInstanceDescription=阿里云测试环境实例
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
< ModifyDBInstanceDescriptionResponse>
         <RequestId>17F57FEE-EA4F-4337-8D2E-9C23CAA63D74</RequestId>
</ModifyDBInstanceDescriptionResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

