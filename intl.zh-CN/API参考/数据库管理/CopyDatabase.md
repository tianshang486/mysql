# CopyDatabase {#doc_api_1084576 .reference}

调用CopyDatabase接口复制数据库SQL Server 2008 R2版，已下线。

**说明：** 该API已下线。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CopyDatabase)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CopyDatabase|系统规定参数，取值：**CopyDatabase**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBName|String|test02|数据库名称。

 |
|DBStatus|String|Creating|数据库状态，取值：

 -   **Creating**：创建中。
-   **Running**：使用中。
-   **Deleting**：删除中。

 |
|TaskId|String|25623542|任务ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CopyDatabase
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CopyDatabaseResponse>
  <RequestID>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestID>
</CopyDatabaseResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestID":"5A77D650-27A1-4E08-AD9E-59008EDB6927"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidDBName.Forbid|Specified DB name is a keyword in RDS.|指定的数据库名是RDS保留字。|
|400|InvalidAccountName.Format|Specified account name is not valid.|指定的帐户名无效。|
|400|InvalidAccountName.Forbid|Specified account name is a keyword in RDS.|指定的帐户名是RDS中的关键字。|
|400|InvalidCharacterSetName.Format|Specified character set name is not valid.|指定的字符集名称无效。|
|400|InvalidAccountPrivilege.Malformed|Specified account privilege is not valid.|指定的帐户权限无效。|
|400|InvalidAccountPassword.Format|Specified account password is not valid.|指定的帐户密码无效。|
|400|InvalidDBDescription.Format|Specified DB description is not valid.|指定的DB描述无效。|
|403|DBLimitExceeded|DBQuotaExceeded: Exceeding the allowed amount of DB.|DB数量达到了上限。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

