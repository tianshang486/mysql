# ModifyInstanceCrossBackupPolicy {#doc_api_Rds_ModifyInstanceCrossBackupPolicy .reference}

调用ModifyInstanceCrossBackupPolicy接口修改RDS跨地域备份设置。

**说明：** 仅适用于如下实例：

-   MySQL 5.7高可用本地SSD盘版
-   MySQL 5.6

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyInstanceCrossBackupPolicy)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyInstanceCrossBackupPolicy|系统规定参数，取值：**ModifyInstanceCrossBackupPolicy**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。一次最多传入30个实例ID，以英文逗号（,）分隔。

 |
|RegionId|String|是|cn-hangzhou|源实例地域ID，可以通过接口[DescribeRegions](~~26243~~)查看地域ID。

 |
|CrossBackupType|String|否|1|跨地域备份保存类型。默认值：**1**，表示每个备份都保存。

 |
|RetentType|Integer|否|1|跨地域备份保留方式。默认值：**1**，表示按时长保留。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|BackupEnabled|String|否|1|跨地域备份总开关（数据备份+日志备份），取值：

 -   **0**：关闭；
-   **1**：开启。

 |
|LogBackupEnabled|String|否|1|跨地域日志备份开关，取值：

 -   **0**：关闭；
-   **1**：开启。

 |
|CrossBackupRegion|String|否|cn-shanghai|跨地域备份的目的地域ID。

 |
|Retention|Integer|否|7|跨地域备份保留天数，取值：**7~1825**。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|BackupEnabled|String|1|跨地域备份总开关，取值：

 -   **0**：关闭；
-   **1**：开启。

 |
|CrossBackupRegion|String|cn-shanghai|跨地域备份的目的地域ID。

 |
|CrossBackupType|String|1|跨地域备份保存类型。默认值：**1**，表示每个备份都保存。

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|LogBackupEnabled|String|1|跨地域日志备份开关，取值：

 -   **0**：关闭；
-   **1**：开启。

 |
|RegionId|String|cn-hangzhou|源实例地域ID，可以通过接口[DescribeRegions](~~26243~~)查看地域ID。

 |
|RequestId|String|50A6059D-6DBB-46C6-A851-1EE93C9013CF|请求ID。

 |
|RetentType|Integer|1|跨地域备份保留方式。默认值：**1**，表示按时长保留。

 |
|Retention|Integer|15|跨地域备份保留天数，取值：**7~1825**。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyInstanceCrossBackupPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyInstanceCrossBackupPolicyResponse>
  <CrossBackupType>1</CrossBackupType>
  <LogBackupEnabled>Enable</LogBackupEnabled>
  <BackupEnabled>Enable</BackupEnabled>
  <CrossBackupRegion>cn-shanghai</CrossBackupRegion>
  <RetentType>1</RetentType>
  <RequestId>50A6059D-6DBB-46C6-A851-1EE93C9013CF</RequestId>
  <DBInstanceId>rm-bpxxxxx</DBInstanceId>
  <RegionId>cn-hangzhou</RegionId>
  <StorageType>oss</StorageType>
  <Endpoint/>
  <Retention>15</Retention>
</ModifyInstanceCrossBackupPolicyResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"LogBackupEnabled":"Enable",
	"CrossBackupType":"1",
	"BackupEnabled":"Enable",
	"RetentType":1,
	"CrossBackupRegion":"cn-shanghai",
	"RegionId":"cn-hangzhou",
	"DBInstanceId":"rm-bpxxxxx",
	"RequestId":"50A6059D-6DBB-46C6-A851-1EE93C9013CF",
	"Retention":15,
	"Endpoint":"",
	"StorageType":"oss"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

