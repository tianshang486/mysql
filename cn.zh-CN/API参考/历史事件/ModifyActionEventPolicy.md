# ModifyActionEventPolicy {#doc_api_Rds_ModifyActionEventPolicy .reference}

调用ModifyActionEventPolicy接口开启或关闭RDS历史事件功能。

RDS提供历史事件功能，开启后您可以所处地域内查看某时间段的历史事件，例如在某个时间创建了实例、修改了参数等等。详情请参见[历史事件](~~129759~~)。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=ModifyActionEventPolicy&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyActionEventPolicy|系统规定参数，取值：**ModifyActionEventPolicy**。

 |
|EnableEventLog|String|是|True|是否开启历史事件记录功能。取值：**True | False**

 |
|RegionId|String|是|cn-hangzhou|需要开启或关闭历史事件功能的地域ID，可以通过接口[DescribeRegions](~~26243~~)查看地域ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|EnableEventLog|String|True|历史事件功能的启用情况。

 |
|RegionId|String|cn-hangzhou|开启或关闭历史事件功能的地域ID。

 |
|RequestId|String|BAC0952C-0EB3-4DE7-A567-B83269BFE43F|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyActionEventPolicy
&Region=cn-hangzhou
&EnableEventLog=True
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyActionEventPolicyResponse>
  <RequestId>BAC0952C-0EB3-4DE7-A567-B83269BFE43F</RequestId>
	  <RegionId>cn-hangzhou</RegionId>
	  <EnableEventLog>True</EnableEventLog>
    </ModifyActionEventPolicyResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RegionId":"cn-hangzhou",
	"RequestId":"BAC0952C-0EB3-4DE7-A567-B83269BFE43F",
	"EnableEventLog":"True"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

