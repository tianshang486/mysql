# DescribeCrossRegionBackups {#doc_api_Rds_DescribeCrossRegionBackups .reference}

调用DescribeCrossRegionBackups接口查看某RDS实例跨地域数据备份文件列表。

查看日志备份文件请参见[DescribeCrossRegionLogBackupFiles](~~121734~~)。

仅适用于如下实例：

-   MySQL 5.7高可用本地SSD盘版
-   MySQL 5.6

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeCrossRegionBackups)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeCrossRegionBackups|系统规定参数，取值：**DescribeCrossRegionBackups**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|RegionId|String|是|cn-hangzhou|实例所在地域ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|CrossBackupId|Integer|否|14562|跨地域备份文件ID。

 **说明：** **CrossBackupId**和起止时间参数（**StartTime**、**EndTime**）必须传入其中一组。

 |
|StartTime|String|否|2019-05-30T12:10Z|查询开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|EndTime|String|否|2019-06-15T12:10Z|查询结束时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|PageNumber|Integer|否|1|页码，取值：大于0且不超过Integer的最大值。

 默认值：**1**。

 |
|CrossBackupRegion|String|否|cn-shanghai|跨地域备份目的地域ID。

 |
|PageSize|Integer|否|30|每页记录数，取值：

 -   **30**；
-   **50**；
-   **100**。

 默认值：30。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RegionId|String|cn-hangzhou|实例所在地域ID。

 |
|StartTime|String|2019-05-30T12:10Z|查询开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|EndTime|String|2019-06-15T12:10Z|查询结束时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|TotalRecordCount|Integer|100|总记录数。

 |
|PageNumber|Integer|1|页码，取值：大于0且不超过Integer的最大值。

 默认值：**1**。

 |
|PageRecordCount|Integer|30|本页备份文件个数。

 |
|RequestId|String|60912B41-7579-4B5D-B289-8856030F0A6A|请求ID。

 |
|Items| | |跨地域备份列表。

 |
|└BackupEndTime|String|2019-06-15T12:10Z|跨地域备份结束时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|└BackupMethod|String|P|跨地域备份方式，取值：

 -   **L**：逻辑备份；
-   **P**：物理备份。

 |
|└BackupSetScale|Integer|0|备份文件的备份策略，取值：

 -   **0**：实例备份；
-   **1**：单库备份。

 |
|└BackupSetStatus|Integer|0|备份文件状态，取值：

 -   **0**：完成备份；
-   **1**：备份失败。

 |
|└BackupStartTime|String|2019-05-30T12:10Z|跨地域备份开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|└BackupType|String|F|跨地域备份类型，取值：

 -   **F**：全量；
-   **I**：增量。

 |
|└Category|String|HighAvailability|实例系列，取值：

 -   **Basic**：基础版；
-   **HighAvailability**：高可用版；
-   **Finance**：金融版（仅中国站支持）。

 |
|└ConsistentTime|String|2019-06-12T05:44:46Z|备份文件里数据的时间点。

 |
|└CrossBackupDownloadLink|String|http://rdsddrbak-shanghai.oss-cn-shanghai.aliyuncs.com/xxxxx|跨地域备份文件外网下载链接。

 |
|└CrossBackupId|Integer|14377|跨地域备份文件ID。

 |
|└CrossBackupRegion|String|cn-shanghai|跨地域备份的目的地域ID。

 |
|└CrossBackupSetFile|String|cn-hangzhou\_rm-xxxxx\_hins81xxx\_data\_20190612134426\_qp.xb|跨地域备份文件压缩包名称。

 |
|└CrossBackupSetLocation|String|oss|备份文件存储位置。

 |
|└CrossBackupSetSize|Long|5312836|跨地域备份文件大小，单位：Byte。

 |
|└DBInstanceStorageType|String|ssd|存储类型。

 |
|└Engine|String|MySQL|数据库类型。

 |
|└EngineVersion|String|5.6|数据库版本。

 |
|└InstanceId|Integer|8161055|实例编号。用于区分该备份集产生于主实例或备实例。

 |
