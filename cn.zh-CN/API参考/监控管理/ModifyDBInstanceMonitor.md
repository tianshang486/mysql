# ModifyDBInstanceMonitor {#doc_api_1086037 .reference}

调用ModifyDBInstanceMonitor修改监控频率。

 **请确保在使用该接口前，已充分了解RDS产品的收费方式和 [价格](https://www.aliyun.com/price/product#/rds/detail)。** 

阿里云对不同实例提供不同的监控频率，详情请参见 [设置监控频率](~~26200~~) 。

**说明：** 秒级监控需要收取额外费用。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceMonitor)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
| Action |String|是|ModifyDBInstanceMonitor| 系统规定参数，取值： **ModifyDBInstanceMonitor** 。

 |
| DBInstanceId |String|是|rm-uf6wjk5xxxxxxx| 实例ID。

 |
| Period |String|是|60| 监控的采集间隔，取值：

 -    **5** ；
-    **60** ；
-    **300** 。

 单位：秒。

 |
| AccessKeyId |String|否|LTAIfCxxxxxxx| 阿里云颁发给用户的访问服务所用的密钥ID。

 |
| ClientToken |String|否|ETnLKlblzczshOTUbOCzxxxxxxx| 用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|52B9805C-432C-4ED1-83FD-2F916B6D2733| 请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyDBInstanceMonitor
&DBInstanceId=rm-uf6wjk5xxxxxxx
&Period=60
&<公共请求参数>

```

正常返回示例

 `XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceMonitorResponse>
  <requestId>52B9805C-432C-4ED1-83FD-2F916B6D2733</requestId>
</ModifyDBInstanceMonitorResponse>

```

 `JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"52B9805C-432C-4ED1-83FD-2F916B6D2733"
}
```

## 错误码 { .section}

 [查看本产品错误码](https://error-center.aliyun.com/status/product/Rds) 

