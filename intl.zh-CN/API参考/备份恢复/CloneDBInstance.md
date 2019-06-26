# CloneDBInstance {#doc_api_Rds_CloneDBInstance .reference}

调用CloneDBInstance接口将历史数据恢复至一个新实例（称为克隆实例）。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   实例当前没有正在执行的迁移任务；
-   实例已开启日志备份（用于按时间点恢复）；
-   若要按备份集克隆实例，则主实例必须至少有一个已完成备份的备份集。

**说明：** RDS支持RAM子账号创建克隆实例，请务必保证子账号已添加克隆实例的授权策略，添加授权请参见 [云数据库RDS授权](~~58932~~) 。


实例内数据库账号信息克隆以及其他功能的设置克隆将遵循如下方式：

-   实例内的白名单设置、SQL审计设置、阈值报警设置、备份设置、参数设置将和当前实例状态保持一致；
-   实例内的数据信息、账号信息与备份文件或时间点当时信息一致。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CloneDBInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
| Action |String|是|CloneDBInstance| 系统规定参数，取值： **CloneDBInstance** 。

 |
| PayType |String|是|Postpaid| 付费类型，取值：

 -    **Postpaid** ：后付费（按量付费）；
-    **Prepaid** ：预付费（包年包月）。

 |
| RegionId |String|否|cn-hangzhou| 地域ID，可以通过接口 [DescribeRegions](~~26243~~) 查看可用的地域ID。

 |
| ZoneId |String|否|cn-hangzhou-b| 可用区ID。

 |
| DBInstanceClass |String|否|mysql.n1.micro.1| 实例规格，详见 [实例规格表](~~26312~~) 。

 **说明：** 默认规格和主实例一致。

 |
| DBInstanceStorage |Integer|否|1000| 实例存储空间，单位：GB。每5GB进行递增，详见 [实例规格表](~~26312~~) 。

 **说明：** 默认存储空间和主实例一致。

 |
| DbNames |String|否|testDB| 数据库名称。

 |
| InstanceNetworkType |String|否|VPC| 实例的网络类型，取值：

 -    **VPC** ：专有网络；
-    **Classic** ：经典网络。

 **说明：** 默认网络类型和主实例一致。

 |
| BackupId |String|否|9026262| 备份集ID。

 您可以通过 [DescribeBackups](~~26273~~) 接口获取备份列表。

 **说明：** **BackupId** 和 **RestoreTime** 两者至少传入一个。

 |
| DBInstanceId |String|否|rm-uf6wjk5xxxxxxxxxx| 实例ID。

 |
| RestoreTime |String|否|2011-06-11T16:00:00Z| 备份保留周期内的任意时间点。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 **说明：** **BackupId** 和 **RestoreTime** 两者至少传入一个。

 |
| VPCId |String|否|vpc-uf6f7l4fg90xxxxxxxxxx| VPC ID。

 |
| VSwitchId |String|否|vsw-uf6adz52c2pxxxxxxxxxx| VSwitch ID。

 |
| PrivateIpAddress |String|否|172.16.201.69| 新实例的内网IP，需要在指定交换机的IP地址范围内。系统默认通过 **VPCId** 和 **VSwitchId** 自动分配。

 |
| UsedTime |String|否|1| 购买时长，取值：

 -   当参数 **Period** 为 **Year** 时，UsedTime取值为 **1~3** ；
-   当参数 **Period** 为 **Month** 时，UsedTime取值为 **1~9** 。

 **说明：** 若付费类型为 **Prepaid** 则该参数必须传入。

 |
| Period |String|否|Year| 预付费实例为包年或者包月类型，取值：

 -    **Year** ：包年；
-    **Month** ：包月。

 **说明：** 若付费类型为 **Prepaid** 则该参数必须传入。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx| 实例ID。

 |
|OrderId|String|100789370xxxxx| 订单ID。

 |
|RequestId|String|1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC| 请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CloneDBInstance
&BackupId=9026262
&PayType=Postpaid
&<公共请求参数>

```

正常返回示例

 `XML` 格式

``` {#xml_return_success_demo}
<CloneDBInstanceResponse>
  <OrderId>100789370xxxxx</OrderId>
  <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
  <RequestId>1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC</RequestId>
</CloneDBInstanceResponse>

```

 `JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC",
	"DBInstanceId":"rm-uf6wjk5xxxxxxx",
	"OrderId":"100789370xxxxx"
}
```

## 错误码 { .section}

 [查看本产品错误码](https://error-center.aliyun.com/status/product/Rds) 

