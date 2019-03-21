# DescribeOssDownloads {#doc_api_1105032 .reference}

调用DescribeOssDownloads接口查看备份数据上云任务的文件详情。

**说明：** 该接口暂不支持SQL Server 2017集群版实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeOssDownloads)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeOssDownloads|系统规定参数，取值：**DescribeOssDownloads**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|MigrateTaskId|String|是|5625458541|迁移任务的ID，可以通过[DescribeMigrateTasks](~~64563~~)接口查询。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|实例ID。

 |
|Items| | |导入的文件列表。

 |
|└BackupMode|String|FULL|备份类型，取值：

 -   **FULL**：表示全量备份文件；
-   **DIFF**：表示差异备份文件；
-   **LOG**：表示日志备份文件。

 |
|└CreateTime|String|2017-08-17T12:45:15Z|备份文件在下载列表中的创建时间。

 |
|└Description|String|App description|文件描述信息。

 |
|└EndTime|String|2017-08-27T12:45:15Z|结束时间。

 |
|└FileName|String|test|备份文件在OSS上的名称。

 |
|└FileSize|String|2|备份文件大小，单位MB。

 |
|└IsAvailable|String|True|是否可用，取值：**True | False**

 |
|└Status|String|Finished|文件状态，取值：

 -   **NoStart**：未开始；
-   **Downloading**：下载中；
-   **Finished**：下载完成；
-   **DownloadFailed**：下载失败；
-   **VerifyFailed**：MD5校验失败；
-   **Deleted**：已删除；
-   **DeleteFailed**：删除失败；
-   **CheckSuccess**：检查成功；
-   **CheckFailed**：检查失败；
-   **Restoring**：还原中；
-   **Restored**：还原成功；
-   **RestoreFailed**：还原失败。

 |
|MigrateTaskId|String|562154852|迁移任务的ID。

 |
|RequestId|String|A5409D02-D661-4BF3-8F3D-0A814D0574E7|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeOssDownloads
&DBInstanceId=rm-uf6wjk5xxxxxxx
&MigrateTaskId=5625458541
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeOssDownloadsResponse>
  <RequestId>A5409D02-D661-4BF3-8F3D-0A814D0574E7</RequestId>
  <DBInstanceId>rdsaiiabnaiiabn</DBInstanceId>
  <MigrateTaskId>rdsaiiabnaiiabn</MigrateTaskId>
  <Items>
    <FileName>rdsaiiabnaiiabn</FileName>
    <CreateTime>2017-05-30 T12:11:4Z</CreateTime>
    <FileSize>2MB</FileSize>
    <IsAvailable>True</IsAvailable>
    <Status>Finished</Status>
    <BackupMode>FULL</BackupMode>
    <Description>Api description</Description>
  </Items>
</DescribeOssDownloadsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"FileSize":"2MB",
		"Status":"Finished",
		"IsAvailable":"True",
		"Description":"Api description",
		"FileName":"rdsaiiabnaiiabn",
		"CreateTime":"2017-05-30 T12:11:4Z",
		"BackupMode":"FULL"
	},
	"MigrateTaskId":"rdsaiiabnaiiabn",
	"DBInstanceId":"rdsaiiabnaiiabn",
	"RequestId":"A5409D02-D661-4BF3-8F3D-0A814D0574E7"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

