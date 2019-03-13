# ModifyDBInstanceHAConfig {#doc_api_1063673 .reference}

调用ModifyDBInstanceHAConfig接口修改实例的高可用模式和数据复制方式。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceHAConfig)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceHAConfig|系统规定参数，取值：**ModifyDBInstanceHAConfig**。

 |
|DbInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|HAMode|String|是|RPO|高可用模式，取值：

 -   **RPO**：数据一致性优先，实例会尽可能保障数据的可靠性，即数据丢失量最少。对于数据一致性要求比较高的用户应该使用RPO模式；
-   **RTO**：实例可用性优先，实例会尽快恢复服务，即可用时间最长。对于数据库在线时间要求比较高的用户应该使用RTO模式。

 |
|SyncMode|String|是|Sync|[数据复制方式](~~26183~~)，取值：

 -   **Sync**：强同步；
-   **Semi-sync**：半同步；
-   **Async**：异步。

 **说明：** 

-   对于SQL Server 2012/2016双机高可用版，值为**Sync**或**Async**；
-   对于SQL Server 2017集群版，值为**Semi-sync**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyDBInstanceHAConfig
&DbInstanceId=rm-uf6wjk5xxxxxxx
&HAMode=RPO
&SyncMode=Sync
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceHAConfigResponse>
  <RequestId>D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD</RequestId>
</ModifyDBInstanceHAConfigResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"D4D4BE8A-DD46-440A-BFCD-EE31DA81C9DD"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

