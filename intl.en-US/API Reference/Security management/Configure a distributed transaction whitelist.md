# Configure a distributed transaction whitelist

Configures a distributed transaction whitelist for an ApsaraDB for RDS instance.

Distributed transaction whitelists allow for distributed transactions between an Elastic Compute Service \(ECS\) instance and an RDS instance. For more information, see [Configure a distributed transaction whitelist](~~124321~~).

This operation is applicable to instances that run one of the following SQL Server versions in the RDS High-Availability Edition: 2012 SE, 2012 EE, 2014 SE, 2016 SE, 2016 EE, and 2017 SE.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyDTCSecurityIpHostsForSQLServer&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDTCSecurityIpHostsForSQLServer|The operation that you want to perform. Set the value to **ModifyDTCSecurityIpHostsForSQLServer**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|SecurityIpHosts|String|Yes|192.168.1.100,k3ecstest|The IP address of the ECS instance and the hostname of the Windows computer. Format: IP address,Hostname. Multiple values are separated with semicolons \(;\).

**Note:** For more information about how to query the computer hostname, see [Configure a distributed transaction whitelist](~~124321~~). |
|WhiteListGroupName|String|Yes|test1|The name of the whitelist. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|DTCSetResult|String|Success|The result of the whitelist configuration. Valid values:

-   **Success**
-   **Fail** |
|RequestId|String|671B6D32-B907-4EFF-A3B7-94D2EAD5E3A3|The ID of the request. |
|TaskId|String|178968983|The ID of the task. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyDTCSecurityIpHostsForSQLServer
&DBInstanceId=rm-uf6wjk5xxxxxxx
&RegionId=cn-hangzhou
&SecurityIpHosts=192.168.1.100,k3ecstest
&WhiteListGroupName=test1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDTCSecurityIpHostsForSQLServerResponse>
  <RequestId>671B6D32-B907-4EFF-A3B7-94D2EAD5E3A3</RequestId>
      <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
      <DTCSetResult>Success</DTCSetResult>
      <TaskId>178968983</TaskId>
</ModifyDTCSecurityIpHostsForSQLServerResponse>
```

`JSON` format

```
{
    "RequestId": "671B6D32-B907-4EFF-A3B7-94D2EAD5E3A3",
    "DBInstanceId": "rm-uf6wjk5xxxxxxx",
    "DTCSetResult": "Success",
    "TaskId": 178968983
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

