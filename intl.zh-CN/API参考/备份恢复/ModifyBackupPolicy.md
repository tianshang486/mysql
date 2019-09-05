# ModifyBackupPolicy {#doc_api_Rds_ModifyBackupPolicy .reference}

调用ModifyBackupPolicy接口修改备份设置。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例不能为只读实例；
-   实例状态为运行中。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=ModifyBackupPolicy&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyBackupPolicy|系统规定参数，取值：**ModifyBackupPolicy**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|BackupPolicyMode|String|否|DataBackupPolicy|备份类型：

 -   **DataBackupPolicy**：数据备份；
-   **LogBackupPolicy**：日志备份。

 |
|PreferredBackupTime|String|否|00:00Z-01:00Z|执行备份任务的时间。格式：*HH:mm*Z-*HH:mm*Z（UTC时间）。

 **说明：** **BackupPolicyMode**为**DataBackupPolicy**时，该参数必传。

 |
|PreferredBackupPeriod|String|否|Monday|备份周期，多个取值用英文逗号（,）隔开，默认为原值。取值：

 -   **Monday**：周一；
-   **Tuesday**：周二；
-   **Wednesday**：周三；
-   **Thursday**：周四；
-   **Friday**：周五；
-   **Saturday**：周六；
-   **Sunday**：周日。

 **说明：** **BackupPolicyMode**为**DataBackupPolicy**时，该参数必传。

 |
|BackupRetentionPeriod|String|否|7| 

 数据备份保留天数，取值：**7~730**。默认为原值。

 **说明：** **BackupPolicyMode**为**LogBackupPolicy**时，该参数必传。

 |
|BackupLog|String|否|Enable|是否开启日志备份。取值：**Enable | Disabled**。默认为原值。

 **说明：** **BackupPolicyMode**为**DataBackupPolicy**时，用于开启或关闭日志备份。

 |
|LogBackupRetentionPeriod|String|否|7|日志备份保留天数。取值：**7~730**，且不大于数据备份保留天数。

 **说明：** 当开启日志备份时，可设置日志备份文件的保留天数，目前仅支持MySQL、PostgreSQL、PPAS实例设置该值。

 |
|EnableBackupLog|String|否|True|是否开启日志备份。取值：**True | False**

 **说明：** **BackupPolicyMode**为**LogBackupPolicy**时，用于开启或关闭日志备份。

 |
|LocalLogRetentionHours|String|否|18|日志备份本地保留小时数。取值：**0~7\*24**，0表示不保留。默认为原值。

 **说明：** **BackupPolicyMode**为**LogBackupPolicy**时，该参数必传。

 |
|LocalLogRetentionSpace|String|否|30|本地日志最大循环空间使用率，超出后，则从最早的Binlog开始清理，直到空间使用率低于该比例。取值：**0~50**。默认为原值。

 **说明：** **BackupPolicyMode**为**LogBackupPolicy**时，该参数必传。

 |
|HighSpaceUsageProtection|String|否|Enable| 

 实例使用空间大于80%，或者剩余空间小于5GB时，是否无条件清理Binlog。取值：**Enable | Disable**。默认为原值。

 **说明：** **BackupPolicyMode**为**LogBackupPolicy**时，该参数必传。

 |
|Duplication|String|否|Disable|是否开启备份文件转储至OSS。取值：**Enable | Disable**。

 |
|DuplicationContent|String|否|DATA|转储数据备份或者日志备份：

 -   **DATA**：转储数据备份；
-   **LOG**：转储日志备份；
-   **DATA&LOG**：转储数据备份和日志备份。

 **说明：** **Duplication**=**Enable**时，该参数必填。

 |
|DuplicationLocation|String|否|\{"Storage":"OSS","Location": \{"Bucket": 'xxx', "Location":'cn-hangzhou',"OSSEndPoint":"oss-test","Object":"obje1"\}|用于让RAM授权RDS访问您的OSS。授权后日志文件才能转储至OSS。格式：

 \{"Storage":"OSS","Location": \{"Bucket": 'xxx', "Location":'cn-hangzhou',"OSSEndPoint":"oss-test","Object":"obje1"\}

 **说明：** 如果**Duplication**=**Enable**，该参数必填。

 |
|LogBackupFrequency|String|否|LogInterval|日志备份频率，取值：

 -   **LogInterval**：每30分钟备份一次。
-   默认与数据备份频率一致；

 **说明：** **LogInterval**参数仅适用于SQL Server。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|CompressType|String|否|4|备份压缩方式，支持库表恢复。取值：**4**。

 **说明：** 支持的实例版本为MySQL 5.7 高可用版（本地SSD盘）和MySQL 5.6高可用版。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|CompressType|String|4|备份压缩方式，取值：

 -   **0**：不压缩；
-   **1**：zlib压缩；
-   **2**：并行zlib压缩；
-   **4**：quicklz压缩，开启了库表恢复；
-   **8**：MySQL8.0 quicklz压缩但是还未支持库表恢复。

 |
|DBInstanceID|String|rm-uf6wjk5xxxxxxx|实例ID。

 |
|EnableBackupLog|String|False|是否开启了日志备份。

 |
|HighSpaceUsageProtection|String|Disable|实例使用空间大于80%，或者剩余空间小于5GB时，是否无条件清理Binlog。

 |
|LocalLogRetentionHours|Integer|18|日志备份本地保留小时数。

 |
|LocalLogRetentionSpace|String|30|本地日志最大循环空间使用率。

 |
|RequestId|String|DA147739-AEAD-4417-9089-65E9B1D8240D|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyBackupPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxx
&BackupPolicyMode=LogBackupPolicy
&EnableBackupLog=True
&HighSpaceUsageProtection=Enable
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyBackupPolicyResponse>
        <HighSpaceUsageProtection>Disable</HighSpaceUsageProtection>
	  <DBInstanceID>rm-bp1z3xxxxx</DBInstanceID>
	  <RequestId>E4BF5598-ED12-4406-AAA4-F375428BE741</RequestId>
	  <LocalLogRetentionHours>18</LocalLogRetentionHours>
	  <EnableBackupLog>1</EnableBackupLog>
	  <LocalLogRetentionSpace>30</LocalLogRetentionSpace>
</ModifyBackupPolicyResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"HighSpaceUsageProtection":"Disable",
	"DBInstanceID":"rm-bp1z3xxxxx",
	"RequestId":"E4BF5598-ED12-4406-AAA4-F375428BE741",
	"EnableBackupLog":"1",
	"LocalLogRetentionHours":"18",
	"LocalLogRetentionSpace":"30"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

