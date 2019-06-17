# DescribeInstanceCrossBackupPolicy {#doc_api_Rds_DescribeInstanceCrossBackupPolicy .reference}

调用DescribeInstanceCrossBackupPolicy接口查询跨地域备份设置。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeInstanceCrossBackupPolicy)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeInstanceCrossBackupPolicy|系统规定参数，取值：**DescribeInstanceCrossBackupPolicy**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|RegionId|String|是|cn-hangzhou|地域ID，可以通过接口[DescribeRegions](~~26243~~)查看地域ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|BackupEnabled|String|Enable|跨地域备份总开关，取值：

 -   **Disable**：关闭；
-   **Enable**：开启。

 |
|BackupEnabledTime|String|2019-06-12T05:44:21Z|跨地域备份开启时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|CrossBackupRegion|String|cn-shanghai|跨地域备份的目的地域ID。

 |
|CrossBackupType|String|1|跨地域备份保存类型。默认值：**1**，表示每个备份都保存。

 |
|DBInstanceDescription|String|测试数据库|实例名称，长度为2~256个字符。以中文、英文字母开头，可以包含数字、中文、英文、下划线（\_）、短横线（-）。

 **说明：** 不能以 http:// 和 https:// 开头。

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|DBInstanceStatus|String|Running|实例状态。详情请参见[实例状态表](~~26315~~)。

 |
|Engine|String|MySQL|数据库类型。

 |
|EngineVersion|String|5.6|数据库版本。

 |
|LockMode|String|Unlock|实例锁定状态，取值：

 -   **Unlock**：正常，没有锁定；
-   **ManualLock**：手动触发锁定；
-   **LockByExpiration**：实例过期自动锁定；
-   **LockByRestoration**：实例回滚前的自动锁定；
-   **LockByDiskQuota**：实例空间满自动锁定，不可访问实例。

 |
|LogBackupEnabled|String|Enable|跨地域日志备份开关，取值：

 -   **Disable**：关闭；
-   **Enable**：开启。

 |
|LogBackupEnabledTime|String|2019-06-12T05:44:21Z|跨地域日志备份开启时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|RegionId|String|cn-hangzhou|实例所在地域ID。

 |
|RequestId|String|CB7667B2-72C8-497B-9BD8-3B343CEF51AB|请求ID。

 |
|RetentType|Integer|1|跨地域备份保留方式。默认值：**1**，表示按时长保留。

 |
|Retention|Integer|15|跨地域备份保留天数，取值：**7~1825**。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeInstanceCrossBackupPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInstanceCrossBackupPolicyResponse>
  <DBInstanceStatusDesc>ACTIVATION</DBInstanceStatusDesc>
  <LockMode>Unlock</LockMode>
  <BackupEnabledTime>2019-06-12T05:44:21Z</BackupEnabledTime>
  <CrossBackupType>1</CrossBackupType>
  <LogBackupEnabled>Enable</LogBackupEnabled>
  <BackupEnabled>Enable</BackupEnabled>
  <RetentType>1</RetentType>
  <DBInstanceId>rm-bpxxxxx</DBInstanceId>
  <DBInstanceDescription/>
  <Retention>15</Retention>
  <Engine>mysql</Engine>
  <LogBackupEnabledTime>2019-06-12T05:44:21Z</LogBackupEnabledTime>
  <CrossBackupRegion>cn-shanghai</CrossBackupRegion>
  <StorageOwner>rds</StorageOwner>
  <RegionId>cn-hangzhou</RegionId>
  <RequestId>CB7667B2-72C8-497B-9BD8-3B343CEF51AB</RequestId>
  <EngineVersion>5.6</EngineVersion>
  <StorageType>oss</StorageType>
  <Endpoint/>
  <DBInstanceStatus>1</DBInstanceStatus>
</DescribeInstanceCrossBackupPolicyResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"DBInstanceStatusDesc":"ACTIVATION",
	"LockMode":"Unlock",
	"BackupEnabledTime":"2019-06-12T05:44:21Z",
	"CrossBackupType":"1",
	"LogBackupEnabled":"Enable",
	"BackupEnabled":"Enable",
	"RetentType":1,
	"DBInstanceId":"rm-bpxxxxx",
	"DBInstanceDescription":"",
	"Retention":15,
	"Engine":"mysql",
	"LogBackupEnabledTime":"2019-06-12T05:44:21Z",
	"CrossBackupRegion":"cn-shanghai",
	"StorageOwner":"rds",
	"RequestId":"CB7667B2-72C8-497B-9BD8-3B343CEF51AB",
	"RegionId":"cn-hangzhou",
	"Endpoint":"",
	"StorageType":"oss",
	"EngineVersion":"5.6",
	"DBInstanceStatus":"1"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

