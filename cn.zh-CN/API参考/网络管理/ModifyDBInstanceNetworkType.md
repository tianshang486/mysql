# ModifyDBInstanceNetworkType {#doc_api_1091246 .reference}

调用ModifyDBInstanceNetworkType接口切换RDS实例网络类型。

该接口用于将实例的网络类型从专有网络切换成经典网络，或从经典网络切换成专有网络。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceNetworkType)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceNetworkType|系统规定参数，取值：**ModifyDBInstanceNetworkType**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|InstanceNetworkType|String|是|Classic|目标网络类型，取值：

 -   **VPC**：专有网络；
-   **Classic**：经典网络。

 |
|RetainClassic|String|否|True|是否保留经典网络地址，取值：

 -   **True**：保留；
-   **False**：不保留。

 默认值：**False**。

 **说明：** 从经典网络切换到专有网络时该参数有效。

 |
|ClassicExpiredDays|String|否|7|经典网络地址保留的天数，取值**1-120**，单位：天。默认值：**7**。

 **说明：** 若传入参数**RetainClassic**=**True**，则该参数必传。

 |
|ReadWriteSplittingClassicExpiredDays|Integer|否|7|读写分离的经典网络地址保留的天数，取值**1-120**，单位：天。默认值：**7**。

 **说明：** 

-   当实例存在经典网络类型的读写分离地址，且**RetainClassic**=**True**，本参数有效。

 |
|VPCId|String|否|vpc-uf6f7l4fg90xxxxxx|VPC ID。

 |
|VSwitchId|String|否|vsw-uf6adz52c2pxxxxx|交换机ID，若传入**VPCId**，则该参数必传。

 |
|PrivateIpAddress|String|否|172.10.40.25|设置实例的内网IP，需要在指定交换机的IP地址范围内。系统默认通过**VPCId**和**VSwitchId**自动分配。

 |
|ReadWriteSplittingPrivateIpAddress|String|否|192.168.0.22|设置实例的内网读写分离地址的IP，需要在指定交换机的IP地址范围内。系统默认通过**VPCId**和**VSwitchId**自动分配。

 **说明：** 当前实例存在经典网络类型的读写分离地址时，该值有效。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |
|TaskId|String|1025486523574|任务ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyDBInstanceNetworkType
&DBInstanceId=rm-uf6wjk5xxxxxxx
&InstanceNetworkType=Classic
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceNetworkTypeResponse>
  <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</ModifyDBInstanceNetworkTypeResponse>

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
|400|NetTypeExists|Specified network type already exists.|网络类型已存在，请检查该参数是否正确。|
|403|OperationDenied.DBInstanceConnType|The current DB instance connection type does not support this operation.|网络连接类型不支持|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

