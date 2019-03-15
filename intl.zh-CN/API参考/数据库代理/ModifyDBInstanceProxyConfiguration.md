# ModifyDBInstanceProxyConfiguration {#doc_api_1084579 .reference}

调用ModifyDBInstanceProxyConfiguration接口设置数据库代理，已下线。

**说明：** 该API已下线。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceProxyConfiguration)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceProxyConfiguration|系统规定参数，取值为：**ModifyDBInstanceProxyConfiguration**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|ProxyConfigurationKey|String|是|TransparentSwitch|数据库代理的**ProxyConfigurationKey**，取值：

 -   **TransparentSwitch**：透明切换；
-   **PersistentConnections**：短连接优化；
-   **AttacksProtection**：防暴力破解。

 |
|ProxyConfigurationValue|String|是|\{"status":"Enable"\}|数据库代理的**ProxyConfigurationValue**，取值：

 -   **TransparentSwitch**：透明切换，取值为：
    -   **Enable**：开启，默认值为Enable；
    -   **Disable**：关闭。如： \{"status":"Enable"\}。
-   **PersistentConnections**：短连接优化，取值为：
    -   **Enable**：开启；
    -   **Disable**：关闭，默认值为Disable。如： \{"status":"Disable"\}。
-   **AttacksProtection**：防暴力破解，取值为：
    -   **Enable**：开启；
    -   **Disable**：关闭，默认值为Disable。如：\{"status":"Disable"\}。

 返回值格式为JSON字符串，如：

 \{"status":"Disable", "check\_interval\_seconds": 60,

 "max\_failed\_login\_attempts": 60, "blocking\_seconds": 600\}

 参数说明及取值范围：

 -   对于每一个客户端，check\_interval\_seconds秒内最多允许max\_failed\_login\_attempts次错误密码登录，否则将对该客户端IP禁止登录blocking\_seconds秒钟。
-   取值范围：

 check\_interval\_seconds：**30~600**，单位为秒；

 max\_failed\_login\_attempts：**10~5000**，单位为次数；

 blocking\_seconds：**30~3600**，单位为秒。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|9705B5D2-C5B6-4526-B779-26D755EC1B8C|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?DBInstanceId=rm-uf6wjk5xxxxxxx
&ProxyConfigurationKey=TransparentSwitch
&ProxyConfigurationValue={"status":"Enable"}
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceProxyConfigurationResponse>
  <RequestId>9705B5D2-C5B6-4526-B779-26D755EC1B8C</RequestId>
</ModifyDBInstanceProxyConfigurationResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"9705B5D2-C5B6-4526-B779-26D755EC1B8C"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|EngineVersionNotSupported|EngineVersion specified cannot be replicate with the source DB Instance.|当前引擎版本不支持克隆实例|
|404|EngineNotSupported|Engine specified cannot be supported the operation.|引擎不支持|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

