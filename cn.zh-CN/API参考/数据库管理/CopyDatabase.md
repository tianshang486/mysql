# CopyDatabase {#doc_api_Rds_CopyDatabase .reference}

调用CopyDatabase接口复制数据库SQL Server 2008 R2版，已下线。

**说明：** 该API已下线。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=CopyDatabase&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CopyDatabase|系统规定参数，取值：**CopyDatabase**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

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
	  <RequestID>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestID></CopyDatabaseResponse>
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
|400|InvalidDBName.Format|Specified DB name is not valid.|指定数据库名无效。|
|400|InvalidDBName.Forbid|Specified DB name is a keyword in RDS.|指定的数据库名是RDS保留字。|
|400|InvalidDBName.Duplicate|Specified DB name already exists in the This instance.|该实例已存在同名的数据库。|
|400|InvalidAccountName.Format|Specified account name is not valid.|指定的帐户名无效。|
|400|InvalidAccountName.Forbid|Specified account name is a keyword in RDS.|指定的帐户名是RDS中的关键字。|
|400|InvalidCharacterSetName.Format|Specified character set name is not valid.|指定的字符集名称无效。|
|400|InvalidAccountPrivilege.Malformed|Specified account privilege is not valid.|指定的帐户权限无效。|
|400|InvalidAccountPassword.Format|Specified account password is not valid.|指定的帐户密码无效。|
|400|InvalidDBDescription.Format|Specified DB description is not valid.|指定的DB描述无效。|
|403|DBLimitExceeded|DBQuotaExceeded: Exceeding the allowed amount of DB.|DB数量达到了上限。|

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

