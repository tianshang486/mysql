# RemoveTagsFromResource {#doc_api_Rds_RemoveTagsFromResource .reference}

调用RemoveTagsFromResource接口解绑标签。

限制条件如下：

-   单次最多支持解绑10个标签；
-   若一个标签所绑定的实例全都解绑，则该标签自动删除；
-   若解绑标签时仅传入标签键（TagKey），未传入标签值（TagValue），则解绑所有符合标签键条件的标签。
-   必须传入至少一组标签或者单独的一个标签键。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=RemoveTagsFromResource&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RemoveTagsFromResource|系统规定参数，取值：**RemoveTagsFromResource**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|RegionId|String|是|cn-hangzhou|地域ID，可以通过接口[DescribeRegions](~~26243~~)查看可用的地域ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|Tag.1.key|String|否|key1|要解绑的第一组标签的Tagkey。需要解绑的标签，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.1.value|String|否|value1|要解绑的第一组标签的TagValue。需要解绑的标签，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.2.key|String|否|key2|要解绑的第二组标签的Tagkey。需要解绑的标签，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.2.value|String|否|value2|要解绑的第二组标签的TagValue。需要解绑的标签，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.3.key|String|否|key3|要解绑的第三组标签的Tagkey。需要解绑的标签，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.3.value|String|否|value4|要解绑的第三组标签的TagValue。需要解绑的标签，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.4.key|String|否|key4|要解绑的第四组标签的Tagkey。需要解绑的标签，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.4.value|String|否|value4|要解绑的第四组标签的TagValue。需要解绑的标签，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.5.key|String|否|key5|要解绑的第五组标签的Tagkey。需要解绑的标签，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.5.value|String|否|value5|要解绑的第五组标签的TagValue。需要解绑的标签，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tags|String|否|\{"key1":"value1"\}|需要解绑的一组标签，包括TagKey和TagValue。格式：\{"key1":"value1"\}。

 **说明：** TagKey不能为空，TagValue可以为空。

 |
|proxyId|String|否|API|代理模式ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|AE00ACCD-1CF9-4920-9BB9-0175EFF43405|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=RemoveTagsFromResource
&DBInstanceId=rm-uf6wjk5xxxxxxx
&RegionId=cn-hangzhou
&Tag.1.key=test
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RemoveTagsFromResourceResponse>
	  <requestId>AE00ACCD-1CF9-4920-9BB9-0175EFF43405</requestId></RemoveTagsFromResourceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"AE00ACCD-1CF9-4920-9BB9-0175EFF43405"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

