# GrantAccountPrivilege {#doc_api_1064586 .reference}

调用GrantAccountPrivilege接口授权账号访问数据库。

一个账号可授权访问一个或多个数据库。调用该接口时，请确保实例状态为运行中，否则将操作失败。

**说明：** 该接口暂不支持SQL Server 2017集群版、PostgreSQL、PPAS实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=GrantAccountPrivilege)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GrantAccountPrivilege|系统规定参数，取值：**GrantAccountPrivilege**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|AccountName|String|是|test1|账号名称。

 |
|DBName|String|是|testDB|需要授权访问的数据库名称。

 |
|AccountPrivilege|String|是|ReadWrite|账号权限，取值：

 -   **ReadWrite**：读写；
-   **ReadOnly**：只读；
-   **DDLOnly**：仅执行DDL，适用于MySQL和MariaDB；
-   **DMLOnly**：只执行DML，适用于MySQL和MariaDB；
-   **DBOwner**：数据库所有者，适用于SQL Server。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|81BC9559-7B22-4B7F-B705-5F56DEECDEA7|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=GrantAccountPrivilege
&DBInstanceId=rm-uf6wjk5xxxxxxx
&AccountName=test1
&DBName=test
&AccountPrivilege=ReadWrite
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GrantAccountPrivilegeResponse>
  <RequestId>81BC9559-7B22-4B7F-B705-5F56DEECDEA7</RequestId>
</GrantAccountPrivilegeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"81BC9559-7B22-4B7F-B705-5F56DEECDEA7"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

