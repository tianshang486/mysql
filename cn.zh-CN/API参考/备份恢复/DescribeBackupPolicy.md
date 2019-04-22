# DescribeBackupPolicy {#doc_api_Rds_DescribeBackupPolicy .reference}

调用DescribeBackupPolicy接口查看实例备份设置。

RDS实例将根据用户设置的备份设置，定期做备份。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeBackupPolicy)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeBackupPolicy|系统规定参数，取值：**DescribeBackupPolicy**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|BackupPolicyMode|String|否|DataBackupPolicy|备份类型，取值：

 -   **DataBackupPolicy**：数据备份；
-   **LogBackupPolicy**：日志备份。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|BackupRetentionPeriod|Integer|7|数据备份保留天数。

 |
|PreferredBackupTime|String|15:00Z-16:00Z|数据备份时间，格式：*HH:mm*Z-*HH:mm*Z。

 |
|PreferredBackupPeriod|String|Monday,Wednesday,Friday,Sunday|数据备份周期，多个取值用英文逗号（,）隔开，取值：

 -   **Monday**：周一；
-   **Tuesday**：周二；
-   **Wednesday**：周三；
-   **Thursday**：周四；
-   **Friday**：周五；
-   **Saturday**：周六；
-   **Sunday**：周日。

 |
|BackupLog|String|Enable|日志备份开关，取值：**Enable | Disabled**

 |
|LogBackupRetentionPeriod|Integer|7|日志备份保留天数。

 |
|Duplication|String|Enable|是否将备份文件转储至OSS，取值：**Enable | Disabled**

 |
|DuplicationContent|String|DATA&LOG|转储数据备份或者日志备份，取值：

 -   **DATA**：转储数据备份；
-   **LOG**：转储日志备份；
-   **DATA&LOG**：转储数据备份和日志备份。

 **说明：** 当**Duplication**=**Enable**时，本参数必填。

 |
|DuplicationLocation| | |备份文件的存储位置。

 |
|└Location| | |位置信息。

 |
|└Bucket|String|mybucket|转储的目标OSS Bucket的名称。

 |
|└Endpoint|String|oss-cn-shanghai.aliyuncs.com|转储目的域的名称。

 |
|└Sotrage|String|OSS|备份存储介质。

 |
|EnableBackupLog|String|True|是否开启日志备份，取值：

 -   **1**：表示开启；
-   **0**：表示关闭。

 |
|HighSpaceUsageProtection|String|Enable|实例使用空间大于80%，或者剩余空间小于5GB时，是否强制清理Binlog：

 -   **Disable**：不清理；
-   **Enable**：清理。

 |
|LocalLogRetentionHours|Integer|0|本地日志备份保留小时数。

 |
|LocalLogRetentionSpace|String|30|本地日志最大空间使用率。

 |
|LogBackupFrequency|String|LogInterval|日志备份频率，取值：

 -   **LogInterval**：每30分钟备份一次；
-   默认与数据备份周期**PreferredBackupPeriod**一致。

 **说明：** 参数**LogBackupFrequency**仅适用于SQL Server。

 |
|PreferredNextBackupTime|String|2018-01-19T15:15Z|下次备份时间。

 |
|RequestId|String|B87E2AB3-B7C9-4394-9160-7F639F732031|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeBackupPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeBackupPolicyResponse>
  <backupLog>Enable</backupLog>
  <backupRetentionPeriod>7</backupRetentionPeriod>
  <logBackupRetentionPeriod>7</logBackupRetentionPeriod>
  <preferredBackupPeriod>Monday,Wednesday,Friday,Sunday</preferredBackupPeriod>
  <preferredBackupTime>15:00Z-16:00Z</preferredBackupTime>
  <preferredNextBackupTime>2018-01-19T15:15Z</preferredNextBackupTime>
  <requestId>B87E2AB3-B7C9-4394-9160-7F639F732031</requestId>
</DescribeBackupPolicyResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"preferredBackupPeriod":"Monday,Wednesday,Friday,Sunday",
	"requestId":"B87E2AB3-B7C9-4394-9160-7F639F732031",
	"logBackupRetentionPeriod":7,
	"backupRetentionPeriod":7,
	"backupLog":"Enable",
	"preferredNextBackupTime":"2018-01-19T15:15Z",
	"preferredBackupTime":"15:00Z-16:00Z"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

