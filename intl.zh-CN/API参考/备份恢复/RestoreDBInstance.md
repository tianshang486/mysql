# RestoreDBInstance {#doc_api_Rds_RestoreDBInstance .reference}

调用RestoreDBInstance接口恢复备份集到原实例（覆盖性恢复），已下线。

**说明：** 该API已下线。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=RestoreDBInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RestoreDBInstance|系统规定参数，取值：**RestoreDBInstance**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxx|实例ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|BackupId|String|否|327329803|备份集ID。可以通过接口[DescribeBackups](~~26273~~)查询备份集ID。

 **说明：** **BackupId**和**RestoreTime**必须传入一个。

 |
|RestoreTime|String|否|2011-06-11T16:00:00Z|用户指定备份保留周期内的任意时间点。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 **说明：** **BackupId**和**RestoreTime**必须传入一个。

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

http(s)://rds.aliyuncs.com/?Action=RestoreDBInstance
&DBInstanceId=rm-uf6wjk5xxxxx
&BackupId=327329803
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RestoreDBInstanceResponse>
  <RequestId>37441409-FFD1-40AA-8EC5-9ECF5E2F7C29</RequestId>
</RestoreDBInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"37441409-FFD1-40AA-8EC5-9ECF5E2F7C29"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

