# Query settings of automatic primary/secondary switchover

Queries the status of the automatic primary/secondary switchover function for an ApsaraDB for RDS instance.

After a primary/secondary switchover, the primary instance is demoted to secondary while the secondary instance is promoted to primary. For more information, see [Manually or automatically switch over services between the RDS MySQL master and slave instances](~~96054~~).

Before you call this operation, make sure the instance runs the High-availability Edition, Enterprise Edition, or Cluster Edition.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeHASwitchConfig&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeHASwitchConfig|The operation that you want to perform. Set the value to **DescribeHASwitchConfig**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx|The ID of the instance. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region to which the instance belongs. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|HAConfig|String|Manual|The status of the automatic primary/secondary switchover function. Valid values:

-   **Auto:** The automatic primary/secondary switchover function is enabled. The system automatically switches over services from the primary to secondary instances in the event of a fault.
-   **Manual:** The automatic primary/secondary switchover function is temporarily disabled. |
|ManualHATime|String|2019-08-29T15:00:00Z|The time when at which the automatic primary/secondary switchover function is enabled again. |
|RequestId|String|4FDF4B79-2741-4C5F-8C76-4B953FC5C2B1|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeHASwitchConfig
&RegionId=cn-hangzhou
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeHASwitchConfigResponse>
   <ManualHATime>2019-08-29T15:00:00Z</ManualHATime>
   <RequestId>4FDF4B79-2741-4C5F-8C76-4B953FC5C2B1</RequestId>
   <HAConfig>Manual</HAConfig>
</DescribeHASwitchConfigResponse>
```

`JSON` format

```
{
    "ManualHATime": "2019-08-29T15:00:00Z",
    "RequestId": "4FDF4B79-2741-4C5F-8C76-4B953FC5C2B1",
    "HAConfig": "Manual"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

