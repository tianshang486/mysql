# SwitchDBInstanceHA {#doc_api_Rds_SwitchDBInstanceHA .reference}

调用SwitchDBInstanceHA接口切换RDS实例的主备实例。

本接口可用于切换高可用版RDS实例的主备实例，切换主备实例后，原来的备实例成为主实例并承担业务流量。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=SwitchDBInstanceHA&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SwitchDBInstanceHA|系统规定参数，取值：**SwitchDBInstanceHA**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|NodeId|String|是|349054|备实例的唯一标识，通过接口[DescribeDBInstanceHAConfig](~~26244~~)可查询该值。

 |
|Force|String|否|No|切换方式，取值：

 -   **Yes**：强制；
-   **No**：非强制。

 默认值：**No**。

 |
|EffectiveTime|String|否|Immediate|生效时间，取值：

 -   **Immediate**：立即执行；
-   **MaintainTime**：可维护时间内执行。

 默认值：**Immediate**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=SwitchDBInstanceHA
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&NodeId=349054
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<SwitchDBInstanceHAResponse>
	  <RequestId>1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC</RequestId></SwitchDBInstanceHAResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

