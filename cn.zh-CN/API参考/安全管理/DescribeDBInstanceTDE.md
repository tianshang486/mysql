# DescribeDBInstanceTDE {#doc_api_Rds_DescribeDBInstanceTDE .reference}

调用DescribeDBInstanceTDE接口查询实例数据加密状态。

该接口用于查看实例的[透明数据加密](~~33510~~)（Transparent Data Encryption，TDE）配置。

**说明：** 该接口只支持MySQL 5.6和SQL Server企业版实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceTDE)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstanceTDE|系统规定参数，取值：**DescribeDBInstanceTDE**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|TDEStatus|String|Enabled|实例级别的TDE状态，取值：**Enable | Disable**

 |
|Databases| | |数据库级别的TDE状态列表。

 **说明：** 对于SQL Server企业版实例，可以在实例级别的TDE开启时，控制数据库级别的TDE开启或关闭。

 |
|└DBName|String|test02|数据库名称。

 |
|└TDEStatus|String|Enabled|数据库级别的TDE状态，取值：**Enable | Disable**

 |
|RequestId|String|C816A4BF-A6EC-4722-95F9-2055859CCFD2|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDBInstanceTDE
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstanceTDEResponse>
  <TDEStatus>Enabled</TDEStatus>
  <Databases>
    <DBName>test02</DBName>
    <TDEStatus>Enabled</TDEStatus>
  </Databases>
  <requestId>C816A4BF-A6EC-4722-95F9-2055859CCFD2</requestId>
</DescribeDBInstanceTDEResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Databases":[
		{
			"TDEStatus":"Enabled",
			"DBName":"test02"
		}
	],
	"requestId":"C816A4BF-A6EC-4722-95F9-2055859CCFD2",
	"TDEStatus":"Enabled"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

