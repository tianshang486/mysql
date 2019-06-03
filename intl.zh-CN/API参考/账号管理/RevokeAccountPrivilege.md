# RevokeAccountPrivilege {#doc_api_Rds_RevokeAccountPrivilege .reference}

调用RevokeAccountPrivilege接口撤销账号对数据库的访问权限。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   数据库状态为运行中。

**说明：** 

-   具体撤销的权限包括SELECT、INSERT、UPDATE、DELETE、CREATE、DROP、REFERENCES、INDEX、ALTER、CREATE TEMPORARY TABLES、LOCK TABLES、EXECUTE、CREATE VIEW、SHOW VIEW、CREATE ROUTINE 、ALTER ROUTINE、EVENT、TRIGGER；
-   该接口暂不支持SQL Server 2017集群版、PostgreSQL、PPAS实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=RevokeAccountPrivilege)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RevokeAccountPrivilege|系统规定参数，取值：**RevokeAccountPrivilege**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccountName|String|是|test1|账号名称。

 |
|DBName|String|是|testDB|数据库名称，撤销账号对该数据库的所有权限。多个数据库用英文逗号（,）隔开。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|E22099CA-A61E-4992-A0B7-CE82DC175626|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=RevokeAccountPrivilege
&DBInstanceId=rm-uf6wjk5xxxxxxx
&AccountName=test1
&DBName=testDB
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RevokeAccountPrivilegeResponse>
  <RequestId>E22099CA-A61E-4992-A0B7-CE82DC175626</RequestId>
</RevokeAccountPrivilegeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"E22099CA-A61E-4992-A0B7-CE82DC175626"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

