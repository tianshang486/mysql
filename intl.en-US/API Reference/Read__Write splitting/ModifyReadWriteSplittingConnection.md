# ModifyReadWriteSplittingConnection {#doc_api_Rds_ModifyReadWriteSplittingConnection .reference}

You can call this operation to modify the latency threshold of the read/write splitting address and the read weight of each instance.

When you call this operation, the instance must meet the following requirements:

-   The instance is in the running state.
-   The instance does not have an ongoing migration task.

**Note:** This operation is applicable to MySQL instances and SQL Server 2017 Cluster Edition instances.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyReadWriteSplittingConnection) to perform debugging.

API Explorer provides various functions to simplify API usage. For example, you can search APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyReadWriteSplittingConnection| The operation that you want to perform. Set the value to **ModifyReadWriteSplittingConnection**.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx| The ID of the master instance.

 |
|ConnectionStringPrefix|String|No|rm-m5xxxxxxxx.mysql.rds.aliyuncs.com| The prefix of the read/write splitting address. It must be unique and start with a letter. It contains at most 30 characters, including lowercase letters or hyphens \(-\).

 **Note:** By default, the prefix is "instance name + rw".

 |
|MaxDelayTime|String|No|12| The latency threshold. Unit: seconds. If a read-only instance reaches the latency threshold, read requests are no longer sent to the read-only instance.

 **Note:** 

-   This parameter is not applicable to SQL Server 2017 Cluster Edition instances.
-   If this parameter is not entered, the parameter value remains unchanged.
-   Either **MaxDelayTime** or **DistributionType** is required.

 |
|DistributionType|String|No|Standard| The mode of read weight distribution. Valid values:

 -   **Standard**: Read weights are distributed according to instance specifications.
-   **Custom**: Read weights are specified by you.

 **Note:** Either **MaxDelayTime** or **DistributionType** is required.

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
|RequestId|String|5A77D650-27A1-4E08-AD9E-59008EDB6927| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyReadWriteSplittingConnection
&DistributionType=Standard
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Normal response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyReadWriteSplittingConnectionResponse>
  <RequestID>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestID>
</ModifyReadWriteSplittingConnectionResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestID":"5A77D650-27A1-4E08-AD9E-59008EDB6927"
}
```

## Error codes {#section_mjm_7zt_cmx .section}

[View error codes](https://error-center.alibabacloud.com/status/product/Rds)

