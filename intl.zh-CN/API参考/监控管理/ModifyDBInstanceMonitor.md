# ModifyDBInstanceMonitor {#doc_api_Rds_ModifyDBInstanceMonitor .reference}

调用ModifyDBInstanceMonitor修改监控频率。

 **请确保在使用该接口前，已充分了解RDS产品的收费方式和[价格](https://www.alibabacloud.com/product/apsaradb-for-rds#pricing)。** 

阿里云对不同实例提供不同的监控频率，详情请参见[设置监控频率](~~26200~~)。

**说明：** 秒级监控需要收取额外费用。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceMonitor&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceMonitor|系统规定参数，取值：**ModifyDBInstanceMonitor**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|Period|String|是|60|监控的采集间隔，取值：

 -   **5**；
-   **60**；
-   **300**。

 单位：秒。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|52B9805C-432C-4ED1-83FD-2F916B6D2733|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyDBInstanceMonitor
&DBInstanceId=rm-uf6wjk5xxxxxxx
&Period=60
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceMonitorResponse>
	  <requestId>52B9805C-432C-4ED1-83FD-2F916B6D2733</requestId></ModifyDBInstanceMonitorResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"52B9805C-432C-4ED1-83FD-2F916B6D2733"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDBInstanceId.NotFound|The DBInstanceId provided does not exist in our records.|实例不存在。确认该实例是在当前账号下面，确定未被删除。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

