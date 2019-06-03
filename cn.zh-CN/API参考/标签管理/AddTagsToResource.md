# AddTagsToResource {#doc_api_Rds_AddTagsToResource .reference}

调用AddTagsToResource接口为实例绑定标签。

为实例绑定已有的或新创建的标签，限制如下：

-   每个标签（Tag）由标签键（TagKey）和标签值（TagValue）组成，TagKey不能为空，TagValue可以为空；
-   TagKey和TagValue的值不允许以aliyun开头；
-   TagKey和TagValue不区分大小写；
-   TagKey最长为64个字符，TagValue最长为128个字符；
-   每个实例最多绑定10个Tag，每个实例绑定的TagKey不能重复。若绑定带有重复TagKey的Tag，则后绑定的Tag将覆盖之前的Tag。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=AddTagsToResource)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AddTagsToResource|系统规定参数，取值：**AddTagsToResource**。

 |
|RegionId|String|是|cn-hagnzhou|地域ID，可以通过接口[DescribeRegions](~~26243~~)查看可用的地域ID。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 **说明：** 支持传入最多30个实例ID进行批量操作，用英文逗号（,）隔开。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|Tags|String|否|\{“key1”:”value1”,“key2”:””\}|需要绑定的Tag列表，包括TagKey和TagValue。单次最多支持传入5组值，格式：\{"key1":"value1","key2":"value2"...\}。

 **说明：** TagKey不能为空，TagValue可以为空。

 |
|Tag.1.key|String|否|key1|当前第一组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.2.key|String|否|key2|当前第二组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.3.key|String|否|key3|当前第三组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.4.key|String|否|key4|当前第四组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.5.key|String|否|key5|当前第五组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.1.value|String|否|value1|当前第一组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.2.value|String|否|value2|当前第二组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.3.value|String|否|value3|当前第三组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.4.value|String|否|value4|当前第四组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.5.value|String|否|value5|当前第五组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|224DB9F7-3100-4899-AB9C-C938BCCB43E7|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=AddTagsToResource
&RegionId=cn-hagnzhou
&DBInstanceId=rm-uf6wjk5xxxxxxx
&Tags=%7B%22test%22%3A%221%22%7D
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AddTagsToResourceResponse>
  <requestId>224DB9F7-3100-4899-AB9C-C938BCCB43E7</requestId>
</AddTagsToResourceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"224DB9F7-3100-4899-AB9C-C938BCCB43E7"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

