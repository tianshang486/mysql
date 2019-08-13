# DescribeDBInstanceIPArrayList {#doc_api_1066780 .reference}

You can call this operation to view the IP address whitelist of an RDS instance.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceIPArrayList) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceIPArrayList| The operation that you want to perform. Set this parameter to DescribeDBInstanceIPArrayList.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|WhitelistNetworkType|String|No|VPC| The network type of the whitelist. Valid values:

 -   Classic: classic networks in safe mode.
-   VPC: VPCs in safe mode.
-   Mix: normal whitelist mode.

 The whitelist IP addresses of all network types are returned by default.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Items|N/A|N/A| The array of the IP address whitelist.

 |
|DBInstanceIPArrayName|String|rds\_default| The name of the IP address whitelist.

 |
|DBInstanceIPArrayAttribute|String|hidden| The attribute of the whitelist group. It is empty by default.

 **Note:** The groups with hidden attribute are not displayed in the console. The groups with hidden attribute are used to access DTS and DRDS.

 |
|SecurityIPList|String|192.168.1.0/24| The IP addresses in an IP address whitelist. Up to 1,000 IP addresses can be returned. These addresses must be separated by commas \(,\).

 |
|SecurityIPType|String|IPv4| The type of the IP address.

 |
|RequestId|String|E2B6AF71-DC32-4055-B477-43B348798D10| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeDBInstanceIPArrayList
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_pk5_7k2_2c3}
<DescribeDBInstanceIPArrayListResponse>
	  <Items>
		    <DBInstanceIPArray>
			      <DBInstanceIPArrayName>rds_default</DBInstanceIPArrayName>
			      <DBInstanceIPArrayAttribute></DBInstanceIPArrayAttribute>
			      <WhitelistNetworkType>VPC</WhitelistNetworkType>
			      <SecurityIPList>192.168.1.0/24</SecurityIPList>
			      <SecurityIPType>IPv4</SecurityIPType>
		    </DBInstanceIPArray>
	  </Items>
	  <RequestId>E2B6AF71-DC32-4055-B477-43B348798D10</RequestId>
    </DescribeDBInstanceIPArrayListResponse>
```

`JSON` format

``` {#codeblock_s2k_shr_27j}
{
	"Items":{
		"DBInstanceIPArray":[
			{
				"DBInstanceIPArrayName":"rds_default",
				"DBInstanceIPArrayAttribute":"",
				"WhitelistNetworkType":"VPC",
				"SecurityIPType":"IPv4",
				"SecurityIPList":"192.168.1.0/24"
			}
		]
	},
	"RequestId":"E2B6AF71-DC32-4055-B477-43B348798D10"
}
```

## Error codes {#section_ess_ulv_8gl .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

