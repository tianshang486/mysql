# DescribeBackups {#doc_api_Rds_DescribeBackups .reference}

调用DescribeBackups接口查看备份集列表。

**说明：** 备份集的状态**BackupStatus**必须是**Success**，才能用于恢复。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DescribeBackups&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeBackups|系统规定参数，取值：**DescribeBackups**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|BackupId|String|否|327329803|备份集ID。

 |
|BackupStatus|String|否|Success|备份集状态。取值：

 -   **Success**：已完成备份；
-   **Failed**：备份失败。

 |
|BackupMode|String|否|Automated|备份模式，取值：

 -   **Automated**：系统自动备份；
-   **Manual**：手动备份。

 |
|StartTime|String|否|2011-06-01T16:00Z|查询开始时间。格式：*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|EndTime|String|否|2011-06-15T16:00Z|查询结束时间，需要大于查询开始时间。格式：*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

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

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|TotalRecordCount|String|100|总记录数。

 |
|PageNumber|String|1|页码。

 |
|PageRecordCount|String|30|本页备份集个数。

 |
|Items| | |备份集列表。

 |
|BackupId|String|321020562|备份集ID。

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|实例ID。

 |
|HostInstanceID|String|5882781|产生备份集的实例编号，用于区分该备份集产生于主实例或备实例。

 |
|BackupStatus|String|Success|备份集状态。

 |
|BackupStartTime|String|2019-02-03T12:20:00Z|本次备份开始时间。格式：*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|BackupEndTime|String|2019-02-13T12:20:00Z|本次备份结束时间。格式：*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|BackupType|String|FullBackup|备份类型，取值：

 -   **FullBackup**：全量备份；
-   **IncrementalBackup**：增量备份。

 |
|BackupMode|String|Automated|备份模式，取值：

 -   **Automated**：系统自动备份；
-   **Manual**：手动备份。

 |
|BackupMethod|String|Physical|备份方式，取值：

 -   **Logical**：逻辑备份；
-   **Physical**：物理备份。

 |
|BackupDownloadURL|String|http://rdsbak-hz-v3.oss-cn-hangzhou.aliyuncs.com/xxxxx|公网下载地址，若当前不可下载，则为空串。

 |
|BackupIntranetDownloadURL|String|http://rdsbak-hz-v3.oss-cn-hangzhou-internal.aliyuncs.com/xxxxx|内网下载地址，若当前不可下载，则为空串。

 |
|BackupSize|Long|2167808|备份文件大小，单位：Byte。

 |
|StoreStatus|String|Disabled|该数据备份是否可删除，取值：

 -   **Enabled**：可删除；
-   **Disabled**：不可删除。

 |
|MetaStatus|String|OK|库表恢复的备份集状态，取值：

 -   **OK**：正常；
-   **LARGE**：表数量过多，不能用于库表恢复；
-   **EMPTY**：备份失败的备份集。

 **说明：** 空串表示未开通库表恢复的备份集。

 |
|RequestId|String|1A6D328C-84B8-40DC-BF49-6C73984D7494|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeBackups
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeBackupsResponse>
	  <Items>
		    <Backup>
			      <StoreStatus>Disabled</StoreStatus>
			      <HostInstanceID>5882781</HostInstanceID>
			      <BackupLocation>OSS</BackupLocation>
			      <BackupIntranetDownloadURL>http://rdsbak-hz-v3.oss-cn-hangzhou-internal.aliyuncs.com/custins10430291/hins5882781_data_20190213201955.tar.gz?OSSAccessKeyId=xxxxxxxx&amp;Expires=1231230&amp;Signature=zIBwxxxxxxx5ga3p%2BVxxxxxxxx%3D</BackupIntranetDownloadURL>
			      <BackupType>FullBackup</BackupType>
			      <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
			      <BackupEndTime>2019-02-13T12:22:53Z</BackupEndTime>
			      <BackupMethod>Physical</BackupMethod>
			      <BackupId>321020562</BackupId>
			      <BackupStartTime>2019-02-13T12:20:37Z</BackupStartTime>
			      <BackupDownloadURL>http://rdsbak-hz-v3.oss-cn-hangzhou.aliyuncs.com/custins10430291/hins5882781_data_20190213201955.tar.gz?OSSAccessKeyId=xxxxxxx&amp;Expires=1231230&amp;Signature=zIBwxxxxxxxxUs5ga3p%2BVxxxxxxxk%3D</BackupDownloadURL>
			      <MetaStatus></MetaStatus>
			      <BackupDBNames>spdb,sys,test20181221,test-20181228,test_20181115,test_20181116</BackupDBNames>
			      <BackupMode>Automated</BackupMode>
			      <BackupSize>2167808</BackupSize>
			      <BackupStatus>Success</BackupStatus>
			      <BackupScale>DBInstance</BackupScale>
		    </Backup>
	  </Items>
	  <TotalBackupSize>8672256</TotalBackupSize>
	  <PageNumber>1</PageNumber>
	  <TotalRecordCount>1</TotalRecordCount>
	  <RequestId>B0E0F374-919F-4BD9-BCAC-AE68122A0D68</RequestId>
	  <PageRecordCount>1</PageRecordCount></DescribeBackupsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TotalBackupSize":"8672256",
	"Items":{
		"Backup":[
			{
				"StoreStatus":"Disabled",
				"HostInstanceID":5882781,
				"BackupLocation":"OSS",
				"BackupIntranetDownloadURL":"http://rdsbak-hz-v3.oss-cn-hangzhou-internal.aliyuncs.com/custins10430291/hins5882781_data_20190213201955.tar.gz?OSSAccessKeyId=xxxxxxxx&Expires=1231230&Signature=zIBwxxxxxxx5ga3p%2BVxxxxxxxx%3D",
				"BackupType":"FullBackup",
				"DBInstanceId":"rm-uf6wjk5xxxxxxx",
				"BackupEndTime":"2019-02-13T12:22:53Z",
				"BackupMethod":"Physical",
				"BackupId":321020562,
				"BackupStartTime":"2019-02-13T12:20:37Z",
				"BackupDownloadURL":"http://rdsbak-hz-v3.oss-cn-hangzhou.aliyuncs.com/custins10430291/hins5882781_data_20190213201955.tar.gz?OSSAccessKeyId=xxxxxxx&Expires=1231230&Signature=zIBwxxxxxxxxUs5ga3p%2BVxxxxxxxk%3D",
				"MetaStatus":"",
				"BackupDBNames":"spdb,sys,test20181221,test-20181228,test_20181115,test_20181116",
				"BackupMode":"Automated",
				"BackupStatus":"Success",
				"BackupSize":2167808,
				"BackupScale":"DBInstance"
			}
		]
	},
	"TotalRecordCount":1,
	"PageNumber":1,
	"RequestId":"B0E0F374-919F-4BD9-BCAC-AE68122A0D68",
	"PageRecordCount":1
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

