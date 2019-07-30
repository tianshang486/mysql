# UpgradeDBInstanceEngineVersion {#doc_api_Rds_UpgradeDBInstanceEngineVersion .reference}

调用UpgradeDBInstanceEngineVersion接口升级实例数据库版本。

**说明：** 升级后根据新老规格信息和磁盘类型信息计算差价。

如果主实例下挂载只读实例或者灾备实例，请先升级只读实例或者灾备实例的数据库版本。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   仅支持从MySQL 5.5升级到MySQL 5.6。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=UpgradeDBInstanceEngineVersion&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpgradeDBInstanceEngineVersion|系统规定参数，取值：**UpgradeDBInstanceEngineVersion**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|待升级的实例ID。

 |
|EngineVersion|String|是|5.6|目标数据库版本，取值：**5.6**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|EffectiveTime|String|否|Immediate|生效时间，取值：

 -   **Immediate**：立即生效；
-   **MaintainTime**：在可运维时间段内生效，请参见[ModifyDBInstanceMaintainTime](~~26249~~)。

 默认值：**Immediate**。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |

## 返回数据 {#resultMapping .section}

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
	  <TaskId>10254125</TaskId></UpgradeDBInstanceEngineVersionResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64",
	"TaskId":"10254125"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

