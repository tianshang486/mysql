# CreateOnlineDatabaseTask {#doc_api_Rds_CreateOnlineDatabaseTask .reference}

在备份数据上云时调用CreateOnlineDatabaseTask接口打开数据库。

本接口用于备份数据上云，建议您先查看或

[全量备份数据上云SQL Server 2012/2016/2017版本](~~68310~~)或[增量备份数据上云SQL Server 2012/2016/2017版本](~~71614~~)，了解流程后再使用本接口。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CreateOnlineDatabaseTask)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateOnlineDatabaseTask|系统规定参数，取值：**CreateOnlineDatabaseTask**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|DBName|String|是|testDB|数据库名称。

 |
|MigrateTaskId|String|是|5652255443|迁移任务ID。

 |
|CheckDBMode|String|是|AsyncExecuteDBCheck|打开数据库后的一致性检查方法，取值：

 -   **SyncExecuteDBCheck**：同步执行DB检查；
-   **AsyncExecuteDBCheck**：异步执行DB检查。

 **说明：** 兼容SQL Server 2008 R2版本。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1B2EBD14-36F6-4645-A3F9-DE19D321C18F|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CreateOnlineDatabaseTask
&DBInstanceId=rm-uf6wjk5xxxxxxx
&DBName=testDB
&MigrateTaskId=5652255443
&CheckDBMode=AsyncExecuteDBCheck
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateOnlineDatabaseTaskResponse>
  <code>200</code>
  <data>
    <RequestId>1B2EBD14-36F6-4645-A3F9-DE19D321C18F</RequestId>
  </data>
  <requestId>1B2EBD14-36F6-4645-A3F9-DE19D321C18F</requestId>
  <successResponse>true</successResponse>
</CreateOnlineDatabaseTaskResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"successResponse":true,
	"requestId":"1B2EBD14-36F6-4645-A3F9-DE19D321C18F",
	"data":{
		"RequestId":"1B2EBD14-36F6-4645-A3F9-DE19D321C18F"
	},
	"code":"200"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

