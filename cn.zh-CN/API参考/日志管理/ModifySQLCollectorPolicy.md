# ModifySQLCollectorPolicy {#doc_api_Rds_ModifySQLCollectorPolicy .reference}

调用ModifySQLCollectorPolicy接口开启或关闭实例的SQL审计功能。

支持的实例版本如下：

-   MySQL 5.5
-   MySQL 5.6
-   MySQL 5.7高可用本地盘版
-   SQL Server 2008 R2
-   PostgreSQL
-   PPAS

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=ModifySQLCollectorPolicy&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifySQLCollectorPolicy|系统规定参数，取值：**ModifySQLCollectorPolicy**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|SQLCollectorStatus|String|是|Enable|开启或关闭SQL审计，取值：**Enable | Disable**

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

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
	  <sQLCollectorStatus>Enable</sQLCollectorStatus></ModifySQLCollectorPolicyResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"C3565F9F-76E9-4F7E-A662-D1B2488EC2FC",
	"sQLCollectorStatus":"Enable"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

