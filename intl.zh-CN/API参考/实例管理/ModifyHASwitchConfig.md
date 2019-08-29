# ModifyHASwitchConfig {#doc_api_Rds_ModifyHASwitchConfig .reference}

调用ModifyHASwitchConfig接口开启或关闭RDS实例的主备切换功能。

主备实例切换后原来的主实例会变成备实例。详情请参见[切换主备实例](~~96054~~)。

调用该接口时，实例必须为高可用版。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=ModifyHASwitchConfig&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyHASwitchConfig|系统规定参数，取值：**ModifyHASwitchConfig**。

 |
|RegionId|String|是|cn-hangzhou|地域ID，可以通过接口[DescribeRegions](~~26243~~)查看地域ID。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|HAConfig|String|否|Manual|主备切换设置，取值：

 -   **Auto**：出现故障时自动切换主备实例；
-   **Manual**：临时关闭自动切换。

 默认值：**Auto**。

 **说明：** 取值为**Manual**时，必须传入参数**ManualHATime**。

 |
|ManualHATime|String|否|2019-08-29T15:00:00Z|临时关闭的截止时间。最晚可设置为7天后的23:59:59。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 **说明：** 仅当参数**HAConfig**取值为**Manual**时，本参数有效。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B6AE1448-D846-4831-B1C7-CFF3E99D5470|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyHASwitchConfig
&RegionId=cn-hangzhou
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&HAConfig=Manual
&ManualHATime=2019-08-28T15:00:00
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyHASwitchConfigResponse>
  <RequestId>B6AE1448-D846-4831-B1C7-CFF3E99D5470</RequestId>
</ModifyHASwitchConfigResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"B6AE1448-D846-4831-B1C7-CFF3E99D5470"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

