# ResetAccount {#doc_api_Rds_ResetAccount .reference}

调用ResetAccount接口重置高权限账号的权限。

**说明：** 该接口不适用于没有高权限账号的SQL Server 2008 R2实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=ResetAccount&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ResetAccount|系统规定参数，取值：**ResetAccount**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccountName|String|是|test1|高权限账号名称。

 |
|AccountPassword|String|是|Test123456|设置新的高权限账号的密码。

 **说明：** 

-   长度为8~32个字符；
-   由大写字母、小写字母、数字、特殊字符中的任意三种组成；
-   特殊字符为!@\#$&%^\*\(\)\_+-=

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|81BC9559-7B22-4B7F-B705-5F56DEECDEA7|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ResetAccount
&AccountName=test1
&AccountPassword=Test123456
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ResetAccountResponse>
	  <RequestId>81BC9559-7B22-4B7F-B705-5F56DEECDEA7</RequestId></ResetAccountResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"81BC9559-7B22-4B7F-B705-5F56DEECDEA7"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

