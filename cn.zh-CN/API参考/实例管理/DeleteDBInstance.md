# DeleteDBInstance {#doc_api_Rds_DeleteDBInstance .reference}

调用DeleteDBInstance接口释放RDS实例。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   实例已关闭读写分离；
-   实例类型为主实例（按量付费类型）、只读实例、灾备实例、临时实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DeleteDBInstance&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteDBInstance|系统规定参数，取值：**DeleteDBInstance**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DeleteDBInstance
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteDBInstanceResponse>
	  <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId></DeleteDBInstanceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

