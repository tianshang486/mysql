# AllocateInstancePublicConnection {#doc_api_Rds_AllocateInstancePublicConnection .reference}

调用AllocateInstancePublicConnection接口申请实例的外网地址。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=AllocateInstancePublicConnection&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AllocateInstancePublicConnection|系统规定参数，取值：**AllocateInstancePublicConnection**。

 |
|ConnectionStringPrefix|String|是|test1.mysql.rds.aliyuncs.com|外网连接地址，前缀可以自定义。

 **说明：** 长度5~40，不能包含汉字和非法字符（~!\#%^&\*=+\\|\{\};:'",<\>/?），建议由字母、数字、短横线（-）组成。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|Port|String|是|3306|外网连接端口，取值：**1000-5999**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=AllocateInstancePublicConnection
&ConnectionStringPrefix=test1.mysql.rds.aliyuncs.com
&DBInstanceId=rm-uf6wjk5xxxxxxx
&Port=3306
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AllocateInstancePublicConnectionResponse>
         <RequestId>65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</AllocateInstancePublicConnectionResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

