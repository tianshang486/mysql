# CreateDdrInstance {#doc_api_Rds_CreateDdrInstance .reference}

调用CreateDdrInstance接口跨地域恢复数据到新实例。

恢复前可以调用[CheckCreateDdrDBInstance](~~121721~~)接口预检查某RDS实例是否可以用跨地域备份集进行跨地域恢复。

仅适用于如下实例：

-   MySQL 5.7高可用本地SSD盘版
-   MySQL 5.6

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CreateDdrInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDdrInstance|系统规定参数，取值：**CreateDdrInstance**。

 |
|RegionId|String|是|cn-hangzhou|目的地域ID，可以通过接口[DescribeRegions](~~26243~~)查看地域ID。

 |
|Engine|String|是|MySQL|目的数据库类型，取值：**MySQL**。

 |
|EngineVersion|String|是|5.6|目的数据库版本，取值：

 -   **5.6**；
-   **5.7**。

 |
|DBInstanceClass|String|是|rds.mysql.s1.small|目的实例规格，详见[实例规格表](~~26312~~)。

 |
|DBInstanceStorage|Integer|是|20|目的实例存储空间，取值： **5~2000**。

 每5G进行递增，单位：GB。详见[实例规格表](~~26312~~)。

 |
|DBInstanceNetType|String|是|Intranet|目的实例的网络连接类型，取值：

 -   **Internet**：公网连接；
-   **Intranet**：内网连接。

 |
|PayType|String|是|Prepaid|目的实例的付费类型，取值：

 -   **Postpaid**：后付费（按量付费）；
-   **Prepaid**：预付费（包年包月）。

 |
|RestoreType|String|是|0|恢复方式，取值：

 -   **0**：基于备份集恢复，您还需要传入参数**BackupSetID**；
-   **1**：基于时间点恢复，您还需要传入参数**RestoreTime**、**SourceRegion**、**SourceDBInstanceName**。

 |
|SecurityIPList|String|是|127.0.0.1|目的实例的[IP白名单](~~43185~~)，多个IP地址请以英文逗号（,）隔开，不可重复，最多1000个。支持如下两种格式：

 -   IP地址形式，例如：10.23.12.24；
-   CIDR形式，例如：10.23.12.24/24（无类域间路由，24表示了地址中前缀的长度，范围为1~32）。

 |
|InstanceNetworkType|String|否|Classic|目的实例的网络类型，取值：

 -   **VPC**：VPC网络；
-   **Classic**：经典网络。

 默认创建经典网络类型的实例。

 **说明：** 当本参数值为 **VPC**时，还需要传入参数**VpcId**、**VSwitchId**。

 |
|ZoneId|String|否|cn-hangzhou-b|目的实例的可用区ID。多可用区用英文冒号（:）分隔。

 **说明：** 指定了VPC和交换机时，为匹配交换机对应的可用区，该参数必填。

 |
|VPCId|String|否|vpc-xxxxxxxxxxxx|目的实例的VPC ID。当**InstanceNetworkType**=**VPC**时，本参数可用。

 **说明：** 如果传入此参数，您还需要传入参数**ZoneId**。

 |
|DBInstanceStorageType|String|否|local\_ssd|目的实例存储类型，当前仅支持SSD本地盘，默认值：**local\_ssd**。

 |
|VSwitchId|String|否|vsw-xxxxxxxxxxx|目的实例的VSwitch ID，多个值用英文逗号（,）隔开。当**InstanceNetworkType**=**VPC**时，本参数可用。

 **说明：** 如果传入此参数，您还需要传入参数**ZoneId**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ConnectionMode|String|否|Standard|目的实例的访问模式，取值：

 -   **Standard**：标准访问模式；
-   **Safe**：数据库代理模式。

 默认值：**Standard**。

 |
|SystemDBCharset|String|否|uft8|目的实例的字符集，取值：

 -   **utf8**；
-   **gbk**；
-   **latin1**；
-   **utf8mb4**。

 |
|DBInstanceDescription|String|否|测试数据库|目的实例名称，长度为2~256个字符。以中文、英文字母开头，可以包含数字、中文、英文、下划线（\_）、短横线（-）。

 **说明：** 不能以 http:// 和 https:// 开头。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|PrivateIpAddress|String|否|172.16.201.69|设置目的实例的内网IP，需要在指定交换机的IP地址范围内。系统默认通过**VPCId**和**VSwitchId**自动分配。

 |
|Period|String|否|Year|指定预付费目的实例为包年或者包月类型，取值：

 -   **Year**：包年；
-   **Month**：包月。

 **说明：** 若付费类型为**Prepaid**则该参数必须传入。

 |
|BackupSetId|String|否|14358|基于备份集恢复时，使用的备份集的ID。可以通过接口[DescribeCrossRegionBackups](~~121733~~)查看备份集ID。

 **说明：** **RestoreTyp**e=**0**时必传。

 |
|SourceDBInstanceName|String|否|rm-uf6wjk5xxxxxxx|基于时间点恢复时，源实例的ID。

 **说明：** **RestoreType**=**1**时必传。

 |
|SourceRegion|String|否|cn-hangzhou|基于时间点恢复时，源地域的ID。

 **说明：** **RestoreType**=**1**时必传。

 |
