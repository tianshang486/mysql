# ModifySQLCollectorPolicy {#doc_api_Rds_ModifySQLCollectorPolicy .reference}

You can call this operation to enable or disable the SQL audit feature of an instance.

This operation is applicable to the following instances:

-   MySQL 5.5
-   MySQL 5.6
-   MySQL 5.7 High-availability Edition \(based on local SSDs\)
-   SQL Server 2008 R2
-   PostgreSQL
-   PPAS

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=ModifySQLCollectorPolicy) to perform debugging.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifySQLCollectorPolicy| The operation that you want to perform. Set the value to **ModifySQLCollectorPolicy**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the instance.

 |
|SQLCollectorStatus|String|Yes|Enable| Indicates whether to enable or disable the SQL audit feature. Valid values: **Enable | Disable**.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifySQLCollectorPolicy
&DBInstanceId=rm-uf6wjk5xxxxxxx
&SQLCollectorStatus=Enable 
&<Common request parameters>
```

Normal response example

`XML` format

``` {#xml_return_success_demo}
<ModifySQLCollectorPolicyResponse> 
  <requestId>C3565F9F-76E9-4F7E-A662-D1B2488EC2FC</requestId>
  <sQLCollectorStatus>Enable</sQLCollectorStatus>
</ModifySQLCollectorPolicyResponse> 
```

`JSON` format

``` {#json_return_success_demo}
{
	"requestId":"C3565F9F-76E9-4F7E-A662-D1B2488EC2FC",
	"sQLCollectorStatus":"Enable"
}
```

