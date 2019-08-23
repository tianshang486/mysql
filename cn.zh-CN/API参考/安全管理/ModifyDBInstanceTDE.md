# ModifyDBInstanceTDE {#doc_api_Rds_ModifyDBInstanceTDE .reference}

调用ModifyDBInstanceTDE接口开启RDS实例透明数据加密功能。

透明数据加密TDE可对数据文件执行实时I/O加密和解密，数据在写入磁盘之前进行加密，从磁盘读入内存时进行解密。详情请参见[透明数据加密](~~33510~~)。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   已开通KMS。如果您未开通KMS，可在开通TDE过程中根据引导开通KMS；
-   实例类型为MySQL 5.6或SQL Server企业版实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceTDE&type=RPC&version=2014-08-15)

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

 **说明：** 仅SQL Server企业版实例可以传入此参数。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|EncryptionKey|String|否|749c1df7-xxxx-xxxx-xxxx-xxxxxxxxxxxx|自定义秘钥ID。

 **说明：** 仅MySQL实例可以传入此参数。

 |
|RoleArn|String|否|acs:ram::1406926xxxxx:role/aliyunrdsinstanceencryptiondefaultrole|角色的全局资源描述符，用来指定具体角色。详情请参见[RAM角色概览](~~93689~~)。

 **说明：** 仅MySQL实例可以传入此参数。

 |

## 返回数据 {#resultMapping .section}

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

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

