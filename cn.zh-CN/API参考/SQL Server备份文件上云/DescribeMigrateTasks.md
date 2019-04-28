# DescribeMigrateTasks {#doc_api_Rds_DescribeMigrateTasks .reference}

调用DescribeMigrateTasks接口查询备份数据上云任务列表。

该接口可以查询实例在最近一周内的备份数据上云任务记录。

**说明：** 

-   备份数据上云的源备份文件必须是全量备份（FULL）文件。
-   暂不支持SQL Server 2017集群版实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeMigrateTasks)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeMigrateTasks|系统规定参数，取值：**DescribeMigrateTasks**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|StartTime|String|是|2017-10-20T01:00Z|查询开始时间，格式：*yyyy-MM-dd*T*HH:mm:ss*Z。

 |
|EndTime|String|是|2017-10-25T01:00Z|查询结束时间，必须大于开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z。

 |
|PageSize|Integer|否|30|每页记录数，取值：

 -   **30**；
-   **50**；
-   **100**。

 默认值：**30**。

 |
|PageNumber|Integer|否|1|页码，取值：大于0且不超过Integer的最大值。

 默认值：**1**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|实例ID。

 |
|Items| | |备份数据上云任务信息列表。

 |
|└BackupMode|String|FULL|备份数据上云任务类型，取值：

 -   FULL：表示通过全量备份文件去执行还原操作。
-   UPDF：表示通过增量文件或者日志文件去还原增量部分的数据。

 |
|└CreateTime|String|2017-05-30T12:11:04Z|备份数据上云任务创建时间。

 |
|└DBName|String|testDB|数据库名称。

 |
|└Description|String|Api description|备份数据上云任务的描述信息。

 |
|└EndTime|String|2017-05-30T13:11:04Z|备份数据上云任务结束时间。

 |
|└IsDBReplaced|String|True|是否是覆盖性导入。

 |
|└MigrateTaskId|String|564522545|备份数据上云任务的ID。

 |
|└Status|String|Success|备份数据上云任务的状态，取值：

 -   **NoStart**：未开始；
-   **Running**：运行中；
-   **Success**：成功；
-   **Failed**：失败；
-   **Waiting**：等待 \(等待增量备份文件导入\)。

 |
|PageRecordCount|Integer|10|每页记录数。

 |
|PageNumber|Integer|1|获取第几页的数据。

 |
|RequestId|String|4E356DDF-6B83-45DB-99D5-4B1E8A0D286B|请求ID。

 |
|TotalRecordCount|Integer|30|满足条件的总的记录数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeMigrateTasks
&DBInstanceId=rm-uf6wjk5xxxxxxx
&StartTime=2017-10-20T01:00Z
&EndTime=2017-10-25T01:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeMigrateTasksResponse>
  <RequestId>A5409D02-D661-4BF3-8F3D-0A814D0574E7</RequestId>
  <PageRecordCount>1</PageRecordCount>
  <PageNumber>1</PageNumber>
  <TotalRecordCount>10</TotalRecordCount>
  <Items>
    <MigrateTaskId>rm-bp1842vxxxxx</MigrateTaskId>
    <DBName>test02</DBName>
    <CreateTime>2017-05-30 T12:11:4Z</CreateTime>
    <EndTime>2017-05-30 T12:11:4Z</EndTime>
    <IsDBReplaced>True</IsDBReplaced>
    <Status>Success</Status>
    <BackupMode>FULL</BackupMode>
    <Description>Api description</Description>
  </Items>
</DescribeMigrateTasksResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"Status":"Success",
		"MigrateTaskId":"rm-bp1842vxxxxx",
		"Description":"Api description",
		"IsDBReplaced":"True",
		"CreateTime":"2017-05-30 T12:11:4Z",
		"BackupMode":"FULL",
		"EndTime":"2017-05-30 T12:11:4Z",
		"DBName":"test02"
	},
	"TotalRecordCount":10,
	"PageNumber":1,
	"RequestId":"A5409D02-D661-4BF3-8F3D-0A814D0574E7",
	"PageRecordCount":1
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

