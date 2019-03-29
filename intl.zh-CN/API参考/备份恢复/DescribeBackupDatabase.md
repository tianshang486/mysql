# DescribeBackupDatabase {#doc_api_1085844 .reference}

调用DescribeBackupDatabase接口查询备份集下的数据库列表，已下线。

**说明：** 该API已下线。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeBackupDatabase)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeBackupDatabase|系统规定参数，取值：**DescribeBackupDatabase**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|BackupId|String|否|90262212|备份集ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DatabaseNames|String|db1,db2|数据库名，格式为"db1,db2"。

 |
|RequestId|String|08A3B71B-FE08-4B03-974F-CC7EA6DB1828|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeBackupDatabase
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeBackupDatabaseResponse>
  <DatabaseNames>db1,db2</DatabaseNames>
  <RequestId>08A3B71B-FE08-4B03-974F-CC7EA6DB1828</RequestId>
</DescribeBackupDatabaseResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"08A3B71B-FE08-4B03-974F-CC7EA6DB1828",
	"DatabaseNames":"db1,db2"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

