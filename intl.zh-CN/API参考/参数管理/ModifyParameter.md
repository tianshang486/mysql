# ModifyParameter {#doc_api_1102294 .reference}

调用ModifyParameter接口修改实例参数。

调用该接口时，实例状态必须为运行中，否则将操作失败。

可以修改的参数请在控制台查看，请参见[使用控制台设置参数](~~26179~~)。

提交修改请求后，RDS将下发任务，将新修改的参数应用到实例，如果所提交的参数中有需要重启数据库的，RDS将重启数据库。

下达任务之前，RDS将会进行参数检查，方法如下：

-   参数是否存在；
-   参数是否可修改；
-   参数是否合法。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyParameter)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyParameter|系统规定参数，取值：**ModifyParameter**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|Parameters|String|是|\{"delayed\_insert\_timeout":"600","max\_length\_for\_sort\_data":"2048"\}|参数及其值的JSON串，参数的值都是字符串类型。格式：\{"参数名称1":"参数值1","参数名称2":"参数值2"...\}

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|Forcerestart|Boolean|否|false|修改参数是否重启数据库，取值：

 -   **true**：强制重启（若修改的参数当中，有需要重启的参数，则必须传入true，否则修改将不生效）。
-   **false**：不强制重启。

 默认值：**false**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|542BB8D6-4268-45CC-A557-B03EFD7AB30A|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyParameter
&DBInstanceId=rm-uf6wjk5xxxxxxx
&Parameters={"delayed_insert_timeout":"600","max_length_for_sort_data":"2048"}
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyeParameterResponse>
  <RequestId>542BB8D6-4268-45CC-A557-B03EFD7AB30A</RequestId>
</ModifyeParameterResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"542BB8D6-4268-45CC-A557-B03EFD7AB30A"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

