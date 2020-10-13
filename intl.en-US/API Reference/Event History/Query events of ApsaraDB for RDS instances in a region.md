# Query events of ApsaraDB for RDS instances in a region

Queries events of ApsaraDB for RDS instances in a region.

The event history feature enables you to view the events that occurred in a region over a specific time range. The events include instance creation and parameter reconfiguration. For more information, see [Event history](~~129759~~).

Before you call this operation, make sure that the event history feature is enabled. Otherwise, this operation fails.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeEvents&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeEvents|The operation that you want to perform. Set the value to **DescribeEvents**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|StartTime|String|No|2019-06-11T15:00:00Z|The start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|EndTime|String|No|2019-06-12T15:00:00Z|The end time. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values:

 -   **30**
-   **50**
-   **100**

 Default value: **30**. |
|PageNumber|Integer|No|1|The number of the page to return. Valid values: a non-zero positive integer.

 Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|EventItems|Array of EventItems| |The list of events. |
|EventItems| | | |
|EventId|Integer|11000053|The ID of an event. |
|EventName|String|ModifySecurityIPList|The name of an event. For more information, see [Event history](~~129759~~). |
|EventPayload|String|\{\\"Domain\\": \\"rds-inc-share.aliyuncs.com\\", \\"Api\\": \\"ReleaseInstancePublicConnection\\"\}|The request or context parameters of an event. |
|EventReason|String|FROM\_USER|The source of an event. For more information, see [Event history](~~129759~~). |
|EventRecordTime|String|2019-08-20T01:12:49Z|The time when an event was recorded. The time is slightly later than the time the event occurred. |
|EventTime|String|2019-08-20T01:08:22Z|The time when an event occurred. |
|EventType|String|NetworkManagement|The type of an event. For more information, see [Event history](~~129759~~). |
|EventUserType|String|SYSTEM|The type of the user who executed the event. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|ResourceName|String|rm-bp1z3065m9976ix8a|The name of the resource associated with an event. Only instance IDs are supported for this parameter. |
|ResourceType|String|instance|The type of the resource associated with an event. Only instances are supported for this parameter. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|30|The number of entries returned per page. |
|RequestId|String|A103039D-B1B2-4C57-B989-7D7C0DA95426|The ID of the request. |
|TotalRecordCount|Integer|40|The total number of records returned. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeEvents
&Region=cn-hangzhou
&StartTime=2019-08-20T01:30:00Z
&EndTime=2019-08-20T01:35:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
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

`JSON` format

```
{
	"EventItems": {
		"EventItems": [
			{
				"EventName": "ModifySecurityIPList",
				"EventUserType": "SYSTEM",
				"ResourceType": "instance",
				"EventPayload": "",
				"EventTime": "2019-08-20T01:33:43Z",
				"RegionId": "cn-hangzhou",
				"EventRecordTime": "2019-08-20T01:33:57Z",
				"EventReason": "FROM_SYSTEM",
				"EventId": 11000048,
				"ResourceName": "rm-bpxxxxxxx",
				"EventType": "SecurityManagement"
			},
			{
				"EventName": "ModifySecurityIPList",
				"EventUserType": "SYSTEM",
				"ResourceType": "instance",
				"EventPayload": "",
				"EventTime": "2019-08-20T01:33:43Z",
				"RegionId": "cn-hangzhou",
				"EventRecordTime": "2019-08-20T01:33:57Z",
				"EventReason": "FROM_SYSTEM",
				"EventId": 11000047,
				"ResourceName": "rm-bpxxxxxxx",
				"EventType": "SecurityManagement"
			}
		]
	},
	"TotalRecordCount": 2,
	"PageNumber": 1,
	"PageSize": 2,
	"RequestId": "B5FF9EE6-830E-4DBE-8498-9890A62D2875"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|400|InvalidStartTime.Format|Specified start time is not valid.|The error message returned because the specified start time is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

