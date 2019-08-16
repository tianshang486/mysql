# CancelImport {#doc_api_Rds_CancelImport .reference}

调用CancelImport接口用于取消RDS实例迁移任务。

支持MySQL和SQL Server的独享和独占规格的实例。发起迁移任务请参见[ImportDatabaseBetweenInstances](~~26301~~)。

**说明：** 该接口暂不支持SQL Server 2017 集群版实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=CancelImport&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CancelImport|系统规定参数，取值：**CancelImport**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|ImportId|Integer|是|8562584|迁移任务ID。

 **说明：** 发起迁移任务时会返回此参数，参见[ImportDatabaseBetweenInstances](~~26301~~)。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|17F57FEE-EA4F-4337-8D2E-9C23CAA63D74|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CancelImport
&DBInstanceId=rm-uf6wjk5xxxxxxx
&ImportId=8562584
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CancelImportResponse>
         <RequestId>17F57FEE-EA4F-4337-8D2E-9C23CAA63D74</RequestId>
</CancelImportResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 17F57FEE-EA4F-4337-8D2E-9C23CAA63D74"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

