# DescribeCrossRegionBackupDBInstance {#doc_api_Rds_DescribeCrossRegionBackupDBInstance .reference}

调用DescribeCrossRegionBackupDBInstance接口查询所选地域的哪些实例开启了跨地域备份，以及这些实例的跨地域备份设置。

仅适用于如下实例：

-   MySQL 5.7高可用本地SSD盘版
-   MySQL 5.6

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeCrossRegionBackupDBInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeCrossRegionBackupDBInstance|系统规定参数，取值：**DescribeCrossRegionBackupDBInstance**。

 |
|RegionId|String|是|cn-hangzhou|地域ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|PageNumber|Integer|否|1|页码，取值：大于0且不超过Integer的最大值。

 默认值：**1**。

 |
|PageSize|Integer|否|30|每页记录数，取值：

 -   **30**；
-   **50**；
-   **100**。

 默认值：30。

 |
|DBInstanceId|String|否|rm-uf6wjk5xxxxxxxxxx|实例ID。一次最多传入30个实例ID，以英文逗号（,）分隔。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RegionId|String|cn-hangzhou|地域ID。

 |
|TotalRecords|Integer|100|总记录数。

 |
|ItemsNumbers|Integer|1|跨地域备份设置列表内的Item数量。

 |
|PageNumber|Integer|1|页码，取值：大于0且不超过Integer的最大值。

 默认值：**1**。

 |
|PageSize|Integer|30|每页记录数，取值：

 -   **30**；
-   **50**；
-   **100**。

 默认值：30。

 |
|RequestId|String|33517002-182D-40BE-93EC-610BD3381045|请求ID。

 |
|Items| | |跨地域备份设置列表。

 |
|└BackupEnabled|String|Enable|跨地域备份总开关，取值：

 -   **Disable**：关闭；
-   **Enable**：开启。

 |
|└BackupEnabledTime|String|2019-06-12T05:44:21Z|跨地域数据备份开启时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|└CrossBackupRegion|String|cn-shanghai|跨地域备份目的地域ID。

 |
|└CrossBackupType|String|1|跨地域备份保存类型。默认值：**1**，表示每个备份都保存。

 |
|└DBInstanceDescription|String|测试数据库|实例名称，长度为2~256个字符。以中文、英文字母开头，可以包含数字、中文、英文、下划线（\_）、短横线（-）。

 **说明：** 不能以 http:// 和 https:// 开头。

 |
|└DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|└DBInstanceStatus|String|Running|实例状态，详情请参见[实例状态表](~~26315~~)。

 |
|└Engine|String|MySQL|数据库类型。

 |
|└EngineVersion|String|5.6|数据库版本。

 |
|└LockMode|String|Unlock|实例锁定状态，取值：

 -   **Unlock**：正常；
-   **ManualLock**：手动触发锁定；
-   **LockByExpiration**：实例过期自动锁定；
-   **LockByRestoration**：实例回滚前的自动锁定；
-   **LockByDiskQuota**：实例空间满自动锁定，不可访问实例。

 |
|└LogBackupEnabled|String|Enable|跨地域日志备份开关，取值：

 -   **Disable**：关闭；
-   **Enable**：开启。

 |
|└LogBackupEnabledTime|String|2019-06-12T05:44:21Z|跨地域日志备份开启时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|└RetentType|Integer|1|跨地域备份保留方式。当前仅支持按配置时长保留，默认值：**1**。

 |
|└Retention|Integer|15|跨地域备份保留天数，取值：**7~1825**。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeCrossRegionBackupDBInstance
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeCrossRegionBackupDBInstanceResponse>
  <Items>
    <Item>
      <LockMode>Unlock</LockMode>
      <CrossBackupType>1</CrossBackupType>
      <LogBackupEnabled>Enable</LogBackupEnabled>
      <BackupEnabledTime>2019-06-12T05:44:21Z</BackupEnabledTime>
      <BackupEnabled>Enable</BackupEnabled>
      <RetentType>1</RetentType>
      <DBInstanceId>rm-bpxxxxx</DBInstanceId>
      <Retention>15</Retention>
      <DBInstanceDescription>测试数据库</DBInstanceDescription>
      <Engine>MySQL</Engine>
      <LogBackupEnabledTime>2019-06-12T05:44:21Z</LogBackupEnabledTime>
      <CrossBackupRegion>cn-shanghai</CrossBackupRegion>
      <EngineVersion>5.6</EngineVersion>
      <DBInstanceStatus>Running</DBInstanceStatus>
    </Item>
  </Items>
  <PageNumber>1</PageNumber>
  <RegionId>cn-hangzhou</RegionId>
  <RequestId>33517002-182D-40BE-93EC-610BD3381045</RequestId>
  <ItemsNumbers>1</ItemsNumbers>
  <TotalRecords>1</TotalRecords>
</DescribeCrossRegionBackupDBInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"Item":[
			{
				"LockMode":"Unlock",
				"CrossBackupType":"1",
				"LogBackupEnabled":"Enable",
				"BackupEnabledTime":"2019-06-12T05:44:21Z",
				"BackupEnabled":"Enable",
				"RetentType":1,
				"DBInstanceId":"rm-bpxxxxx",
				"Retention":15,
				"DBInstanceDescription":"测试数据库",
				"Engine":"MySQL",
				"LogBackupEnabledTime":"2019-06-12T05:44:21Z",
				"CrossBackupRegion":"cn-shanghai",
				"EngineVersion":"5.6",
				"DBInstanceStatus":"Running"
			}
		]
	},
	"PageNumber":1,
	"RequestId":"33517002-182D-40BE-93EC-610BD3381045",
	"RegionId":"cn-hangzhou",
	"ItemsNumbers":1,
	"TotalRecords":1
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

