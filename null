# AddTagsToResource

调用AddTagsToResource接口为实例绑定标签。

为实例绑定已有的或新创建的标签，限制如下：

-   每个标签（Tag）由标签键（TagKey）和标签值（TagValue）组成，TagKey不能为空，TagValue可以为空；
-   TagKey和TagValue的值不允许以aliyun开头；
-   TagKey和TagValue不区分大小写；
-   TagKey最长为64个字符，TagValue最长为128个字符；
-   每个实例最多绑定10个Tag，每个实例绑定的TagKey不能重复。若绑定带有重复TagKey的Tag，则后绑定的Tag将覆盖之前的Tag。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=AddTagsToResource&type=RPC&version=2014-08-15)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AddTagsToResource|系统规定参数，取值：**AddTagsToResource**。 |
|RegionId|String|是|cn-hagnzhou|地域ID，可以通过接口[DescribeRegions](~~26243~~)查看可用的地域ID。 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 **说明：** 支持传入最多30个实例ID进行批量操作，用英文逗号（,）隔开。 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。 |
|Tags|String|否|\{“key1”:”value1”,“key2”:””\}|需要绑定的Tag列表，包括TagKey和TagValue。单次最多支持传入5组值，格式：\{"key1":"value1","key2":"value2"...\}。

 **说明：** TagKey不能为空，TagValue可以为空。 |
|Tag.1.key|String|否|key1|当前第一组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。 |
|Tag.2.key|String|否|key2|当前第二组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。 |
|Tag.3.key|String|否|key3|当前第三组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。 |
|Tag.4.key|String|否|key4|当前第四组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。 |
|Tag.5.key|String|否|key5|当前第五组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。 |
|Tag.1.value|String|否|value1|当前第一组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。 |
|Tag.2.value|String|否|value2|当前第二组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。 |
|Tag.3.value|String|否|value3|当前第三组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。 |
|Tag.4.value|String|否|value4|当前第四组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。 |
|Tag.5.value|String|否|value5|当前第五组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。 |
|proxyId|String|否|API|代理模式ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|224DB9F7-3100-4899-AB9C-C938BCCB43E7|请求ID。 |

## 示例

请求示例

```

http(s)://rds.aliyuncs.com/?Action=AddTagsToResource
&RegionId=cn-hagnzhou
&DBInstanceId=rm-uf6wjk5xxxxxxx
&Tags=%7B%22test%22%3A%221%22%7D
&<公共请求参数>

```

正常返回示例

`XML` 格式

```
<AddTagsToResourceResponse>
	  <requestId>224DB9F7-3100-4899-AB9C-C938BCCB43E7</requestId></AddTagsToResourceResponse>
```

`JSON` 格式

```
{
	"requestId":"224DB9F7-3100-4899-AB9C-C938BCCB43E7"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

