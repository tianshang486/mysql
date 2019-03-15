# DeleteAccount {#doc_api_1064578 .reference}

调用DeleteAccount接口删除数据库账号。

调用该接口时，实例状态需要为运行中，否则将操作失败：

**说明：** 该接口暂不支持SQL Server 2017集群版、PostgreSQL、PPAS实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DeleteAccount)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteAccount|系统规定参数，取值：**DeleteAccount**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccountName|String|是|test1|需要删除的数据库账号名称。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91E855E5-7E80-4955-929B-C74EE1D38C66|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DeleteAccount
&DBInstanceId=rm-uf6wjk5xxxxxxx
&AccountName=test1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteAccountResponse>
  <RequestID>91E855E5-7E80-4955-929B-C74EE1D38C66</RequestID>
</DeleteAccountResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestID":"91E855E5-7E80-4955-929B-C74EE1D38C66"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

