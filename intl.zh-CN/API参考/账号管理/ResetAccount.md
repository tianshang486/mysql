# ResetAccount {#doc_api_1021631 .reference}

该接口用于重置高权限账号的权限。

**说明：** 该接口不适用于没有高权限账号的SQL Server 2008 R2实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ResetAccount)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ResetAccount|系统规定参数，取值：**ResetAccount**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|AccountName|String|是|test1|高权限账号名称。

 |
|AccountPassword|String|是|Test123456|设置新的高权限账号的密码。

 **说明：** 

-   长度为8~32个字符；
-   由大写字母、小写字母、数字、特殊字符中的任意三种组成；
-   特殊字符为!@\#$%^\*\(\)\_+-=

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|81BC9559-7B22-4B7F-B705-5F56DEECDEA7|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ResetAccount
&AccountName=test1
&AccountPassword=Test123456
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ResetAccountResponse>
  <RequestId>81BC9559-7B22-4B7F-B705-5F56DEECDEA7</RequestId>
</ResetAccountResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"81BC9559-7B22-4B7F-B705-5F56DEECDEA7"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

