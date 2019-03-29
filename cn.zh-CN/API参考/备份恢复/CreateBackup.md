# CreateBackup {#doc_api_1084693 .reference}

调用CreateBackup接口为实例创建一个备份集。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   没有正在执行中的备份任务；
-   单个实例一天内可创建的备份集数量不超过20个。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CreateBackup)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateBackup|系统规定参数，取值：**CreateBackup**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|BackupMethod|String|否|Physical|备份类型，取值：

 -   **Logical**：逻辑备份；
-   **Physical**：物理备份或快照备份。

 默认值：**Physical**。

 **说明：** 

-   MySQL支持物理备份和逻辑备份，MariaDB支持快照备份，其他引擎支持物理备份；
-   实例必须存在数据库才能进行逻辑备份。

 |
|BackupStrategy|String|否|db|备份策略，取值：

 -   **db**：单库备份；
-   **instance**：实例备份。

 **说明：** MySQL进行逻辑备份或SQL Server进行全量物理备份时可传入该参数。

 |
|DBName|String|否|rds\_mysql|数据库列表，多个数据库之间用英文逗号（,）隔开。

 **说明：** MySQL进行单库逻辑备份或SQL Server进行单库全量物理备份时可传入该参数。

 |
|BackupType|String|否|Auto|备份方式，取值：

 -   **Auto**：自动选择全量备份或增量备份；
-   **FullBackup**：全量备份。

 默认值：**Auto**。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|BackupJobId|String|5073731|备份任务ID。

 |
|RequestId|String|2C125605-266F-41CA-8AC5-3A643D4F42C5|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CreateBackup
DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateBackupResponse>
  <RequestId>2C125605-266F-41CA-8AC5-3A643D4F42C5</RequestId>
  <BackupJobId>5073731</BackupJobId>
</CreateBackupResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"2C125605-266F-41CA-8AC5-3A643D4F42C5",
	"BackupJobId":"5073731"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

