# DescribeParameterTemplates {#doc_api_Rds_DescribeParameterTemplates .reference}

调用DescribeParameterTemplates接口查看数据库参数模板。

该接口适用的实例版本如下：

-   MySQL 5.5/5.6/5.7/8.0
-   SQL Server 2008 R2
-   PostgreSQL 9.4/10.0
-   PPAS 9.3/10.0
-   MariaDB 10.3

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeParameterTemplates)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeParameterTemplates|系统规定参数，取值：**DescribeParameterTemplates**。

 |
|Engine|String|是|MySQL|数据库类型，取值：

 -   **mysql**：MySQL数据库；
-   **mssql**：SQL Server数据库；
-   **PostgreSQL**：PostgreSQL数据库；
-   **PPAS**：PPAS数据库；
-   **MariaDB**：MariaDB数据库。

 |
|EngineVersion|String|是|5.6|数据库版本号，取值：

 -   MySQL数据库：**5.5/5.6/5.7/8.0**；
-   SQL Server数据库：**2008r2**；
-   PostgreSQL数据库：**9.4/10.0**；
-   PPAS数据库：**9.3/10.0**；
-   MariaDB数据库：**10.3**。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|Category|String|否|Basic|实例类别，取值：

 -   **Basic**：基础版；
-   **HighAvailability**：高可用版；
-   **Finance**：金融版（仅支持中国站）。

 默认返回所有实例类型的参数模板。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Engine|String|MySQL|数据库类型。

 |
|EngineVersion|String|5.5|数据库版本号。

 |
|ParameterCount|String|56|参数个数。

 |
|Parameters| | |参数列表。

 |
|ParameterName|String|auto\_increment\_increment|参数名。

 |
|ParameterValue|String|1|参数默认值。

 |
|ForceModify|String|true|参数是否可修改，取值：**true | false**

 |
|ForceRestart|String|false|是否重启才生效，取值：**true | false**

 |
|CheckingCode|String|\[10-3000\]|参数取值范围。

 |
|ParameterDescription|String|determines the starting point for the AUTO\_INCREMENT column value.|参数描述。

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeParameterTemplates
&Engine=MySQL
&EngineVersion=5.6
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeParameterTemplatesResponse>
  <Engine>mssql</Engine>
  <EngineVersion>2008r2</EngineVersion>
  <ParameterCount>1</ParameterCount>
  <Parameters>
    <TemplateRecord>
      <CheckingCode>[0-100]</CheckingCode>
      <ForceRestart>True</ForceRestart>
      <Factor>1</Factor>
      <ParameterDescription>此选项设置服务器范围内的默认填充因子值。提供填充因子是为了优化索引数据存储和性能。</ParameterDescription>
      <ParameterName>fill factor</ParameterName>
      <ParameterValue>0</ParameterValue>
      <ForceModify>True</ForceModify>
      <Unit>INT</Unit>
    </TemplateRecord>
  </Parameters>
  <RequestId>7B96585A-0FF2-4979-8FE5-7D147A29FDC0</RequestId>
</DescribeParameterTemplatesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"DescribeParameterTemplatesResponse":{
		"Parameters":{
			"TemplateRecord":{
				"ForceModify":"True",
				"ParameterDescription":"此选项设置服务器范围内的默认填充因子值。提供填充因子是为了优化索引数据存储和性能。",
				"Factor":"1",
				"ParameterValue":"0",
				"ForceRestart":"True",
				"CheckingCode":"[0-100]",
				"ParameterName":"fill factor",
				"Unit":"INT"
			}
		},
		"RequestId":"7B96585A-0FF2-4979-8FE5-7D147A29FDC0",
		"ParameterCount":"1",
		"EngineVersion":"2008r2",
		"Engine":"mssql"
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

