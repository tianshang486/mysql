# CheckCreateDdrDBInstance {#doc_api_Rds_CheckCreateDdrDBInstance .reference}

调用CheckCreateDdrDBInstance接口预检查备份集是否支持跨地域恢复。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CheckCreateDdrDBInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CheckCreateDdrDBInstance|系统规定参数，取值：**CheckCreateDdrDBInstance**。

 |
|RegionId|String|是|cn-hangzhou|目的实例地域ID，可以通过接口[DescribeRegions](~~26243~~)查看地域ID。

 |
|Engine|String|是|MySQL|目的数据库类型，取值：**MySQL**。

 |
|DBInstanceClass|String|是|rds.mysql.s1.small|目的实例规格，详见[实例规格表](~~26312~~)。

 |
|DBInstanceStorage|Integer|是|20|目的实例存储空间，取值： **5~2000**。

 每5G进行递增，单位：GB。详见[实例规格表](~~26312~~)。

 |
|EngineVersion|String|是|5.6|目的数据库版本，取值：

 -   **5.6**；
-   **5.7**。

 |
|RestoreType|String|是|0|恢复类型，取值：

 -   **0**：基于备份集恢复，您还需要传入参数**BackupSetID**；
-   **1**：基于时间点恢复，您还需要传入参数**RestoreTime**、**SourceRegion**、**SourceDBInstanceName**。

 默认值：**0**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|BackupSetId|String|否|14358|基于备份集恢复时，使用的备份集的ID。可以通过接口[DescribeCrossRegionBackups](~~121733~~)查看备份集ID。

 **说明：** **RestoreTyp**e=**0**时必传。

 |
|RestoreTime|String|否|2019-05-30T03:29:10Z|基于时间点恢复时，要恢复的时间节点，需要早于当前时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 **说明：** **RestoreType**=**1**时必传 。

 |
|SourceRegion|String|否|cn-hangzhou|基于时间点恢复时，源地域的ID。

 **说明：** **RestoreType**=**1**时必传。

 |
|SourceDBInstanceName|String|否|rm-uf6wjk5xxxxxxx|基于时间点恢复时，源实例的ID。

 **说明：** **RestoreType**=**1**时必传。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|IsValid|String|true|是否能创建容灾恢复实例，取值：**true | false**

 |
|RequestId|String|1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CheckCreateDdrDBInstance
&RegionId=cn-hangzhou
&Engine=MySQL
&DBInstanceClass=rds.mysql.s1.small
&DBInstanceStorage=20
&EngineVersion=5.6
&RestoreType=0
&BackupSetId=14358
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CheckCreateDdrDBInstanceResponse>
  <IsValid>true</IsValid>
  <RequestId>346C62D7-8BB9-4516-93E7-25A469EAABCB</RequestId>
</CheckCreateDdrDBInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"IsValid":"true",
	"RequestId":"346C62D7-8BB9-4516-93E7-25A469EAABCB"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IncorrectDBInstanceType|Current DB instance engine and type does not support operations.|当前DB实例引擎和类型不支持操作。|
|400|InvalidRestoreType.Format|Specified restore type is not valid.|指定的恢复类型无效。|
|400|InvalidBackupType.Format|Specified backup type is not valid.|指定的备份类型无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

