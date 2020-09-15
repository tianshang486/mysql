# Query parameter configuration logs

Queries the parameter reconfiguration logs of an ApsaraDB for RDS instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeModifyParameterLog&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeModifyParameterLog|The operation that you want to perform. Set the value to **DescribeModifyParameterLog**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxx|The ID of the RDS instance. |
|StartTime|String|Yes|2020-03-01T00:00Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|EndTime|String|Yes|2020-03-01T10:00Z|The end of the time range to query. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values:

-   **30**
-   **50**
-   **100**

Default value: **30**. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxx|The ID of the RDS instance. |
|Engine|String|MySQL|The database engine that the RDS instance runs. |
|EngineVersion|String|5.6|The version of the database engine that the RDS instance runs. |
|Items|Array| |An array that consists of parameter reconfiguration log entries. |
|ParameterChangeLog| | | |
|ModifyTime|String|1584076066000|The time when the parameter was reconfigured. This value is a UNIX timestamp. Unit: milliseconds. |
|NewParameterValue|String|3|The new value of the parameter. |
|OldParameterValue|String|8|The original value of the parameter. |
|ParameterName|String|innodb\_stats\_sample\_pages|The name of the parameter. |
|Status|String|Syncing|The status of the new value specified for the parameter. Valid values:

-   **Applied:** The new value has taken effect.
-   **Syncing:** The new value is being applied and has not taken effect. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageRecordCount|Integer|1|The number of entries returned per page. |
|RequestId|String|C8E88DED-533F-4B3C-9207-731FBF394CCA|The ID of the request. |
|TotalRecordCount|Integer|1|The total number of entries returned. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeModifyParameterLog
&DBInstanceId=rm-uf6wjk5xxxxx
&StartTime=2020-03-01T00:00Z
&EndTime=2020-03-01T10:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeModifyParameterLogResponse>
  <EngineVersion>5.6</EngineVersion>
  <Engine>mysql</Engine>
  <RequestId>C8E88DED-533F-4B3C-9207-731FBF394CCA</RequestId>
  <DBInstanceId>rm-uf6wjk5xxxxx</DBInstanceId>
  <PageNumber>1</PageNumber>
  <PageRecordCount>1</PageRecordCount>
  <TotalRecordCount>1</TotalRecordCount>
  <Items>
        <ParameterChangeLog>
              <Status>Syncing</Status>
              <ModifyTime>1584076066000</ModifyTime>
              <NewParameterValue>3</NewParameterValue>
              <OldParameterValue>8</OldParameterValue>
              <ParameterName>innodb_stats_sample_pages</ParameterName>
        </ParameterChangeLog>
  </Items>
</DescribeModifyParameterLogResponse>
```

`JSON` format

```
{"EngineVersion":"5.6",
   "Engine":"mysql",
   "RequestId":"C8E88DED-533F-4B3C-9207-731FBF394CCA",
   "DBInstanceId":"rm-uf6wjk5xxxxx",
   "PageNumber":"1",
   "PageRecordCount":"1",
   "TotalRecordCount":"1",
   "Items":
    {"ParameterChangeLog":
      [{"Status":"Syncing",
        "ModifyTime":"1584076066000",
        "NewParameterValue":"3",
        "OldParameterValue":"8",
        "ParameterName":"innodb_stats_sample_pages"}]}
   }
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

