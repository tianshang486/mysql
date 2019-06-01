# ReleaseReadWriteSplittingConnection {#doc_api_1064557 .reference}

You can call this operation to release the read/write splitting address of an RDS instance.

This operation is applicable to the following instances:

-   MySQL 5.7 High-availability Edition \(based on local SSDs\)
-   MySQL 5.6
-   SQL Server 2017 Cluster Edition

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=ReleaseReadWriteSplittingConnection) to perform debugging.

API Explorer provides various functions to simplify API usage. For example, you can search APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ReleaseReadWriteSplittingConnection| The operation that you want to perform. Set the value to **ReleaseReadWriteSplittingConnection**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the master instance.

 |

## Response parameter {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|5A77D650-27A1-4E08-AD9E-59008EDB6927| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ReleaseReadWriteSplittingConnection
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Normal response example

`XML` format

``` {#xml_return_success_demo}
<ReleaseReadWriteSplittingConnectionResponse>
  <RequestID>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestID>
</ReleaseReadWriteSplittingConnectionResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestID":"5A77D650-27A1-4E08-AD9E-59008EDB6927"
}
```

## Error codes {#section_du7_086_bey .section}

[View error codes](https://error-center.alibabacloud.com/status/product/Rds)

