# ModifyDBInstanceMaintainTime {#doc_api_1013039 .reference}

修改RDS实例可维护时间。

该接口用于修改实例可例行维护的时间，一般设置为业务的低峰时间段。阿里云会在您设置的可维护时间段内进行实例维护，保证对业务的影响降到最低。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceMaintainTime)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceMaintainTime|系统规定参数，取值：**ModifyDBInstanceMaintainTime**。

 |
|DBInstanceId|String|是|rdsaiiabnaiiabn|实例ID。

 |
|MaintainTime|String|是|22:00Z-02:00Z :22点至凌晨2点|实例的维护时间，取值范围如下：

 -   22:00Z-02:00Z :22点至凌晨2点
-   02:00Z-06:00Z:凌晨2点至6点
-   06:00Z-10:00Z：6点至10点
-   10:00Z14:00Z：10点至14点
-   14:00Z-18:00Z：14点至18点
-   18:00Z-22:00Z：18点至22点

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII 字符，且该参数值中不能包含非 ASCII 字符。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?DBInstanceId=rdsaiiabnaiiabn
&MaintainTime=22:00Z-02:00Z :22点至凌晨2点
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceMaintainTimeResponse>
  <RequestId>65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</ModifyDBInstanceMaintainTimeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

