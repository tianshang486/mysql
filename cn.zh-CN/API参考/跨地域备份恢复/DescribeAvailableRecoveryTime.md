# DescribeAvailableRecoveryTime {#doc_api_Rds_DescribeAvailableRecoveryTime .reference}

调用DescribeAvailableRecoveryTime接口查询所选备份文件可恢复的时间段。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeAvailableRecoveryTime)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAvailableRecoveryTime|系统规定参数，取值：**DescribeAvailableRecoveryTime**。

 |
|CrossBackupId|Integer|是|14377|跨地域备份文件ID。

 |
|RegionId|String|否|cn-hangzhou|地域ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|CrossBackupId|Integer|14377|跨地域备份文件ID。

 |
|RecoveryBeginTime|String|2019-06-12T05:22:29Z|跨地域备份文件可恢复的起始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|RecoveryEndTime|String|2019-06-12T07:33:12Z|跨地域备份文件可恢复的结束时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|RegionId|String|cn-hangzhou|源实例所在地域ID。

 |
|RequestId|String|8CCBF4BA-7CE1-47E1-B49F-E97EA200A40D|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeAvailableRecoveryTime
&CrossBackupId=14377
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAvailableRecoveryTimeResponse>
  <RecoveryEndTime>2019-06-12T07:33:12Z</RecoveryEndTime>
  <RecoveryBeginTime>2019-06-12T05:22:29Z</RecoveryBeginTime>
  <RequestId>8CCBF4BA-7CE1-47E1-B49F-E97EA200A40D</RequestId>
  <RegionId>cn-hangzhou</RegionId>
  <CrossBackupId>14377</CrossBackupId>
</DescribeAvailableRecoveryTimeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RecoveryEndTime":"2019-06-12T07:33:12Z",
	"RecoveryBeginTime":"2019-06-12T05:22:29Z",
	"CrossBackupId":14377,
	"RegionId":"cn-hangzhou",
	"RequestId":"8CCBF4BA-7CE1-47E1-B49F-E97EA200A40D"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidBackupSetID.NotFound|Specified backup set ID does not exist.|指定的备份集 ID 不存在。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

