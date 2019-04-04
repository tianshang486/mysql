# DescribeBackupTasks {#doc_api_Rds_DescribeBackupTasks .reference}

调用DescribeBackupTasks接口查询实例的备份任务列表。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeBackupTasks)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeBackupTasks|系统规定参数，取值：**DescribeBackupTasks**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|BackupJobId|String|否|4762614|备份任务ID。

 |
|BackupMode|String|否|Automated|备份模式，取值：

 -   **Automated**：系统自动备份；
-   **Manual**：手动备份。

 |
|BackupJobStatus|String|否|0|备份任务状态，取值：

 -   **0**：未开始；
-   **1**：正在进行中。

 默认为所有状态。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Items| | |备份任务详情。

 |
|└BackupJobId|String|4762614|备份任务ID。

 |
|└BackupProgressStatus|String|NoStart|备份程序状态。

 |
|└BackupStatus|String|NoStart|备份任务状态，取值：

 -   **NoStart**：未开始；
-   **Preparing**：准备备份；
-   **Waiting**：等待备份；
-   **Uploading**：上传备份；
-   **Checking**：检查备份；
-   **Finished**：完成备份。

 |
|└JobMode|String|Automated|备份模式，取值：

 -   **Automated**：系统自动备份；
-   **Manual**：手动备份。

 |
|└TaskAction|String|NormalBackupTask|任务类型，取值：

 -   **TempBackupTask**：临时备份任务；
-   **NormalBackupTask**：普通备份任务。

 |
|RequestId|String|90496720-2319-42A8-87CD-FCE4DF95EBED|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeBackupTasks
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeBackupTasksResponse>
  <Items>
    <BackupJob>
      <JobMode>Automated</JobMode>
      <BackupProgressStatus>NoStart</BackupProgressStatus>
      <TaskAction>NormalBackupTask</TaskAction>
      <BackupStatus>NoStart</BackupStatus>
      <BackupJobId>4762614</BackupJobId>
    </BackupJob>
  </Items>
  <RequestId>90496720-2319-42A8-87CD-FCE4DF95EBED</RequestId>
</DescribeBackupTasksResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"BackupJob":[
			{
				"BackupProgressStatus":"NoStart",
				"JobMode":"Automated",
				"TaskAction":"NormalBackupTask",
				"BackupStatus":"NoStart",
				"BackupJobId":4762614
			}
		]
	},
	"RequestId":"90496720-2319-42A8-87CD-FCE4DF95EBED"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

