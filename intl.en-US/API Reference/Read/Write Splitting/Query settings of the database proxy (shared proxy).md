# Query settings of the database proxy \(shared proxy\)

Queries settings of the database proxy for an ApsaraDB for RDS instance.

**Note:** This operation queries settings of the shared database proxy, rather than the dedicated proxy. To query the dedicated proxy, see [DescribeDBProxy](~~141055~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceProxyConfiguration&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceProxyConfiguration|The operation that you want to perform. Set the value to **DescribeDBInstanceProxyConfiguration**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx|The ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AttacksProtectionConfiguration|String|\{\\"check\_interval\_seconds\\":\\"0\\",\\"max\_failed\_login\_attempts\\":\\"0\\",\\"blocking\_seconds\\":\\"0\\",\\"status\\":\\"Disable\\"\}|Indicates whether protection against brute-force attacks is enabled:

-   **Enable**
-   **Disable**

The returned value is a JSON string. Example:

\{"status":"Disable", "check\_interval\_seconds": 60,

"max\_failed\_login\_attempts": 60, "blocking\_seconds": 600\}

Description:

-   Each client allows \{max\_failed\_login\_attempts\} logon failure attempts within \{check\_interval\_seconds\} seconds. If one more such attempt is conducted, the client will have to wait for \{blocking\_seconds\} seconds to try again.
-   Valid values:
    -   check\_interval\_seconds: **30 to 600**. Unit: seconds.
    -   max\_failed\_login\_attempts: **10 to 5000**. Unit: times.
    -   blocking\_seconds: **30 to 3600**. Unit: seconds. |
|PersistentConnectionsConfiguration|String|\{\\"status\\":\\"Disable\\"\}|Indicates whether connection optimization is enabled.

-   **Enable**
-   **Disable**

The returned value is a JSON string. Example:

\{"status":"Disable"\}. |
|TransparentSwitchConfiguration|String|\{\\"status\\":\\"Enable\\"\}|Indicates whether transparent switchover is enabled.

-   **Enable**
-   **Disable**

The returned value is a JSON string. Example:

\{"status":"Enable"\}. |
|RequestId|String|E9DD55F4-1A5F-48CA-BA57-DFB3CA8C4C34|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDBInstanceProxyConfigurationResponse>
      <PersistentConnectionsConfiguration>{"status":"Disable"}</PersistentConnectionsConfiguration>
      <TransparentSwitchConfiguration>{"status":"Enable"}</TransparentSwitchConfiguration>
      <AttacksProtectionConfiguration>{"check_interval_seconds":"0","max_failed_login_attempts":"0","blocking_seconds":"0","status":"Disable"}</AttacksProtectionConfiguration>
      <RequestId>E9DD55F4-1A5F-48CA-BA57-DFB3CA8C4C34</RequestId>
</DescribeDBInstanceProxyConfigurationResponse>
```

`JSON` format

```
{
    "PersistentConnectionsConfiguration": "{\"status\":\"Disable\"}", 
    "TransparentSwitchConfiguration": "{\"status\":\"Enable\"}", 
    "AttacksProtectionConfiguration": "{\"check_interval_seconds\":\"0\",\"max_failed_login_attempts\":\"0\",\"blocking_seconds\":\"0\",\"status\":\"Disable\"}", 
    "RequestId": "E9DD55F4-1A5F-48CA-BA57-DFB3CA8C4C34"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

