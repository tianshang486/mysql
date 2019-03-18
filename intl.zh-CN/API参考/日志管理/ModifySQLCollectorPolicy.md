# ModifySQLCollectorPolicy {#doc_api_1091160 .reference}

调用ModifySQLCollectorPolicy接口开启或关闭实例的SQL审计功能。

支持的实例版本如下：

-   MySQL 5.5
-   MySQL 5.6
-   MySQL 5.7高可用本地盘版
-   SQL Server 2008 R2
-   PostgreSQL
-   PPAS

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifySQLCollectorPolicy)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifySQLCollectorPolicy|系统规定参数，取值：**ModifySQLCollectorPolicy**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|SQLCollectorStatus|String|是|Enable|开启或关闭SQL审计，取值：**Enable | Disable**

 |
|StoragePeriod|Integer|否|30|SQL审计日志存储时长，取值：**1~30**，单位：天。默认值：**30**。

 **说明：** 在SQL审计开启时，可传入该参数修改存储时间，不传则与现有值保持一致。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifySQLCollectorPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxx
&SQLCollectorStatus=Enable
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifySQLCollectorPolicyResponse>
  <requestId>C3565F9F-76E9-4F7E-A662-D1B2488EC2FC</requestId>
  <sQLCollectorStatus>Enable</sQLCollectorStatus>
</ModifySQLCollectorPolicyResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"C3565F9F-76E9-4F7E-A662-D1B2488EC2FC",
	"sQLCollectorStatus":"Enable"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

