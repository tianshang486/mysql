# PurgeDBInstanceLog {#doc_api_1063624 .reference}

调用PurgeDBInstanceLog接口清理或收缩RDS实例日志。

-   对于RDS for MySQL实例，该接口可以将本地Binlog日志上传至OSS空间，然后清理本地Binlog日志，释放空间；
-   对于RDS for SQL Server实例，该接口可以产生一个临时备份，临时备份完成后将收缩事务日志，释放空间。

**说明：** 该接口适用于MySQL、SQL Server实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=PurgeDBInstanceLog)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|PurgeDBInstanceLog|系统规定参数，取值：**PurgeDBInstanceLog**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|待清理或收缩日志的实例ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=PurgeDBInstanceLog
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<PurgeDBInstanceLogResponse>
  <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
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

