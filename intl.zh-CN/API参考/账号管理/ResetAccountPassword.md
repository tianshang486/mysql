# ResetAccountPassword {#doc_api_1105982 .reference}

调用ResetAccountPassword接口重置账号密码。

实例状态需要为运行中，否则操作将失败。

**说明：** 该接口暂不支持对SQL Server 2017集群版、PostgreSQL、PPAS实例通过SQL创建的账号进行密码重置。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ResetAccountPassword)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ResetAccountPassword|系统规定参数，取值：**ResetAccountPassword**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccountName|String|是|test1|账号名称。

 |
|AccountPassword|String|是|Test123456|新密码。

 **说明：** 

-   长度为8~32个字符；
-   由大写字母、小写字母、数字、特殊字符中的任意三种组成；
-   特殊字符为!@\#$&%^\*\(\)\_+-=

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ResetAccountPassword
&DBInstanceId=rm-uf6wjk5xxxxxxx
&AccountName=test1
&AccountPassword=Test123456
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ResetAccountPasswordResponse>
  <RequestId>D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD</RequestId>
</ResetAccountPasswordResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

