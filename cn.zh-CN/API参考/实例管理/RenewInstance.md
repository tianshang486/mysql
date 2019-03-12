# RenewInstance {#doc_api_1059321 .reference}

调用RenewInstance接口对RDS实例进行续费。

 **请确保在使用该接口前，已充分了解RDS产品的收费方式和[价格](https://www.alibabacloud.com/product/apsaradb-for-rds#pricing)。** 

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   该接口仅支持续费包年包月的RDS实例；
-   付款时，默认优先使用您账号下可用的优惠券；
-   您的账号必须支持账号余额支付或信用支付。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=RenewInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RenewInstance|系统规定参数。取值：**RenewInstance**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|需要续费的实例ID。

 |
|Period|String|是|12|预付费续费时长，单位：月。取值：

 -   **1-9**
-   **12**
-   **24**
-   **36**
-   **48**
-   **60**

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|AutoPay|String|否|True|是否自动付费。取值：

 -   **True**：自动付费。请确保账号有足够的余额。
-   **False**：控制台手动付费。具体操作为：登录控制台，在右上角选择**费用\>进入费用中心**，在**订单管理**找到目标订单进行支付。

 默认值：**False**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|Long|201815745430941|订单ID。

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=RenewInstance
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&Period=12
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RenewInstanceResponse>
  <OrderId>202867170710728</OrderId>
  <RequestId>E10319A3-B96A-46B0-81CE-D610DC891409</RequestId>
</RenewInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"E10319A3-B96A-46B0-81CE-D610DC891409",
	"OrderId":"202867170710728"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

