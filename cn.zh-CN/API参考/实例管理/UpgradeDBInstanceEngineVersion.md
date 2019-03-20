# UpgradeDBInstanceEngineVersion {#doc_api_1102542 .reference}

调用UpgradeDBInstanceEngineVersion接口升级实例数据库版本。

**说明：** **升级后根据新老规格信息和磁盘类型信息计算差价。**

如果主实例下挂载只读实例或者灾备实例，请先升级只读实例或者灾备实例的数据库版本。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   目前支持从MySQL 5.5升级到MySQL 5.6，以及从SQL Server 2008 R2升级到SQL Server 2012/2016企业版、SQL Server 2016标准版。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=UpgradeDBInstanceEngineVersion)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpgradeDBInstanceEngineVersion|系统规定参数，取值：UpgradeDBInstanceEngineVersion。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|待升级的实例ID。

 |
|EngineVersion|String|是|5.6|目标数据库版本，取值：

 -   MySQL：**5.6**；
-   SQL Server：**2016\_web/2012\_std\_ha/2016\_std\_ha/2012\_ent\_ha/2016\_ent\_ha**

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|EffectiveTime|String|否|Immediate|生效时间，取值：

 -   **Immediate**：立即生效；
-   **MaintainTime**：在可运维时间段内生效，请参见[ModifyDBInstanceMaintainTime](~~26249~~)。

 默认值：**Immediate**。

 |
|DBInstanceClass|String|否|mssql.x4.medium.s2|目标实例规格，详见[实例规格表](~~26312~~)。MySQL可以为空，SQL Server需要传入。

 |
|DBInstanceStorageType|String|否|cloud\_ssd|目标存储类型，MySQL可以为空，SQL Server需要传入。取值：

 -   **local\_ssd/ephemeral\_ssd**：本地SSD盘；
-   **cloud\_ssd**：SSD云盘；
-   **cloud\_essd**：ESSD云盘。

 |
|ZoneId|String|否|cn-hangzhou-b|目标可用区ID，默认和实例当前可用区一致。

 |
|InstanceNetworkType|String|否|VPC|目标网络类型，MySQL可以为空，SQL Server需要传入。取值：

 -   **VPC**：专有网络；
-   **Classic**：经典网络。

 |
|VpcId|String|否|vpc-xxxxxxxxxxxx|目标VPC ID，MySQL可以为空，SQL Server需要传入。

 |
|VSwitchId|String|否|vsw-xxxxxxxxxxx|目标交换机ID，MySQL可以为空，SQL Server需要传入。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|TaskId|String|10254125|任务ID。

 |
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=UpgradeDBInstanceEngineVersion
&DBInstanceId=rm-uf6wjk5xxxxxxx
&EngineVersion=5.6
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UpgradeDBInstanceEngineVersionResponse>
  <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
  <TaskId>10254125</TaskId>
</UpgradeDBInstanceEngineVersionResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64",
	"TaskId":"10254125"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

