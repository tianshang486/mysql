# DescribeParameters {#doc_api_Rds_DescribeParameters .reference}

调用DescribeParameters接口查询实例当前的参数配置。

该接口适用的实例版本如下：

-   MySQL 5.5/5.6/5.7/8.0
-   SQL Server 2008 R2
-   PostgreSQL 9.4/10.0
-   PPAS 9.3/10.0
-   MariaDB 10.3

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeParameters)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeParameters|系统规定参数，取值：**DescribeParameters**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Engine|String|MySQL|数据库类型。

 |
|EngineVersion|String|5.5|数据库版本号。

 |
|RunningParameters| | |当前运行的参数列表。

 |
|└ParameterName|String|fill factor|参数名称。

 |
|└ParameterValue|String|0|参数值。

 |
|└ParameterDescription|String|此选项设置服务器范围内的默认填充因子值。提供填充因子是为了优化索引数据存储和性能。|参数描述。

 |
|ConfigParameters| | |正在同步的参数列表。修改并提交参数后，需要等待实例同步参数，同步结束后从此列表删除。

 |
|└ParameterName|String|fill factor|参数名称。

 |
|└ParameterValue|String|50|参数值。

 |
|└ParameterDescription|String|此选项设置服务器范围内的默认填充因子值。提供填充因子是为了优化索引数据存储和性能。|参数描述。

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeParameters
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeParametersResponse>
  <ConfigParameters>
    <DBInstanceParameter>
      <ParameterDescription>此选项设置服务器范围内的默认填充因子值。提供填充因子是为了优化索引数据存储和性能。</ParameterDescription>
      <ParameterName>fill factor</ParameterName>
      <ParameterValue>50</ParameterValue>
    </DBInstanceParameter>
  </ConfigParameters>
  <Engine>mssql</Engine>
  <EngineVersion>2008r2</EngineVersion>
  <RunningParameters>
    <DBInstanceParameter>
      <ParameterDescription>此选项设置服务器范围内的默认填充因子值。提供填充因子是为了优化索引数据存储和性能。</ParameterDescription>
      <ParameterName>fill factor</ParameterName>
      <ParameterValue>0</ParameterValue>
    </DBInstanceParameter>
  </RunningParameters>
  <RequestId>2A748162-8040-4D6B-813E-6910C8C033F1</RequestId>
</DescribeParametersResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"ConfigParameters":{
		"DBInstanceParameter":[
			{
				"ParameterDescription":"此选项设置服务器范围内的默认填充因子值。提供填充因子是为了优化索引数据存储和性能。",
				"ParameterValue":"50",
				"ParameterName":"fill factor"
			}
		]
	},
	"RequestId":"2A748162-8040-4D6B-813E-6910C8C033F1",
	"RunningParameters":{
		"DBInstanceParameter":[
			{
				"ParameterDescription":"此选项设置服务器范围内的默认填充因子值。提供填充因子是为了优化索引数据存储和性能。",
				"ParameterValue":"0",
				"ParameterName":"fill factor"
			}
		]
	},
	"EngineVersion":"2008r2",
	"Engine":"mssql"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

