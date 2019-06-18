# DescribeCrossRegionLogBackupFiles {#doc_api_Rds_DescribeCrossRegionLogBackupFiles .reference}

调用DescribeCrossRegionLogBackupFiles接口查看跨地域日志备份文件列表。

查看数据备份文件请参见[DescribeCrossRegionBackups](~~121733~~)。

仅适用于如下实例：

-   MySQL 5.7高可用本地SSD盘版
-   MySQL 5.6

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeCrossRegionLogBackupFiles)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeCrossRegionLogBackupFiles|系统规定参数，取值：**DescribeCrossRegionLogBackupFiles**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|StartTime|String|是|2019-05-30T12:10Z|查询开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|EndTime|String|是|2019-06-15T12:10Z|查询结束时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|RegionId|String|是|cn-hangzhou|实例所在地域ID。可以通过接口[DescribeRegions](~~26243~~)查看地域ID。

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
|CrossBackupRegion|String|否|cn-shanghai|跨地域备份目的地域ID。可以通过接口[DescribeCrossRegionBackupDBInstance](~~121737~~)查看地域ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx|实例ID。

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
|RegionId|String|cn-hangzhou|实例所在地域ID。

 |
|RequestId|String|DAC241E8-28E6-49DA-BFB0-B2DD090885C1|请求ID。

 |
|Items| | |跨地域日志备份列表。

 |
|└CrossBackupRegion|String|cn-shanghai|跨地域备份目的地域ID。

 |
|└CrossDownloadLink|String|"http://rdsddrlog-zb.oss-cn-zhangjiakou.aliyuncs.com/xxxxx|跨地域日志备份外网下载链接。

 |
|└CrossIntranetDownloadLink|String|http://rdsddrlog-zb.oss-cn-zhangjiakou-internal.aliyuncs.com/xxxxx|跨地域日志备份内网下载链接。

 |
|└CrossLogBackupId|Integer|14567|跨地域日志备份文件ID。

 |
|└CrossLogBackupSize|Long|5312836|跨地域日志备份文件大小，单位：Byte。

 |
|└InstanceId|Integer|8161055|实例编号。

 |
|└LinkExpiredTime|String|2019-06-30T15:00:00Z|下载链接过期时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|└LogBeginTime|String|2019-05-30T12:10Z|跨地域日志备份文件记录的开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|└LogEndTime|String|2019-05-30T20:10Z|跨地域日志备份文件记录的结束时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|└LogFileName|String|cn-hangzhou\_rm-bpxxxxx\_7198739\_mysql-bin.000230|跨地域日志备份文件名称。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeCrossRegionLogBackupFiles
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&StartTime=2019-05-30T12:10Z
&EndTime=2019-06-15T12:10Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeCrossRegionLogBackupFilesResponse>
  <Items>
    <Item>
      <LinkExpiredTime>2019-06-02T07:36:18Z</LinkExpiredTime>
      <CrossBackupRegion>cn-zhangjiakou</CrossBackupRegion>
      <LogEndTime>2019-06-01T06:11:49Z</LogEndTime>
      <LogBeginTime>2019-06-01T00:11:44Z</LogBeginTime>
      <InstanceId>7198743</InstanceId>
      <CrossLogBackupSize>770014</CrossLogBackupSize>
      <CrossDownloadLink>http://rdsddrlog-zb.oss-cn-zhangjiakou.aliyuncs.com/xxxxxx</CrossDownloadLink>
      <CrossIntranetDownloadLink>http://rdsddrlog-zb.oss-cn-zhangjiakou-internal.aliyuncs.com/xxxxx</CrossIntranetDownloadLink>
    </Item>
  </Items>
  <PageNumber>1</PageNumber>
  <TotalRecordCount>52</TotalRecordCount>
  <DBInstanceId>rm-xxxxx</DBInstanceId>
  <RegionId>cn-hangzhou</RegionId>
  <RequestId>A9723BCE-F32F-4F05-9922-8371C0842FA7</RequestId>
  <EndTime>EndTime=2019-06-15T12:10Z</EndTime>
  <StartTime>2019-05-30T12:10Z</StartTime>
  <PageRecordCount>10</PageRecordCount>
</DescribeCrossRegionLogBackupFilesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"Item":[
			{
				"LinkExpiredTime":"2019-06-02T07:36:18Z",
				"CrossBackupRegion":"cn-zhangjiakou",
				"LogBeginTime":"2019-06-01T00:11:44Z",
				"LogEndTime":"2019-06-01T06:11:49Z",
				"InstanceId":7198743,
				"CrossLogBackupSize":770014,
				"CrossDownloadLink":"http://rdsddrlog-zb.oss-cn-zhangjiakou.aliyuncs.com/xxxxxx",
				"CrossIntranetDownloadLink":"http://rdsddrlog-zb.oss-cn-zhangjiakou-internal.aliyuncs.com/xxxxx"
			}
		]
	},
	"TotalRecordCount":52,
	"PageNumber":1,
	"RequestId":"A9723BCE-F32F-4F05-9922-8371C0842FA7",
	"RegionId":"cn-hangzhou",
	"DBInstanceId":"rm-xxxxx",
	"EndTime":"EndTime=2019-06-15T12:10Z",
	"StartTime":"2019-05-30T12:10Z",
	"PageRecordCount":10
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidStartTime.Format|Specified start time is not valid.|指定的起始时间无效。|
|400|InvalidEndTime.Format|Specified end time is not valid.|指定结束时间无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

