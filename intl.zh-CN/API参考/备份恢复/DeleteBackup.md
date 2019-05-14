# DeleteBackup {#doc_api_Rds_DeleteBackup .reference}

调用DeleteBackup接口删除数据备份文件。

调用该接口删除数据备份文件只删除实例自身的备份集，不会删除所关联实例（只读、灾备、克隆等）的备份集。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   实例为MySQL、PostgreSQL、PPAS的高可用版本；
-   如果日志备份已关闭，RDS实例不支持按时间点恢复功能。此时您可以删除已生成超过7天的任意数据备份文件；
-   如果日志备份已开启，且日志备份保留时间小于数据备份保留时间，则超过日志备份保留时间的数据备份文件可以删除。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DeleteBackup)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteBackup|系统规定参数，取值：**DeleteBackup**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|BackupId|String|是|324909958|备份集ID。可通过接口[DescribeBackups](~~26273~~)查询。多组值以英文逗号（,）隔开，单次最多传入100个。

 **说明：** 只支持删除[DescribeBackups](~~26273~~)中**StoreStatus**为**Enabled**的备份集。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|37441409-FFD1-40AA-8EC5-9ECF5E2F7C29|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DeleteBackup
&DBInstanceId=rm-uf6wjk5xxxxxxx
&BackupId=324909958
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteBackupResponse>
  <RequestId>37441409-FFD1-40AA-8EC5-9ECF5E2F7C29</RequestId>
</DeleteBackupResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"37441409-FFD1-40AA-8EC5-9ECF5E2F7C29"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

