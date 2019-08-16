# MigrateToOtherZone {#doc_api_Rds_MigrateToOtherZone .reference}

调用MigrateToOtherZone接口将RDS实例迁移至其他可用区。

例如，实例目前位于华东1\(杭州\) 的cn-hangzhou-a可用区，调用此接口可以将该实例迁移至杭州的cn-hangzhou-b可用区。

**说明：** 仅支持迁移到同一地域的其它可用区，不支持迁移到其它地域的可用区，如华东1\(杭州\) 可用区内的实例不支持迁移至华北1\(青岛\) 的可用区。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=MigrateToOtherZone&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|MigrateToOtherZone|系统规定参数，取值：**MigrateToOtherZone**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|ZoneId|String|是|cn-hangzhou-b|目标可用区ID，可以通过[DescribeRegions](~~26243~~)接口查看。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|VSwitchId|String|否|vsw-uf6adz52c2pxxxxxxx|交换机ID。

 |
|EffectiveTime|String|否|Immediate|生效时间，取值：

 -   **Immediate**：立即生效；
-   **MaintainTime**：在可运维时间段内生效，请参见[ModifyDBInstanceMaintainTime](~~26249~~)。

 默认值：**Immediate**。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=MigrateToOtherZone
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&ZoneId=cn-hangzhou-b
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<MigrateToOtherZoneResponse>
	  <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId></MigrateToOtherZoneResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IncorrectDBInstanceLockMode.ValueNotSupported|The Current DB instance lock mode does not support this operation.|当前DB实例锁模式不支持此操作。|
|403|OperationDenied.OutofUsage|The resource is out of usage.|资源不足，请选择其他可用区。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

