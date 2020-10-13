# Unbind tags

Unbinds tags from an ApsaraDB for RDS instance.

**Note:**

-   You can unbind up to 20 tags at a time.
-   If a tag is unbound from an instance and is not bound to other instances, the tag is deleted.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=UntagResources&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UntagResources|The operation that you want to perform. Set the value to **UntagResources**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|ResourceId.N|RepeatList|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. You can bind tags to N instances at a time. Valid values of N: **1** to **50**. |
|ResourceType|String|Yes|INSTANCE|The type of the resource. Set the value to **INSTANCE**. |
|All|Boolean|No|false|Specifies whether to delete all tags of the instance. Valid values:

 -   **true**
-   **false**

 Default value: **false**.

 **Note:** This parameter is valid when **TagKey.N** is not specified. |
|TagKey.N|RepeatList|No|testkey1|The key of the tag. You can delete N keys at a time. Valid values of N: **1** to **20**. The tag key cannot be left empty. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|601B6F25-21E7-4484-99D5-3EF2625C0088|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=UntagResources
&RegionId=cn-hangzhou
&ResourceType=INSTANCE
&ResourceId.1=rm-uf6wjk5xxxxxxx
&TagKey.1=testkey1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UntagResourcesResponse>
        <RequestId>601B6F25-21E7-4484-99D5-3EF2625C0088</RequestId>
</UntagResourcesResponse>
```

`JSON` format

```
{
	"RequestId":"601B6F25-21E7-4484-99D5-3EF2625C0088"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

