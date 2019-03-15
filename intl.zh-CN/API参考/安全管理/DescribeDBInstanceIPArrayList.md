# DescribeDBInstanceIPArrayList {#doc_api_1066780 .reference}

调用DescribeDBInstanceIPArrayList接口查看RDS实例IP白名单。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceIPArrayList)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstanceIPArrayList|系统规定参数，取值：**DescribeDBInstanceIPArrayList**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|WhitelistNetworkType|String|否|VPC|白名单的网络类型，取值：

 -   **Classic**：高安全白名单模式下的经典网络；
-   **VPC**：高安全白名单模式下的专有网络；
-   **MIX**：通用白名单模式。

 默认返回所有网络类型的白名单IP。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Items| | |IP白名单分组列表。

 |
|└DBInstanceIPArrayName|String|rds\_default|IP白名单分组名称。

 |
|└DBInstanceIPArrayAttribute|String|hidden|白名单分组属性，默认为空。

 **说明：** 控制台不显示带有“hidden”属性的分组，带有该标签的分组通常是用于访问DTS、DRDS服务的。

 |
|└SecurityIPList|String|192.168.1.0/24|IP白名单分组下的IP列表，最多1000个，以英文逗号（,）隔开。

 |
|└SecurityIPType|String|IPv4|IP地址的类型。

 |
|RequestId|String|E2B6AF71-DC32-4055-B477-43B348798D10|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDBInstanceIPArrayList
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstanceIPArrayListResponse>
  <Items>
    <DBInstanceIPArray>
      <DBInstanceIPArrayName>rds_default</DBInstanceIPArrayName>
      <DBInstanceIPArrayAttribute/>
      <WhitelistNetworkType>VPC</WhitelistNetworkType>
      <SecurityIPList>192.168.1.0/24</SecurityIPList>
      <SecurityIPType>IPv4</SecurityIPType>
    </DBInstanceIPArray>
  </Items>
  <RequestId>E2B6AF71-DC32-4055-B477-43B348798D10</RequestId>
</DescribeDBInstanceIPArrayListResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"DBInstanceIPArray":[
			{
				"DBInstanceIPArrayName":"rds_default",
				"DBInstanceIPArrayAttribute":"",
				"WhitelistNetworkType":"VPC",
				"SecurityIPType":"IPv4",
				"SecurityIPList":"192.168.1.0/24"
			}
		]
	},
	"RequestId":"E2B6AF71-DC32-4055-B477-43B348798D10"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

