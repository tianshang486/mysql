# Query parameter configurations

Queries the parameter configurations of an ApsaraDB for RDS instance.

This operation is applicable to ApsaraDB for RDS instances that run the following database engines:

-   MySQL 5.5, 5.6, 5.7, and 8.0
-   SQL Server 2008 R2
-   PostgreSQL 9.4, 10, 11, and 12
-   PPAS 9.3 and 10
-   MariaDB 10.3

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeParameters&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeParameters|The operation that you want to perform. Set the value to **DescribeParameters**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxx|The client token that is used to ensure the idempotency of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Engine|String|MySQL|The database engine. |
|EngineVersion|String|5.5|The edition of the database engine. |
|RunningParameters|Array| |The list of running parameters for the instance. |
|DBInstanceParameter| | | |
|ParameterName|String|fill factor|The name of a parameter. |
|ParameterValue|String|0|The value of a parameter. |
|ParameterDescription|String|This parameter sets the default fill factor value at the server scope. A fill factor is provided to optimize index data storage and performance.|The description of a parameter. |
|ConfigParameters|Array| |The list of parameters that are being synchronized. After you modify and submit the parameters, you must wait for the parameters to be synchronized to the instance. After synchronization, you can delete the parameters from the list. |
|DBInstanceParameter| | | |
|ParameterName|String|fill factor|The name of a parameter. |
|ParameterValue|String|50|The value of a parameter. |
|ParameterDescription|String|This parameter sets the default fill factor value at the server scope. A fill factor is provided to optimize index data storage and performance.|The description of a parameter. |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeParameters
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeParametersResponse>
	  <ConfigParameters>
		    <DBInstanceParameter>
			      <ParameterDescription> This parameter sets the default fill factor value at the server scope. A fill factor is provided to optimize index data storage and performance. </ParameterDescription>
			      <ParameterName>fill factor</ParameterName>
			      <ParameterValue>50</ParameterValue>
		    </DBInstanceParameter>
	  </ConfigParameters>
	  <Engine>mssql</Engine>
	  <EngineVersion>2008r2</EngineVersion>
	  <RunningParameters>
		    <DBInstanceParameter>
			      <ParameterDescription> This parameter sets the default fill factor value at the server scope. A fill factor is provided to optimize index data storage and performance. </ParameterDescription>
			      <ParameterName>fill factor</ParameterName>
			      <ParameterValue>0</ParameterValue>
		    </DBInstanceParameter>
	  </RunningParameters>
	  <RequestId>2A748162-8040-4D6B-813E-6910C8C033F1</RequestId>
</DescribeParametersResponse>
```

`JSON` format

```
{
  "ConfigParameters": {
      "DBInstanceParameter": [
          {
              "ParameterDescription": "This parameter sets the default fill factor value for the server range. A fill factor is provided to optimize index data storage and performance.", 
              "ParameterName": "fill factor", 
              "ParameterValue": "50"
          }
      ]
  }, 
  "Engine": "mssql", 
  "EngineVersion": "2008r2", 
  "RunningParameters": {
      "DBInstanceParameter": [
          {
              "ParameterDescription": "This parameter sets the default fill factor value for the server range. A fill factor is provided to optimize index data storage and performance.", 
              "ParameterName": "fill factor", 
              "ParameterValue": "0"
          }
      ]
  }, 
  "RequestId": "2A748162-8040-4D6B-813E-6910C8C033F1"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

