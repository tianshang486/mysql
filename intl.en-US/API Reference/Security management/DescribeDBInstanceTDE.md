# DescribeDBInstanceTDE {#doc_api_1066900 .reference}

You can call this operation to query the data encryption status of an instance.

This operation is used to view the [TDE](../../../../intl.en-US/User Guide/Security/Set TDE.md#) configuration of an instance.

**Note:** This operation is applicable only to MySQL 5.6 and SQL Server Enterprise Edition instances.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceTDE) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceTDE| The operation that you want to perform. Set this parameter to DescribeDBInstanceTDE.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|TDEStatus|String|Enabled| The TDE status at the instance level. Valid values: Enable | Disable.

 |
|Databases|N/A|N/A| The TDE status list at the database level.

 **Note:** For SQL Server Enterprise Edition instances, you can enable or disable TDE at the database level when TDE is enabled at the instance level.

 |
|DBName|String|test02| The name of the database.

 |
|TDEStatus|String|Enabled| The TDE status at the database level. Valid values: Enable | Disable.

 |
|RequestId|String|C816A4BF-A6EC-4722-95F9-2055859CCFD2| The ID of the instance.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeDBInstanceTDE
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_9e1_bgf_o66}
<DescribeDBInstanceTDEResponse>
	  <TDEStatus>Enabled</TDEStatus>
	  <Databases>
		    <DBName>test02</DBName>
		    <TDEStatus>Enabled</TDEStatus>
	  </Databases>
	  <requestId>C816A4BF-A6EC-4722-95F9-2055859CCFD2</requestId>
</DescribeDBInstanceTDEResponse>
```

`JSON` format

``` {#codeblock_a2p_gy2_qgv}
{
	"Databases":[
		{
			"TDEStatus":"Enabled",
			"DBName":"test02"
		}
	],
	"requestId":"C816A4BF-A6EC-4722-95F9-2055859CCFD2",
	"TDEStatus":"Enabled"
}
```

## Error codes {#section_nlc_lb2_jg8 .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

