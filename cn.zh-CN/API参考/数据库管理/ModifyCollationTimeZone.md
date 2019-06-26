# ModifyCollationTimeZone {#doc_api_1101360 .reference}

调用ModifyCollationTimeZone接口修改系统库的字符集排序规则和时区，已下线。

**说明：** 该API已下线。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyCollationTimeZone)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
| Action |String|是|ModifyCollationTimeZone| 系统规定参数，取值为 **ModifyCollationTimeZone** 。

 |
| DBInstanceId |String|是|rm-uf6wjk5xxxxxxx| 实例ID。

 |
| AccessKeyId |String|否|LTAIfCxxxxxxx| 阿里云颁发给用户的访问服务所用的密钥ID。

 |
| Collation |String|否|Latin1\_General\_CI\_AS| 系统字符集排序规则，取值：

 -    **Latin1\_General\_CI\_AS** 
-    **Latin1\_General\_CS\_AS** 
-    **SQL\_Latin1\_General\_CP1\_CI\_AS** 
-    **SQL\_Latin1\_General\_CP1\_CS\_AS** 
-    **Chinese\_PRC\_CS\_AS** 
-    **Chinese\_PRC\_BIN** 
-    **Chinese\_PRC\_CI\_AS** 
-    **Japanese\_CI\_AS** 
-    **Japanese\_CS\_AS** 
-    **Chinese\_Taiwan\_Stroke\_CI\_AS** 
-    **Chinese\_Taiwan\_Stroke\_CS\_AS** 

 默认为不修改。

 **说明：** **Collation** 与 **Timezone** 必须传入至少一个。

 |
| Timezone |String|否|China Standard Time| 系统时区，默认为不修改。

 **说明：** **Collation** 与 **Timezone** 必须传入至少一个。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Collation|String|Latin1\_General\_CI\_AS| 系统字符集排序规则。

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx| 实例ID。

 |
|RequestId|String|8EA054AF-DFA7-497D-9F57-790FFC974C0B| 请求ID。

 |
|TaskId|String|114413215| 任务ID。

 |
|Timezone|String|China Standard Time| 时区。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyCollationTimeZone
&DBInstanceId=rm-uf6wjk5xxxxxxx
%Timezone=China Standard Time
&<公共请求参数>

```

正常返回示例

 `XML` 格式

``` {#xml_return_success_demo}
<ModifyCollationTimeZoneResponse>
  <collation>Latin1_General_CI_AS</collation>
  <dBInstanceId>rm-bp1yx1dv50269syxa</dBInstanceId>
  <requestId>8EA054AF-DFA7-497D-9F57-790FFC974C0B</requestId>
  <taskId>114413215</taskId>
  <timezone>nochange</timezone>
</ModifyCollationTimeZoneResponse>

```

 `JSON` 格式

``` {#json_return_success_demo}
{
	"taskId":"114413215",
	"timezone":"nochange",
	"requestId":"8EA054AF-DFA7-497D-9F57-790FFC974C0B",
	"collation":"Latin1_General_CI_AS",
	"dBInstanceId":"rdsaiiabnaiiabn"
}
```

## 错误码 { .section}

 [查看本产品错误码](https://error-center.aliyun.com/status/product/Rds) 