|RestoreTime|String|否|2019-05-30T03:29:10Z|基于时间点恢复时，要恢复的时间节点，需要早于当前时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 **说明：** **RestoreType**=**1**时必传 。

 |
|UsedTime|String|否|2|指定购买时长，取值：

 -   当参数**Period**为**Year**时，UsedTime取值为**1~3**；
-   当参数**Period**为**Month**时，UsedTime取值为**1~9**。

 **说明：** 若付费类型为**Prepaid**则该参数必须传入。

 |
|ResourceGroupId|String|否|rg-acfmyxxxxxxxxxx|资源组ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-xxxxx|新实例ID。

 |
|ConnectionString|String|rm-xxxxx.mysql.rds.aliyuncs.com|新实例连接地址。

 **说明：** 参数**DBInstanceNetType**决定该地址为内网或外网。

 |
|OrderId|String|2038691xxxxx|订单ID。

 |
|Port|String|3306|新实例连接端口。

 **说明：** 参数**DBInstanceNetType**决定该端口为内网端口或外网端口。

 |
|RequestId|String|E52666CC-330E-418A-8E5B-A19E3FB42D13|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action==CreateDdrInstance
&RegionId=cn-hangzhou
&Engine=MySQL
&EngineVersion=5.6
&DBInstanceClass=rds.mysql.s1.small
&DBInstanceStorage=20
&DBInstanceNetType=Intranet
&PayType=Prepaid
&RestoreType=0
&SecurityIPList=127.0.0.1
&BackupSetId=14358
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateDdrInstanceResponse>
  <ConnectionString>rm-xxxxx.mysql.rds.aliyuncs.com</ConnectionString>
  <Port>3306</Port>
  <RequestId>E52666CC-330E-418A-8E5B-A19E3FB42D13</RequestId>
  <DBInstanceId>rm-xxxxx</DBInstanceId>
  <OrderId>2038691xxxxx</OrderId>
</CreateDdrInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Port":"3306",
	"ConnectionString":"rm-xxxxx.mysql.rds.aliyuncs.com",
	"OrderId":"2038691xxxxx",
	"DBInstanceId":"rm-xxxxx",
	"RequestId":"E52666CC-330E-418A-8E5B-A19E3FB42D13"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidZoneId.NotSupported|The Specified vpc Zone not supported.|当前可用区不支持生产 VPC 实例，请您更换可用区再试。|
|400|InvalidDBInstanceName.Format|Specified DB instance name is not valid.|指定的DB实例名不正确。|
|400|InvalidServiceType.Format|Specified service type is not valid.|指定的服务类型无效。|
|400|InvalidEngine.Malformed|Specified engine is not valid.|指定数据库引擎无效。|
|400|InvalidEngineVersion.Malformed|Specified engine version is not valid.|指定数据库引擎版本无效。|
|400|InvalidConnectionString.Format|Specified connection string is not valid.|指定的连接字符串无效。|
|400|InvalidConnectionString.Duplicate|Specified connection string already exists in the Aliyun RDS.|在阿里云RDS中已经存在指定的连接字符串。|
|400|InvalidCharacterSetName.Format|Specified character set name is not valid.|指定的字符集名称无效。|
|400|InvalidDBInstanceType.Format|Specified instance type is not valid.|指定实例类型无效。|
|400|InvalidPort.Malformed|Specified port is not valid.|指定端口无效。|
|400|InvalidBackupRetentionPeriod.Malformed|Specified backup retention period is not valid.|指定的备份保留期无效。|
|400|InvalidPreferredBackupTime.Format|Specified preferred backup time is not valid.|指定的期望备份时间无效。|
|400|InvalidPreferredBackupPeriod.Malformed|Specified backup period is not valid.|指定的期望备份时间无效。|
|404|InvalidDBInstanceClass.NotFound|Specified DB instance class is not found.|实例规格无效，请检查该参数是否正确。|
|404|InvalidDBInstanceNetType.NotFound|Specified DB instance net type is not found.|指定DB实例网络类型不存在。|
|400|InvalidOptmizationService|Specified optmization service is not valid.|参数OptmizationService无效|
|400|InvalidExpiredTime.Format|Specified expired time is not valid.|指定的失效时间不正确。|
|400|InvalidSecurityIPList.Format|Specified security IP list format is not valid.|指定的安全IP列表格式不正确。|
|400|InvalidSecurityIPList.QuotaExceeded|Specified security IP list is not valid: Exceeding the allowed amount of IP address in the list.|指定的安全IP列表中包含的IP地址数超过允许上限。|
|400|InvalidDBInstanceDescription.Format|Specified DB instance description is not valid.|指定的DB实例描述无效。|
|400|InvalidStorage.Format|Specified Storage is not valid.|指定的Storage参数无效。|
|400|IncorrectDBInstanceType|Current DB instance engine and type does not support operations.|当前DB实例引擎和类型不支持操作。|
|400|InvalidRestoreType.Format|Specified restore type is not valid.|指定的恢复类型无效。|
|400|InvalidBackupType.Format|Specified backup type is not valid.|指定的备份类型无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