|└RestoreRegions| |"cn-hangzhou", "cn-shanghai"|备份文件可以进行恢复的地域列表，即备份文件可以恢复到哪些地域。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeCrossRegionBackups
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&CrossBackupId=14562
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeCrossRegionBackupsResponse>
  <Items>
    <Item>
      <CrossBackupSetFile>cn-hangzhou_rm-bpxxxxx_hins798xxxx_data_20190611125201.tar.gz</CrossBackupSetFile>
      <BackupSetScale>0</BackupSetScale>
      <BackupType>F</BackupType>
      <InstanceId>7980000</InstanceId>
      <CrossBackupId>14358</CrossBackupId>
      <BackupEndTime>2019-06-11T04:55:02Z</BackupEndTime>
      <BackupMethod>P</BackupMethod>
      <CrossBackupSetLocation>oss</CrossBackupSetLocation>
      <CrossBackupSetSize>2179643</CrossBackupSetSize>
      <Engine>mysql</Engine>
      <BackupStartTime>2019-06-11T04:52:46Z</BackupStartTime>
      <CrossBackupDownloadLink>http://rdsddrbak-zb.oss-cn-zhangjiakou.aliyuncs.com/cn-hangzhou_rm-bpxxxxx_hins7986073_data_20190611125201.tar.gz?OSSAccessKeyId=LTAxxxxx&amp;Expires=1560501641&amp;Signature=laK0kxxxxx%3D</CrossBackupDownloadLink>
      <Category>HighAvailability</Category>
      <CrossBackupRegion>cn-zhangjiakou</CrossBackupRegion>
      <RestoreRegions>
        <RestoreRegion>cn-hangzhou</RestoreRegion>
        <RestoreRegion>cn-zhangjiakou</RestoreRegion>
      </RestoreRegions>
      <EngineVersion>5.7</EngineVersion>
      <DBInstanceStorageType>ssd</DBInstanceStorageType>
    </Item>
  </Items>
  <TotalRecordCount>1</TotalRecordCount>
  <PageNumber>1</PageNumber>
  <RequestId>60912B41-7579-4B5D-B289-8856030F0A6A</RequestId>
  <RegionId>cn-hangzhou</RegionId>
  <EndTime>2019-06-11T08:00:00Z</EndTime>
  <StartTime>2019-06-10T00:00:00Z</StartTime>
  <PageRecordCount>30</PageRecordCount>
</DescribeCrossRegionBackupsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"Item":[
			{
				"CrossBackupSetFile":"cn-hangzhou_rm-bpxxxxx_hins798xxxx_data_20190611125201.tar.gz",
				"BackupSetScale":0,
				"BackupType":"F",
				"InstanceId":7980000,
				"CrossBackupId":14358,
				"BackupEndTime":"2019-06-11T04:55:02Z",
				"BackupMethod":"P",
				"CrossBackupSetLocation":"oss",
				"CrossBackupSetSize":2179643,
				"Engine":"mysql",
				"BackupStartTime":"2019-06-11T04:52:46Z",
				"CrossBackupDownloadLink":"http://rdsddrbak-zb.oss-cn-zhangjiakou.aliyuncs.com/cn-hangzhou_rm-bpxxxxx_hins7986073_data_20190611125201.tar.gz?OSSAccessKeyId=LTAxxxxx&Expires=1560501641&Signature=laK0kxxxxx%3D",
				"Category":"HighAvailability",
				"CrossBackupRegion":"cn-zhangjiakou",
				"RestoreRegions":{
					"RestoreRegion":[
						"cn-hangzhou",
						"cn-zhangjiakou"
					]
				},
				"EngineVersion":"5.7",
				"DBInstanceStorageType":"ssd"
			}
		]
	},
	"PageNumber":1,
	"TotalRecordCount":1,
	"RegionId":"cn-hangzhou",
	"RequestId":"60912B41-7579-4B5D-B289-8856030F0A6A",
	"EndTime":"2019-06-11T08:00:00Z",
	"StartTime":"2019-06-10T00:00:00Z",
	"PageRecordCount":30
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

