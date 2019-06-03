# ReleaseReadWriteSplittingConnection {#doc_api_Rds_ReleaseReadWriteSplittingConnection .reference}

调用ReleaseReadWriteSplittingConnection接口释放读写分离地址。

适用于已经开通读写分离的以下版本实例：

-   MySQL 5.7高可用版（本地SSD盘）
-   MySQL 5.6
-   SQL Server 2017集群版

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ReleaseReadWriteSplittingConnection)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ReleaseReadWriteSplittingConnection|系统规定参数，取值：**ReleaseReadWriteSplittingConnection**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|主实例ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|5A77D650-27A1-4E08-AD9E-59008EDB6927|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ReleaseReadWriteSplittingConnection
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ReleaseReadWriteSplittingConnectionResponse>
  <RequestID>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestID>
</ReleaseReadWriteSplittingConnectionResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestID":"5A77D650-27A1-4E08-AD9E-59008EDB6927"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

