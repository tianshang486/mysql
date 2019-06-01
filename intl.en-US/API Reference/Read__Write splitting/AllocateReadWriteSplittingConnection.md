# AllocateReadWriteSplittingConnection {#doc_api_1064456 .reference}

You can call this operation to apply for the read-write splitting address.

For a master instance that has read-only instances, you can apply for the [read/write splitting address](~~51073~~). The read/write splitting address does not affect the existing connection addresses of the master instance and its read-only instances, nor does it affect your applying for the intranet and Internet addresses.

When you call this operation, the instance must meet the following requirements:

-   The instance is in the running state.
-   The instance has at least one read-only instance.
-   The instance does not have an ongoing migration task.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=AllocateReadWriteSplittingConnection) to perform debugging.

API Explorer provides various functions to simplify API usage. For example, you can search APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AllocateReadWriteSplittingConnection| The operation that you want to perform. Set the value to **AllocateReadWriteSplittingConnection**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the master instance.

 |
|ConnectionStringPrefix|String|否|rr-m5exxxxx-rw.mysql.rds.aliyuncs.com| The prefix of the read/write splitting address. It must be unique and start with a letter. It contains at most 30 characters, including lowercase letters or hyphens \(-\).

 **Note:** By default, the prefix is "instance name + rw".

 |
|Port|String|No|3306| The read/write splitting port. Valid values:

 -   MySQL: 3001 to 3999. Default value: 3306.
-   SQL Server: 1000 to 5999. Default value: 1433.

 |
|MaxDelayTime|String|No|30| The latency threshold. It ranges from 0 to 7,200. Default value: 30. Unit: seconds.

 **Note:** If a read-only instance reaches the latency threshold, read requests are no longer sent to the read-only instance.

 |
|NetType|String|No|Intranet| The network type of the read/write splitting address. Valid values:

 -   **Internet**.
-   **Intranet** \(default value\). The intranet type \(classic network or VPC\) is the same as the that of the master instance.

 |
|DistributionType|String|No|Standard| The mode of read weight distribution. Valid values:

 -   **Standard**: Read weights are distributed according to instance specifications.
-   **Custom**: Read weights are specified by you.

 |
|Weight|String|No|\{“Instanceid1“:”100”,”Instanceid2”:”200”\}| The read weight distribution. Enter the read weights for the master instance and its read-only instances. It must be a multiple of 100. The maximum value is 10000. Format: \{“Instanceid1“:”Weight”,”Instanceid2”:”Weight”...\}.

 **Note:** 

-   This parameter is required if DistributionType is set to **Custom**.
-   This parameter is invalid if DistributionType is set to **Standard**.

 |
|AccessKeyId|String|No|LTAIfCxxxxxxx| The AccessKey ID issued by Alibaba Cloud for users to access services.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|4C467B38-3910-447D-87BC-AC049166F216| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=AllocateReadWriteSplittingConnection
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Normal response examples

`XML` format

``` {#xml_return_success_demo}
<AllocateReadWriteSplittingConnectionResponse>
  <RequestId>4C467B38-3910-447D-87BC-AC049166F216</RequestId> 
</AllocateReadWriteSplittingConnectionResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"4C467B38-3910-447D-87BC-AC049166F216"
}
```

## Error codes { .section}

[View error codes](https://error-center.alibabacloud.com/status/product/Rds)

