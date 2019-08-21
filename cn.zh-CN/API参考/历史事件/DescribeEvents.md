# DescribeEvents {#doc_api_Rds_DescribeEvents .reference}

调用DescribeEvents接口查询RDS事件记录列表。

RDS提供历史事件功能，开启后您可以所处地域内查看某时间段的历史事件，例如在某个时间创建了实例、修改了参数等等。详情请参见[历史事件](~~129759~~)。

调用该接口时，实例必须已开启历史事件功能，否则将操作失败。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DescribeEvents&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeEvents|系统规定参数，取值：**DescribeEvents**。

 |
|RegionId|String|是|cn-hangzhou|地域ID，可以通过接口[DescribeRegions](~~26243~~)查看地域ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|StartTime|String|否|2019-06-11T15:00:00Z|查询开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|EndTime|String|否|2019-06-12T15:00:00Z|查询结束时间，需要晚于开始时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|PageSize|Integer|否|30|每页记录数，取值：

 -   **30**；
-   **50**；
-   **100**。

 默认值：**30**。

 |
|PageNumber|Integer|否|1|页码，取值：大于0且不超过Integer的最大值。

 默认值：**1**。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|EventItems| | |事件列表。

 |
|EventId|Integer|11000053|事件ID。

 |
|EventName|String|ModifySecurityIPList|事件名称。

 |
|EventPayload|String|\{\\"Domain\\": \\"rds-inc-share.aliyuncs.com\\", \\"Api\\": \\"ReleaseInstancePublicConnection\\"\}|事件的请求参数或上下文参数。

 |
|EventReason|String|FROM\_USER|事件操作的来源。

 |
|EventRecordTime|String|2019-08-20T01:12:49Z|事件的记录时间。会稍晚于事件的发生时间。

 |
|EventTime|String|2019-08-20T01:08:22Z|事件发生时间。

 |
|EventType|String|NetworkManagement|事件类型。

 |
|EventUserType|String|SYSTEM|执行事件的用户类型。

 |
|RegionId|String|cn-hangzhou|地域ID。

 |
|ResourceName|String|rm-bp1z3065m9976ix8a|事件关联资源名称。当前仅有实例ID。

 |
|ResourceType|String|instance|事件关联资源类型。当前仅有实例。

 |
|PageNumber|Integer|1|页码。

 |
|PageSize|Integer|30|每页记录数。

 |
|RequestId|String|A103039D-B1B2-4C57-B989-7D7C0DA95426|请求ID。

 |
|TotalRecordCount|Integer|40|总记录数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeEvents
&Region=cn-hangzhou
&StartTime=2019-08-20T01:30:00Z
&EndTime=2019-08-20T01:35:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeEventsResponse>
  <EventItems>
		    <EventItems>
			      <EventName>ModifySecurityIPList</EventName>
			      <EventUserType>SYSTEM</EventUserType>
			      <ResourceType>instance</ResourceType>
			      <EventPayload></EventPayload>
			      <EventTime>2019-08-20T01:33:43Z</EventTime>
			      <RegionId>cn-hangzhou</RegionId>
			      <EventRecordTime>2019-08-20T01:33:57Z</EventRecordTime>
			      <EventReason>FROM_SYSTEM</EventReason>
			      <EventId>11000048</EventId>
			      <ResourceName>rm-bpxxxxxxx</ResourceName>
			      <EventType>SecurityManagement</EventType>
		    </EventItems>
		    <EventItems>
			      <EventName>ModifySecurityIPList</EventName>
			      <EventUserType>SYSTEM</EventUserType>
			      <ResourceType>instance</ResourceType>
			      <EventPayload></EventPayload>
			      <EventTime>2019-08-20T01:33:43Z</EventTime>
			      <RegionId>cn-hangzhou</RegionId>
			      <EventRecordTime>2019-08-20T01:33:57Z</EventRecordTime>
			      <EventReason>FROM_SYSTEM</EventReason>
			      <EventId>11000047</EventId>
			      <ResourceName>rm-bpxxxxxxx</ResourceName>
			      <EventType>SecurityManagement</EventType>
		    </EventItems>
	  </EventItems>
	  <TotalRecordCount>2</TotalRecordCount>
	  <PageNumber>1</PageNumber>
	  <PageSize>2</PageSize>
	  <RequestId>B5FF9EE6-830E-4DBE-8498-9890A62D2875</RequestId>
</DescribeEventsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"EventItems":{
		"EventItems":[
			{
				"EventName":"ModifySecurityIPList",
				"EventUserType":"SYSTEM",
				"ResourceType":"instance",
				"EventPayload":"",
				"EventTime":"2019-08-20T01:33:43Z",
				"RegionId":"cn-hangzhou",
				"EventRecordTime":"2019-08-20T01:33:57Z",
				"EventId":11000048,
				"EventReason":"FROM_SYSTEM",
				"ResourceName":"rm-bpxxxxxxx",
				"EventType":"SecurityManagement"
			},
			{
				"EventName":"ModifySecurityIPList",
				"EventUserType":"SYSTEM",
				"ResourceType":"instance",
				"EventPayload":"",
				"EventTime":"2019-08-20T01:33:43Z",
				"RegionId":"cn-hangzhou",
				"EventRecordTime":"2019-08-20T01:33:57Z",
				"EventId":11000047,
				"EventReason":"FROM_SYSTEM",
				"ResourceName":"rm-bpxxxxxxx",
				"EventType":"SecurityManagement"
			}
		]
	},
	"PageNumber":1,
	"TotalRecordCount":2,
	"PageSize":2,
	"RequestId":"B5FF9EE6-830E-4DBE-8498-9890A62D2875"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidStartTime.Format|Specified start time is not valid.|指定的起始时间无效。|

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

