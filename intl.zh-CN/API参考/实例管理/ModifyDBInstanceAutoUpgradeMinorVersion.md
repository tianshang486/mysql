# ModifyDBInstanceAutoUpgradeMinorVersion {#doc_api_Rds_ModifyDBInstanceAutoUpgradeMinorVersion .reference}

调用ModifyDBInstanceAutoUpgradeMinorVersion接口修改RDS实例升级小版本的方式。

支持的实例版本如下：

-   MySQL 8.0高可用版（本地SSD盘）
-   MySQL 8.0基础版
-   MySQL 5.7高可用版（本地SSD盘）
-   MySQL 5.7基础版
-   MySQL 5.6
-   MySQL 5.5

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceAutoUpgradeMinorVersion)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceAutoUpgradeMinorVersion|系统规定参数，取值：**ModifyDBInstanceAutoUpgradeMinorVersion**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxx|实例ID。

 |
|AutoUpgradeMinorVersion|String|是|Auto|实例升级小版本的方式，取值：

 -   **Auto**：自动升级小版本；
-   **Manual**：不自动升级，仅在当前版本下线时才强制升级。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|A31818D5-0550-4A81-8D13-B45948D7193F|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyDBInstanceAutoUpgradeMinorVersion
&DBInstanceId=rm-uf6wjk5xxx
&AutoUpgradeMinorVersion=Auto
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceAutoUpgradeMinorVersionResponse>
  <RequestId>A31818D5-0550-4A81-8D13-B45948D7193F</RequestId>
</ModifyDBInstanceAutoUpgradeMinorVersionResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"A31818D5-0550-4A81-8D13-B45948D7193F"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

