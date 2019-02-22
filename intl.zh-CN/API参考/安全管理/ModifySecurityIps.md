# ModifySecurityIps {#doc_api_1021521 .reference}

该接口用于修改允许访问实例的IP名单。

调用该接口需要实例状态为运行中，否则操作将失败 **。**

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifySecurityIps)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifySecurityIps|系统规定参数，取值：**ModifySecurityIps**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|SecurityIps|String|是|0.0.0.0/0,10.23.12.24|IP白名单分组下的IP列表，最多1000个，以英文逗号“,”隔开，格式如下：

 -   0.0.0.0/0，10.23.12.24（IP）；
-   10.23.12.24/24（CIDR模式，无类域间路由，/24表示了地址中前缀的长度，范围1~32）。

 |
|DBInstanceIPArrayName|String|否|test|IP白名单分组的名字，如果不传默认操作“Default”分组。

 **说明：** 1个实例最多支持50个白名单分组。

 |
|DBInstanceIPArrayAttribute|String|否|hidden|白名单分组属性，默认为空。

 **说明：** 用于区分不同的属性值，控制台不显示带有“hidden”标签的分组。

 |
|ModifyMode|String|否|Cover|修改方式，取值如下：

 -   **Cover**：覆盖原IP白名单；
-   **Append**：追加IP；
-   **Delete**：删除IP。

 默认值：**Cover**。

 |
|WhitelistNetworkType|String|否|Classic|白名单的网络类型。取值范围：

 -   **Classic**：高安全白名单模式下的经典网络；
-   **VPC**：高安全白名单模式下的专有网络；
-   **MIX**：通用模式，在通用白名单模式下会添加IP到通用分组里，在高安全白名单模式下会同时添加IP到经典网络和专有网络分组里。

 默认值：**MIX**。

 |
|SecurityGroupId|String|否|rg-acfmyxxxxxxxxxx|安全组编码。

 |
|SecurityIPType|String|否|IPv4|IP地址类型。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |
|TaskId|String|115855279|任务ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifySecurityIps
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&SecurityIps=0.0.0.0/0,10.23.12.24
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifySecurityIpsResponse>
  <RequestId> 1AD222E9-E606-4A42-BF6D-8A4442913CEF</RequestId>
  <TaskId>123</TaskId>
</ModifySecurityIpsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 1AD222E9-E606-4A42-BF6D-8A4442913CEF",
	"TaskId":123
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

