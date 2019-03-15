# ModifyAccountDescription {#doc_api_1064592 .reference}

调用ModifyAccountDescription接口修改数据库账号的描述。

**说明：** 该接口暂不支持SQL Server 2017集群版、PostgreSQL、PPAS实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyAccountDescription)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyAccountDescription|系统规定参数，取值：**ModifyAccountDescription**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccountName|String|是|test1|账号名称。

 |
|AccountDescription|String|是|测试账号A|账号描述，长度为2~256个字符。以中文、英文字母开头，可以包含可以包含数字、中文、英文、下划线（\_）、短横线（-）。

 **说明：** 不能以 http:// 和 https:// 开头。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|17F57FEE-EA4F-4337-8D2E-9C23CAA63D74|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyAccountDescription
&AccountDescription=测试账号A
&AccountName=test1
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyAccountDescriptionResponse>
  <RequestId> 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74</RequestId>
</ModifyAccountDescriptionResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

