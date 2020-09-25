# DescribeTags

调用DescribeTags接口查询RDS实例的标签。

调用本接口时限制条件如下：

-   如果传入指定实例ID，则查询该实例下所有标签，其他过滤条件失效；
-   若查询标签时仅传入标签键（TagKey），未传入标签值（TagValue），则返回所有符合标签键条件的结果。若同时传入标签键和标签值，则返回两个条件都符合的结果。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DescribeTags&type=RPC&version=2014-08-15)

## 请求参数

|名称|位置|类型|是否必选|示例值|描述|
|--|--|--|----|---|--|
|Action|Query|String|是|DescribeTags|系统规定参数，取值：**DescribeTags**。 |
|RegionId|Query|String|是|cn-hangzhou|地域ID，可以通过接口[DescribeRegions](~~26243~~)查看可用的地域ID。 |
|DBInstanceId|Query|String|否|rm-uf6wjk5xxxxxxx|实例ID。

 **说明：** 传入该参数，其他过滤条件失效。 |
|Tags|Query|String|否|\{“key1”:”value1”\}|需要查询的标签，包括TagKey和TagValue。格式：\{“key1”:”value1”\}。 |
|ClientToken|Query|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。 |
|proxyId|Query|String|否|API|代理模式ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Items|Array of TagInfos| |由Tag信息组成的数组。 |
|TagInfos| | | |
|TagKey|String|key1|标签键。 |
|TagValue|String|value1|标签值。 |
|DBInstanceIds|List|rm-uf6wjk5xxxxxxx|该标签所绑定的实例ID。 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。 |

## 示例

请求示例

```
http(s)://rds.aliyuncs.com/?Action=DescribeTags
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
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

```
{
    "Items": {
        "TagInfos": [
            {
                "TagValue": "1",
                "TagKey": "测试",
                "DBInstanceIds": {
                    "DBInstanceIds": [
                        "rm-uf6wjk5xxxxxxx"
                    ]
                }
            }
        ]
    },
    "RequestId": "6D709088-6D7D-4152-99F4-C2FE86463862"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Tag.NoRegionIdExist|the region Id can not be blank.|RegionId不能为空。创建，续费，变配的时候region不能为空。|
|400|Tag.NoTagInfoExist|all the tags and tagN parameters is null.|Tag参数无效。|
|400|Tag.TagKeyCanNotBeAll|tag key can not be all.|TagKey无效。|
|400|Tag.TagKeyDuplex|tag key must be sole in one operation.|标签键必须是唯一的。|
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

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。

