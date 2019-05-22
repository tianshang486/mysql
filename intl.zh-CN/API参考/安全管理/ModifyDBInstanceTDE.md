# ModifyDBInstanceTDE {#doc_api_Rds_ModifyDBInstanceTDE .reference}

调用ModifyDBInstanceTDE接口修改实例数据加密状态。

该接口用于为实例设置[透明数据加密](~~33510~~)（Transparent Data Encryption，TDE）。

-   加密密钥由密钥管理服务（KMS）产生和管理，RDS不提供加密所需的密钥和证书。开通TDE后，用户如果要恢复数据到本地，需要先通过RDS解密数据；
-   开通TDE前需要先开通KMS。如果您未开通KMS，可在开通TDE过程中根据引导开通KMS；
-   对于SQL Server 2008R2，TDE开通后无法从实例级别关闭，只支持数据库级别的开启和关闭；
-   对于MySQL 5.6，TDE开通后无法关闭；
-   TDE开通后会增加CPU使用率。

**说明：** 仅支持MySQL 5.6和SQL Server 2008 R2实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceTDE)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceTDE|系统规定参数，取值：**ModifyDBInstanceTDE**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|TDEStatus|String|是|Enabled|TDE状态，取值：**Enabled | Disabled**

 |
|DBName|String|否|testDB|想要开启TDE的数据库名称，可以一次输入多个，以英文逗号（,）分隔，最多传入50个。

 **说明：** 仅SQL Server 2008 R2实例需要传入此参数。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|777C4593-8053-427B-99E2-105593277CAB|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyDBInstanceTDE
&DBInstanceId=rm-uf6wjk5xxxxxxx
&TDEStatus=Enabled
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceTDEResponse>
  <requestId>777C4593-8053-427B-99E2-105593277CAB</requestId>
</ModifyDBInstanceTDEResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"777C4593-8053-427B-99E2-105593277CAB"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

