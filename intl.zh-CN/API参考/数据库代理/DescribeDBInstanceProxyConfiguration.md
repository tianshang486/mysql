# DescribeDBInstanceProxyConfiguration {#doc_api_1084581 .reference}

调用DescribeDBInstanceProxyConfiguration接口查看数据库代理设置，已下线。

**说明：** 该API已下线。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceProxyConfiguration)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstanceProxyConfiguration|系统规定参数，取值为：**DescribeDBInstanceProxyConfiguration**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AttacksProtectionConfiguration|String|\{\\"check\_interval\_seconds\\":\\"0\\",\\"max\_failed\_login\_attempts\\":\\"0\\",\\"blocking\_seconds\\":\\"0\\",\\"status\\":\\"Disable\\"\}|是否开启防暴力破解：

 -   **Enable**：开启；
-   **Disable**：关闭。

 返回值格式为json字符串，如：

 \{"status":"Disable", "check\_interval\_seconds": 60,

 "max\_failed\_login\_attempts": 60, "blocking\_seconds": 600\}

 参数说明及取值范围：

 -   对于每一个客户端，check\_interval\_seconds秒内最多允许max\_failed\_login\_attempts次错误密码登录，否则将对该客户端IP禁止登录blocking\_seconds秒钟。
-   取值范围：
    -   check\_interval\_seconds：**30-600**，单位为秒；
    -   max\_failed\_login\_attempts：**10-5000**，单位为次数；
    -   blocking\_seconds：**30-3600**，单位为妙。

 |
|PersistentConnectionsConfiguration|String|\{\\"status\\":\\"Disable\\"\}|是否开启短连接优化：

 -   **Enable**：开启；
-   **Disable**：关闭。

 返回值格式为json字符串，如：

 \{"status":"Disable"\}。

 |
|TransparentSwitchConfiguration|String|\{\\"status\\":\\"Enable\\"\}|是否开启透明切换：

 -   **Enable**：开启；
-   **Disable**：关闭。

 返回值格式为json字符串，如：

 \{"status":"Enable"\}。

 |
|RequestId|String|E9DD55F4-1A5F-48CA-BA57-DFB3CA8C4C34|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstanceProxyConfigurationResponse>
  <PersistentConnectionsConfiguration>{"status":"Disable"}</PersistentConnectionsConfiguration>
  <TransparentSwitchConfiguration>{"status":"Enable"}</TransparentSwitchConfiguration>
  <AttacksProtectionConfiguration>{"check_interval_seconds":"0","max_failed_login_attempts":"0","blocking_seconds":"0","status":"Disable"}</AttacksProtectionConfiguration>
  <RequestId>E9DD55F4-1A5F-48CA-BA57-DFB3CA8C4C34</RequestId>
</DescribeDBInstanceProxyConfigurationResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TransparentSwitchConfiguration":"{\"status\":\"Enable\"}",
	"PersistentConnectionsConfiguration":"{\"status\":\"Disable\"}",
	"AttacksProtectionConfiguration":"{\"check_interval_seconds\":\"0\",\"max_failed_login_attempts\":\"0\",\"blocking_seconds\":\"0\",\"status\":\"Disable\"}",
	"RequestId":"E9DD55F4-1A5F-48CA-BA57-DFB3CA8C4C34"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

