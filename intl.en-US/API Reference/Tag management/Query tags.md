# Query tags

Queries tags that are bound to one or more ApsaraDB for RDS instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ListTagResources&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTagResources|The operation that you want to perform. Set the value to **ListTagResources**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|ResourceType|String|Yes|INSTANCE|The type of the resource. Set the value to **INSTANCE**. |
|NextToken|String|No|212db86sca4384811e0b5e8707ec21345|The token required to retrieve more results. This parameter is not required in the first query. If a query does not return all results, you can enter this token in the next query to obtain more results. |
|ResourceId.N|RepeatList|No|rm-uf6wjk5xxxxxxx|The ID of the instance. You can query tags of N instances at a time. Valid values of N: **1** to **50**.

**Note:** You must specify at least one of the **ResourceId.N** and the **Tag.N.Key** parameters. |
|Tag.N.Key|String|No|testkey1|The key of the tag. You can query N keys at a time. Valid values of N: **1** to **20**. The tag key cannot be left empty.

**Note:** You must specify at least one of the **ResourceId.N** and the **Tag.N.Key** parameters. |
|Tag.N.Value|String|No|testvalue1|The value of the tag. You can query N values at a time. Valid values of N: **1** to **20**. The tag value can be left empty. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|212db86sca4384811e0b5e8707ec21345|The token required to obtain the next set of results. If not all results are returned in a query, you can provide the token returned from this query to obtain more results in the next query. |
|RequestId|String|47A514A1-4B77-4E30-B4C5-2A880650B3FD|The ID of the request. |
|TagResources|Array| |The information of the returned instances and tags. |
|TagResource| | | |
|ResourceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|ResourceType|String|ALIYUN::RDS::INSTANCE|The resource type. The value is `aliyun::rds:instance`, which indicates RDS instances. |
|TagKey|String|testkey1|The key of the tag. |
|TagValue|String|testvalue1|The value of the tag. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ListTagResources
&RegionId=cn-hangzhou
&ResourceType=INSTANCE
&ResourceId.1=rm-uf6wjk5xxxxxxx
&Tag.1.Key=testkey1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListTagResourcesResponse>
  <TagResources>
        <TagResource>
              <ResourceType>ALIYUN::RDS::INSTANCE</ResourceType>
              <TagValue>testvalue1</TagValue>
              <ResourceId>rm-uf6wjk5xxxxxxx</ResourceId>
              <TagKey>testkey1</TagKey>
        </TagResource>
  </TagResources>
  <RequestId>47A514A1-4B77-4E30-B4C5-2A880650B3FD</RequestId>
</ListTagResourcesResponse>
```

`JSON` format

```
{
    "TagResources":{
        "TagResource":[
            {
                "ResourceType":"ALIYUN::RDS::INSTANCE",
                "TagValue":"testvalue1",
                "ResourceId":"rm-uf6wjk5xxxxxxx",
                "TagKey":"testkey1"
            }
        ]
    },
    "RequestId":"47A514A1-4B77-4E30-B4C5-2A880650B3FD"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

