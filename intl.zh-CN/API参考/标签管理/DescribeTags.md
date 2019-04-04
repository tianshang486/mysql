# DescribeTags {#doc_api_Rds_DescribeTags .reference}

调用DescribeTags接口查询RDS实例的标签。

调用本接口时限制条件如下：

-   如果传入指定实例ID，则查询该实例下所有标签，其他过滤条件失效；
-   若查询标签时仅传入标签键（TagKey），未传入标签值（TagValue），则返回所有符合标签键条件的结果。若同时传入标签键和标签值，则返回两个条件都符合的结果。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeTags)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeTags|系统规定参数，取值：**DescribeTags**。

 |
|RegionId|String|是|cn-hangzhou|地域ID，长度不超过50个字符，可以通过接口[DescribeRegions](~~26243~~)查看可用的地域ID。

 |
|DBInstanceId|String|否|rm-uf6wjk5xxxxxxx|实例ID。

 **说明：** 传入该参数，其他过滤条件失效。

 |
|Tags|String|否|\{“key1”:”value1”\}|需要查询的标签，包括TagKey和TagValue。格式：\{“key1”:”value1”\}。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Items| | |由Tag信息组成的数组。

 |
|└TagKey|String|key1|标签键。

 |
|└TagValue|String|value1|标签值。

 |
|└DBInstanceIds| |rm-uf6wjk5xxxxxxx|该标签所绑定的实例ID。

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeTags
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeTagsResponse>
  <Items>
    <TagInfos>
      <TagValue>1</TagValue>
      <TagKey>测试</TagKey>
      <DBInstanceIds>
        <DBInstanceIds>rm-uf6wjk5xxxxxxx</DBInstanceIds>
      </DBInstanceIds>
    </TagInfos>
  </Items>
  <RequestId>6D709088-6D7D-4152-99F4-C2FE86463862</RequestId>
</DescribeTagsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"TagInfos":[
			{
				"TagValue":"1",
				"TagKey":"测试",
				"DBInstanceIds":{
					"DBInstanceIds":[
						"rm-uf6wjk5xxxxxxx"
					]
				}
			}
		]
	},
	"RequestId":"6D709088-6D7D-4152-99F4-C2FE86463862"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Tag.NoRegionIdExist|the region Id can not be blank.|RegionId不能为空。创建，续费，变配的时候region不能为空。|
|400|Tag.NoTagInfoExist|all the tags and tagN parameters is null.|Tag参数无效。|
|400|Tag.TagKeyCanNotBeAll|tag key can not be all.|TagKey无效。|
|400|Tag.TagKeyDuplex|tag key must be sole in one operation.|标签键必须是唯一的。|
|400|Tag.NoDBInstanceIdExist|the dbinstance Id can not be blank.|实例Id是必传参数。续费，变配的时候，实例Id不能为空。|
|400|Tag.TooManyDBInstanceIds|the dbinstance Ids is more than 30.|实例Id的最多为30个。|
|400|Tag.TooManyTagsForOneInstance|total 10 tags can be added to one resource.|一个资源最多可以添加10个tag，请您不要超量添加。|
|400|Tag.SetTagInfoAtTwoParamters|only tags or tagN parameter could be setted.|你的tag参数设置取消。|
|400|Tag.Allow5TagInfos|only 5 tags allowed in one operation.|在一次操作中最多可以使用5个标记。|
|400|Tag.TagKeyIsBlank|tag key can not be blank.|标签键不能为空。|
|400|Tag.TagKeyStartWith.aliyun|tag key and value can not be started with aliyun.|TagKeyStartWith无效。|
|400|Tag.TagKeyTooLong|the max tag key's length is 64.|标签键的长度不能超过64。|
|400|Tag.TagValueTooLong|the max tag value's length is 128.|标签值的长度不能超过128。|
|400|Tag.InvalidTagsParamter|tags paramter is invalid.|标签参数无效。|
|404|InvalidDBInstanceId.NotFound|The DBInstanceId provided does not exist in our records.|实例不存在。确认该实例是在当前账号下面，确定未被删除。|
|400|Tag.Malformed|The specified parameter Tag is not valid.|Tag无效|
|400|Tag.Malformed|The specified parameter Value is not valid.|TagValue无效|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

