# ModifyDBInstanceConnectionString {#doc_api_Rds_ModifyDBInstanceConnectionString .reference}

调用ModifyDBInstanceConnectionString接口修改实例的连接地址和端口。

目前RDS提供内外网两种连接地址，同时也支持混访模式下的专有网络和经典网络地址并存。

**说明：** 

-   仅支持修改连接地址的前缀；
-   不支持修改读写分离地址。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceConnectionString)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceConnectionString|系统规定参数，取值：**ModifyDBInstanceConnectionString**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|CurrentConnectionString|String|是|rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com|实例当前的某个连接地址，可以是内外网地址，或者混访模式下的经典网络地址。

 **说明：** 不支持修改读写分离地址。

 |
|ConnectionStringPrefix|String|是|m-xxxxbn5c23qo|目标连接地址的前缀，即只能修改**CurrentConnectionString**参数的前缀部分。

 **说明：** 长度5~40，不能包含汉字和非法字符（~!\#%^&\*=+\\|\{\};:'",<\>/?），建议由字母、数字、短横线（-）组成。

 |
|Port|String|是|3306|目标端口。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyDBInstanceConnectionString
&DBInstanceId=rm-uf6wjk5xxxxxxx
&CurrentConnectionString=rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com
&ConnectionStringPrefix=m-xxxxbn5c23qo
&Port=3306
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<PurgeDBInstanceLogResponse>
  <RequestId>65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</PurgeDBInstanceLogResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

