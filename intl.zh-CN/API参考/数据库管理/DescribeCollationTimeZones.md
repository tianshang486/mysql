# DescribeCollationTimeZones {#doc_api_1064090 .reference}

调用DescribeCollationTimeZones接口查看支持的字符集排序规则和时区。

**说明：** 仅支持RDS for SQL Server 2012或以上版本实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeCollationTimeZones)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeCollationTimeZones|系统规定参数，取值：**DescribeCollationTimeZones**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|CollationTimeZones| | |支持的字符集排序规则和时区列表。

 |
|└Description|String|Kabul|描述。

 |
|└StandardTimeOffset|String|\(UTC+04:30\)|世界协调时间偏移。由世界协调时间UTC+时区差组成，格式：\(UTC+*HH:mm*\)。

 |
|└TimeZone|String|Afghanistan Standard Time|时区。

 |
|RequestId|String|4EAED246-DB18-4C8D-9EB5-C319626F2A77|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeCollationTimeZones
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeCollationTimeZonesResponse>
  <CollationTimeZones>
    <CollationTimeZone>
      <StandardTimeOffset>(UTC+04:30)</StandardTimeOffset>
      <Description>Kabul</Description>
      <TimeZone>Afghanistan Standard Time</TimeZone>
    </CollationTimeZone>
  </CollationTimeZones>
  <RequestId>4EAED246-DB18-4C8D-9EB5-C319626F2A77</RequestId>
</DescribeCollationTimeZonesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"CollationTimeZones":{
		"CollationTimeZone":[
			{
				"StandardTimeOffset":"(UTC+04:30)",
				"Description":"Kabul",
				"TimeZone":"Afghanistan Standard Time"
			}
		]
	},
	"RequestId":"4EAED246-DB18-4C8D-9EB5-C319626F2A77"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

