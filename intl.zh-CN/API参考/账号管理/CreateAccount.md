# CreateAccount {#doc_api_Rds_CreateAccount .reference}

调用CreateAccount接口创建管理数据库的账号。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   数据库状态为运行中；
-   没有超出单个实例内的最大账号数量。

**说明：** 

-   该参数仅适用于MySQL、MariaDB、SQL Server（除SQL Server 2017集群版）实例；
-   PostgreSQL、PPAS、SQL Server 2017集群版有且仅有一个高权限账号，其他账号由高权限账号连接数据库后通过SQL创建。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CreateAccount)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateAccount|系统规定参数，取值：**CreateAccount**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccountName|String|是|test1|数据库账号名称。

 **说明：** 

-   名称唯一；
-   以字母开头，以字母或数字结尾；
-   由小写字母、数字或下划线组成；
-   长度为2~16个字符；
-   其他非法字符，见[禁用关键字表](~~26317~~)。

 |
|AccountPassword|String|是|Test123456|数据库账号的密码。

 **说明：** 

-   长度为8~32个字符；
-   由大写字母、小写字母、数字、特殊字符中的任意三种组成；
-   特殊字符为!@\#$&%^\*\(\)\_+-=

 |
|AccountDescription|String|否|测试账号A|账号描述，长度为2~256个字符。以中文、英文字母开头，可以包含数字、中文、英文、下划线（\_）、短横线（-）。

 **说明：** 不能以 http:// 和 https:// 开头。

 |
|AccountType|String|否|Normal|账号类型，取值：

 -   **Normal**：普通账号；
-   **Super**：高权限账号。

 默认值：**Normal**。

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

http(s)://rds.aliyuncs.com/?Action=CreateAccount
&DBInstanceId=rm-uf6wjk5xxxxxxx
&AccountName=test1
&AccountPassword=Test123456
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateAccountResponse>
  <RequestId>D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD</RequestId>
</CreateAccountResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

