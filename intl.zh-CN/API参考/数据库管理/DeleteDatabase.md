# DeleteDatabase {#doc_api_Rds_DeleteDatabase .reference}

调用DeleteDatabase接口删除实例下的某个数据库。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   实例类型为主实例；
-   数据库类型为：MySQL/SQL Server/MariaDB。

**说明：** 该接口不支持PostgreSQL、PPAS类型的实例，您可以通过SQL做DROP DATABASE操作。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DeleteDatabase&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteDatabase| 系统规定参数，取值：**DeleteDatabase**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx| 实例ID。

 |
|DBName|String|是|testdb01| 数据库名称。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|07F6177E-6DE4-408A-BB4F-0723301340F3| 请求ID。

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
	  <RequestId>07F6177E-6DE4-408A-BB4F-0723301340F3</RequestId></DeleteDatabaseResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"07F6177E-6DE4-408A-BB4F-0723301340F3"
}
```

## 错误码 {#section_32e_1bh_mvc .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

