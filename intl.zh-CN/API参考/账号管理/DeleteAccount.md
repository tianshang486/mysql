# DeleteAccount {#doc_api_Rds_DeleteAccount .reference}

调用DeleteAccount接口删除数据库账号。

调用该接口时，实例状态需要为运行中，否则将操作失败：

**说明：** 该接口暂不支持SQL Server 2017集群版、PostgreSQL、PPAS实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DeleteAccount&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteAccount|系统规定参数，取值：**DeleteAccount**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccountName|String|是|test1|需要删除的数据库账号名称。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91E855E5-7E80-4955-929B-C74EE1D38C66|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DeleteAccount
&DBInstanceId=rm-uf6wjk5xxxxxxx
&AccountName=test1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteAccountResponse>
	  <RequestID>91E855E5-7E80-4955-929B-C74EE1D38C66</RequestID></DeleteAccountResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestID":"91E855E5-7E80-4955-929B-C74EE1D38C66"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

