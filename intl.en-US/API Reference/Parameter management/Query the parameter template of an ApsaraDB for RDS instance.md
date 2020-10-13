# Query the parameter template of an ApsaraDB for RDS instance

Queries the parameter template of an ApsaraDB for RDS instance.

Before you call this operation, make sure that the instance runs one of the following database engines:

-   MySQL 5.5, 5.6, 5.7, and 8.0
-   SQL Server 2008 R2
-   PostgreSQL 9.4, 10, 11, and 12
-   PPAS 9.3 and 10.0
-   MariaDB 10.3

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeParameterTemplates&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeParameterTemplates|The operation that you want to perform. Set the value to **DescribeParameterTemplates**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx|The ID of the instance. |
|Engine|String|Yes|mysql|The database engine that the instance runs. Valid values:

 -   **mysql:** The instance runs MySQL.
-   **mssql:** The instance runs SQL Server.
-   **PostgreSQL:** The instance runs PostgreSQL.
-   **PPAS:** The instance runs PPAS.
-   **MariaDB:** The instance runs MariaDB. |
|EngineVersion|String|Yes|5.6|The version of the database engine. Valid values:

 -   MySQL: **5.5 \| 5.6 \| 5.7 \| 8.0**
-   SQL Server: **2008r2**
-   PostgreSQL: **9.4 \| 10.0 \| 11.0 \| 12.0**
-   PPAS: **9.3 \| 10.0**
-   MariaDB: **10.3** |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxx|The client token that is used to ensure the idempotency of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|Category|String|No|Basic|The RDS edition of the instance. Valid values:

 -   **Basic:** The instance is of the Basic Edition.
-   **HighAvailability:** The instance is of the High-availability Edition.
-   **Finance:** The instance is of the Enterprise Edition. |
|RegionId|String|No|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Engine|String|MySQL|The database engine. |
|EngineVersion|String|5.5|The version of the database engine. |
|ParameterCount|String|56|The number of parameters. |
|Parameters|Array| |The list of parameters. |
|TemplateRecord| | | |
|ParameterName|String|auto\_increment\_increment|The name of the parameter. |
|ParameterValue|String|1|The default value of the parameter. |
|ForceModify|String|true|Indicates whether the parameter can be modified. Valid values: **true \| false** |
|ForceRestart|String|false|Indicates whether the modified parameter takes effect only after a database restart. Valid values: **true \| false** |
|CheckingCode|String|\[10-3000\]|The value range of the parameter. |
|ParameterDescription|String|determines the starting point for the AUTO\_INCREMENT column value.|The description of the parameter. |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeParameterTemplates
&Engine=MySQL
&EngineVersion=5.6
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeParameterTemplatesResponse>
    <Engine>mssql</Engine>
    <EngineVersion>2008r2</EngineVersion>
    <ParameterCount>1</ParameterCount>
    <Parameters>
        <TemplateRecord>
          <CheckingCode>[0-100]</CheckingCode>
          <ForceRestart>True</ForceRestart>
          <Factor>1</Factor>
          <ParameterDescription>xxxxxxx</ParameterDescription>
          <ParameterName>fill factor</ParameterName>
          <ParameterValue>0</ParameterValue>
          <ForceModify>True</ForceModify>
          <Unit>INT</Unit>
        </TemplateRecord>
    </Parameters>
    <RequestId>7B96585A-0FF2-4979-8FE5-7D147A29FDC0</RequestId>
</DescribeParameterTemplatesResponse>
```

`JSON` format

```
{
  "DescribeParameterTemplatesResponse": {
    "Engine": "mssql",
    "EngineVersion": "2008r2",
    "ParameterCount": "1",
    "Parameters": {
      "TemplateRecord": {
        "CheckingCode": "[0-100]",
        "ForceRestart": "True",
        "Factor": "1",
        "ParameterDescription": "xxxxxxx",
        "ParameterName": "fill factor",
        "ParameterValue": "0",
        "ForceModify": "True",
        "Unit": "INT"
      }
    },
    "RequestId": "7B96585A-0FF2-4979-8FE5-7D147A29FDC0"
  }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).

