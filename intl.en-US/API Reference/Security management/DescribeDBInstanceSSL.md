# DescribeDBInstanceSSL {#doc_api_Rds_DescribeDBInstanceSSL .reference}

You can call this operation to query the SSL settings of an instance.

**Note:** This operation is applicable only to MySQL 5.6, MySQL 5.7/8.0 High-availability Edition \(based on local SSDs\), and all editions of SQL Server.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceSSL) to perform debugging. OpenAPI Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceSSL| The operation that you want to perform. Set this parameter to DescribeDBInstanceSSL.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID fo the instance.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ConnectionString|String|rm-uf6wjk5xxxxxx.mysql.rds.aliyuncs.com| The connection address protected by the SSL certificate.

 |
|SSLExpireTime|String|2018-01-17T12:18:15Z| The expiration time of the SSL certificate. The time is in the following UTC format: yyyy-MM-ddTHH:mm:ssZ.

 |
|RequireUpdate|String|Yes| Indicates whether the SSL certificate needs to be updated. Valid values: Yes | No.

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF| The ID of the request.

 |
|RequireUpdateReason|String|N/A| The reason why the SSL certificate needs to be updated.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://rds.aliyuncs.com/? Action=DescribeDBInstanceSSL
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#codeblock_534_h01_n4e}
<DescribeDBInstanceSSLResponse>
	  <items>
		    <ConnectionString>rm-uf6wjk5xxxxxx.mysql.rds.aliyuncs.com</ConnectionString>
		    <SSLExpireTime>2018-01-17T12:18:15Z</SSLExpireTime>
		    <RequireUpdate>Yes</RequireUpdate>
		    <RequireUpdateReason></RequireUpdateReason>
	  </items>
	  <requestId>1AD222E9-E606-4A42-BF6D-8A4442913CEF</requestId></DescribeDBInstanceSSLResponse>
```

`JSON` format

``` {#codeblock_fqt_hcv_azz}
{
	"requestId":"1AD222E9-E606-4A42-BF6D-8A4442913CEF",
	"items":[
		{
			"RequireUpdate":"Yes",
			"ConnectionString":"rm-uf6wjk5xxxxxx.mysql.rds.aliyuncs.com",
			"RequireUpdateReason":"",
			"SSLExpireTime":"2018-01-17T12:18:15Z"
		}
	]
}
```

## Error codes {#section_mkl_b6e_8n1 .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

