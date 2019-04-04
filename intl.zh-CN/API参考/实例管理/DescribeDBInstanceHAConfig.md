# DescribeDBInstanceHAConfig {#doc_api_Rds_DescribeDBInstanceHAConfig .reference}

调用DescribeDBInstanceHAConfig接口查询RDS实例高可用模式和数据复制方式。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceHAConfig)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstanceHAConfig|系统规定参数，取值：**DescribeDBInstanceHAConfig**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxx|实例ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxx|实例ID。

 |
|HAMode|String|RPO|高可用模式，取值：

 -   **RPO**：数据一致性优先，实例会尽可能保障数据的可靠性，即数据丢失量最少。对于数据一致性要求比较高的用户应该使用RPO模式；
-   **RTO**：实例可用性优先，实例会尽快恢复服务，即可用时间最长。对于数据库在线时间要求比较高的用户应该使用RTO模式。

 |
|SyncMode|String|Sync|[数据复制方式](~~26183~~)，取值：

 -   **Sync**：强同步；
-   **Semi-sync**：半同步；
-   **Async**：异步。

 **说明：** 

-   对于SQL Server 2012/2016双机高可用版，值为**Sync**或**Async**；
-   对于SQL Server 2017集群版，值为**Semi-sync**。

 |
|HostInstanceInfos| | |主备实例信息列表。

 |
|└NodeId|String|3397027|实例的唯一标识。

 |
|└NodeType|String|Master|节点类型，取值：

 -   **Master**：主节点；
-   **Slave**：备节点。

 |
|└RegionId|String|cn-hangzhou|地域ID。

 |
|└ZoneId|String|cn-hangzhou-b|可用区ID。

 |
|└SyncStatus|String|NotAvailable|同步状态，取值：

 -   **NotAvailable**：不可用，即发生故障；
-   **Syncing**：同步中，切换可能会发生数据丢失；
-   **Synchronized**：完成同步；
-   **NotSupport**：引擎类型或者版本不涉及主备同步。

 |
|└LogSyncTime|String|2018-05-05T15:15:00Z|备实例与主实例的日志同步时间差，单位为毫秒。

 |
|└DataSyncTime|String|2018-05-05T15:15:00Z|备实例上的日志应用时间差，单位为毫秒。

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDBInstanceHAConfig
&DBInstanceId=rm-uf6wjk5xxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstanceHAConfigResponse>
  <dBInstanceId>rm-uf6wjk5xxxxxx</dBInstanceId>
  <hAMode>RPO</hAMode>
  <hostInstanceInfos>
    <logSyncTime>2018-01-19T12:33:06Z</logSyncTime>
    <nodeId>3397027</nodeId>
    <nodeType>Slave</nodeType>
    <regionId>cn-shenzhen</regionId>
    <syncStatus>Syncing</syncStatus>
    <zoneId>cn-shenzhen-b</zoneId>
  </hostInstanceInfos>
  <hostInstanceInfos>
    <logSyncTime>2018-01-19T12:33:06Z</logSyncTime>
    <nodeId>3397029</nodeId>
    <nodeType>Master</nodeType>
    <regionId>cn-shenzhen</regionId>
    <syncStatus>Syncing</syncStatus>
    <zoneId>cn-shenzhen-a</zoneId>
  </hostInstanceInfos>
  <requestId>F051AEB2-7655-4F0A-BC46-7E0C18A7910C</requestId>
  <syncMode>Semi-sync</syncMode>
</DescribeDBInstanceHAConfigResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"hostInstanceInfos":[
		{
			"nodeId":"3397027",
			"syncStatus":"Syncing",
			"logSyncTime":"2018-01-19T12:33:06Z",
			"nodeType":"Slave",
			"zoneId":"cn-shenzhen-b",
			"regionId":"cn-shenzhen"
		},
		{
			"nodeId":"3397029",
			"syncStatus":"Syncing",
			"logSyncTime":"2018-01-19T12:33:06Z",
			"nodeType":"Master",
			"zoneId":"cn-shenzhen-a",
			"regionId":"cn-shenzhen"
		}
	],
	"requestId":"F051AEB2-7655-4F0A-BC46-7E0C18A7910C",
	"syncMode":"Semi-sync",
	"hAMode":"RPO",
	"dBInstanceId":"rm-uf6wjk5xxxxxx"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

