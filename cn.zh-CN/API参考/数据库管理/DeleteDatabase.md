# DeleteDatabase {#doc_api_1061384 .reference}

调用DeleteDatabase接口删除实例下的某个数据库。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   实例类型为主实例；
-   数据库类型为：MySQL/SQL Server/MariaDB。

**说明：** 该接口不支持PostgreSQL、PPAS类型的实例，您需要通过SQL做DROP DATABASE操作。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DeleteDatabase)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteDatabase|系统规定参数，取值：**DeleteDatabase**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|DBName|String|是|testdb01|数据库名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|07F6177E-6DE4-408A-BB4F-0723301340F3|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DeleteDatabase
&DBInstanceId=rm-uf6wjk5xxxxxxx
&DBName=testdb01
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteDatabaseResponse>
  <RequestId>07F6177E-6DE4-408A-BB4F-0723301340F3</RequestId>
</DeleteDatabaseResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"07F6177E-6DE4-408A-BB4F-0723301340F3"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

