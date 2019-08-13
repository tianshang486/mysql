# SwitchDBInstanceHA {#doc_api_Rds_SwitchDBInstanceHA .reference}

You can call this operation to switch between the master and slave instances.

This operation switches between the master and slave instances for ApsaraDB for RDS High-Availability Edition. After switching, the slave instance becomes master and carries all business traffic.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=SwitchDBInstanceHA) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SwitchDBInstanceHA| The operation that you want to perform. Set this parameter to SwitchDBInstanceHA.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx| The ID of the instance.

 |
|NodeId|String|Yes|349054| The unique ID of the slave instance. You can call the [DescribeDBInstanceHAConfig](intl.en-US/API Reference/Instance management/DescribeDBInstanceHAConfig.md#) API operation to view the ID of the slave instance.

 |
|Force|String|No|No| Indicates whether to turn on the forcible switch. Valid values:

 -   Yes
-   No

 Default value: No

 |
|EffectiveTime|String|No|Immediate| The time when the switch takes effect. Valid values:

 -   Immediate: The switch takes effect immediately.
-   MaintainTime: The switch takes effect during the maintenance time.

 Default value: Immediate.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxxxxx| The AccessKey ID that Alibaba Cloud issues to a user for service access.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=SwitchDBInstanceHA
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&NodeId=349054
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_t6o_dpf_mz5}
<SwitchDBInstanceHAResponse>
	  <RequestId>1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC</RequestId></SwitchDBInstanceHAResponse>
```

`JSON` format

``` {#codeblock_dvt_nvv_d4r}
{
	"RequestId":"1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC"
}
```

## Error codes {#section_nrb_8uj_ihz .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

