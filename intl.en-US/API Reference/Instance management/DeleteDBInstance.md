# DeleteDBInstance {#doc_api_Rds_DeleteDBInstance .reference}

You can call this operation to release an RDS instance.

When you perform this operation, the instance must meet the following requirements:

-   The instance is in the running state.
-   The read/write splitting function is disabled for the instance.
-   The instance is a Pay-As-You-Go master instance, read-only instance, disaster recovery instance, or temporary instance.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DeleteDBInstance) to perform debugging.

API Explorer provides various functions to simplify API usage. For example, you can search APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteDBInstance| The operation that you want to perform. Set this parameter to DeleteDBInstance.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx| The ID of the instance.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DeleteDBInstance
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<Common request parameters>
```

Normal response examples

`XML` format

``` {#codeblock_byd_khg_k1r}
<DeleteDBInstanceResponse>
	  <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId></DeleteDBInstanceResponse>
```

`JSON` format

``` {#codeblock_sp0_8e9_5mn}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## Error codes {#section_5lj_bdh_8jx .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

