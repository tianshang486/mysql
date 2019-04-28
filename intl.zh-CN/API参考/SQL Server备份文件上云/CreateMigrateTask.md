# CreateMigrateTask {#doc_api_Rds_CreateMigrateTask .reference}

调用CreateMigrateTask接口将OSS上的备份文件还原到RDS实例，实现数据上云。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CreateMigrateTask)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateMigrateTask|系统规定参数，取值：**CreateMigrateTask**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|DBName|String|是|testDB|目标数据库名称。

 |
|BackupMode|String|是|FULL|迁移上云任务类型，取值：

 -   **FULL**：通过全量备份文件执去执行还原操作。
-   **UPDF**：通过增量文件或者日志文件去还原增量部分的数据。

 |
|IsOnlineDB|String|是|True|是否将还原后的数据库带上线，便于用户访问，取值：

 -   **True**：将数据库带上线。
-   **False**：不将数据库带上线。

 **说明：** 目前SQL Server 2008 R2 版本该值恒定为**True**。

 |
|CheckDBMode|String|否|AsyncExecuteDBCheck|打开数据库后一致性检查方法，取值：

 -   **SyncExecuteDBCheck**：同步执行DB检查；
-   **AsyncExecuteDBCheck**：异步执行DB检查。

 默认值为**AsyncExecuteDBCheck**（兼容 SQL Server 2008 R2）。

 **说明：** 当 **IsOnlineDB**=**True**时，该值有效。

 |
|OssObjectPositions|String|否|oss-ap-southeast-1.aliyuncs.com:rdsmssqlsingapore:autotest\_2008R2\_TestMigration\_FULL.bak|OSS的组成部分。

 取值由3段组成，用英文冒号（:）分隔：

 -   OSS Endpoint地址：oss-ap-southeast-1.aliyuncs.com；
-   OSS Bucket名字：rdsmssqlsingapore；
-   OSS上的备份文件Key：autotest\_2008R2\_TestMigration\_FULL.bak。

 **说明：** 

 -   该参数对于 SQL Server 2008 R2 版本实例是可选参数。
-   该参数对于 SQL Server 2008 R2 以上版本实例是必传参数。

 |
|OSSUrls|String|否|check\_cdn\_oss.sh www.xxxxxx.mobi|备份文件所在OSS共享URL地址（Encode编码后的URL）。

 有多个地址时，先使用“|”隔开，再编码后传入参数。

 **说明：** SQL Server 2008 R2 必须传入该参数。

 |
|MigrateTaskId|String|否|无|迁移任务ID：

 -   **BackupMode**=**FULL**时，该值为空。（兼容RDS for SQLServer 2008 R2）；
-   **BackupMode**=**UPDF**时，该值为对应FULL任务的ID。

 默认值为FULL。

 **说明：** 

 -   **IsOnlineDB**=**True**时，**BackupMode**必须取值为**FULL**；
-   **IsOnlineDB**=**False**时，**BackupMode**必须为**UPDF**。

 |
|AccessKeyId|String|否|LTAIKw8gxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|BackupMode|String|FULL|迁移上云任务类型，取值为：

 -   **FULL**：示通过全量备份文件执去执行还原操作；
-   **UPDF**：表示通过增量文件或者日志文件去还原增量部分的数据。

 |
|DBInstanceId|String|rm-uf6wjk5xxxxx|实例ID。

 |
|DBName|String|test02|数据库名称。

 |
|MigrateTaskId|String|564563256|迁移任务ID。

 |
|RequestId|String|866F5EB8-4650-4061-87F0-379F6F968BCE|请求ID。

 |
|TaskId|String|5451225|任务ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CreateMigrateTask
&DBInstanceId=rm-uf6wjk5xxxxxxx
&DBName=testDB
&BackupMode=FULL
&IsOnlineDB=True
&OssObjectPositions=oss-ap-southeast-1.aliyuncs.com:rdsmssqlsingapore:autotest_2008R2_TestMigration_FULL.bak
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateMigrateTaskResponse>
  <MigrateTaskId>135847</MigrateTaskId>
  <DBInstanceId>rm-bp178grbxxxxxxx</DBInstanceId>
  <RequestId>5F2B3757-BD56-40B3-B5F2-FCDD9FA0E2E2</RequestId>
  <BackupMode>UPDF</BackupMode>
  <TaskId>128301751</TaskId>
  <DBName>test02</DBName>
</CreateMigrateTaskResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"MigrateTaskId":"135847",
	"RequestId":"5F2B3757-BD56-40B3-B5F2-FCDD9FA0E2E2",
	"DBInstanceId":"rm-bp178grbxxxxxxx",
	"BackupMode":"UPDF",
	"TaskId":"128301751",
	"DBName":"test02"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidDBName|The instance does not have the specified DB name.|指定数据库名不存在。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

