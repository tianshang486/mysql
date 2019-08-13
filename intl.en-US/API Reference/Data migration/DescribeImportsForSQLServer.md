# DescribeImportsForSQLServer {#reference_ujt_12m_12b .reference}

You can call this operation to view the list of the SQL Server database import tasks and the status of import tasks, and determine whether the import tasks are completed.

**Note:** This operation is not applicable to SQL Server 2017 Cluster Edition instances.

## Request parameters {#section_qzx_w32_12b .section}

|Parameter|Type|Required?|Description|
|---------|----|---------|-----------|
|Action|String|Yes| The operation that you want to perform. Set this parameter to DescribeImportsForSQLServer.

 |
|DBInstanceId|String|Yes|The ID of the instance.|
|ImportId|Integer|No|The ID of the migration result.|
|StartTime|String|Yes|The start time of the query. Format: YYYY-MM-DDThh:mmZ, for example, 2011-06-11T15:00Z.|
|EndTime|String|Yes|The end time of the query. It must be later than the query start time. Format: YYYY-MM-DDThh:mmZ, for example, 2011-06-11T16:00Z.|
|PageSize|Integer|No|The number of records on each page. Valid values: 30 | 50 | 100. Default value: 30.|
|PageNumber|Integer|No|The page number. It must be greater than 0 and cannot exceed the maximum value of the given Integer. Default value: 1.|

## Response parameters {#section_a5x_zlh_12b .section}

The following table describes the response parameters.

|Parameter|Type|Description|
|---------|----|-----------|
|TotalRecordCount|Integer|The total number of records.|
|PageNumber|Integer|The page number.|
|PageRecordCount|Integer|The number of SQL statements on the current page.|
|Items|List<SQLServerImport\>|None.|

The following table describes the parameters in the SQLServerImport field.

|Parameter|Type|Description|
|---------|----|-----------|
|ImportId|Integer|The migration ID.|
|FileName|String|The name of the file.|
|DBName|String|The name of the imported database.|
|ImportStatus|Integer|The import status. Valid values: -   Pending
-   Importing
-   Success
-   Failed
-   Canceled
-   Canceling

 |
|StartTime|String|The import time. Format: YYYY-MM-DD’T’HH:mm:ssZ, for example, 2011-05-30T12:11:40Z.|

## Sample requests {#section_l4g_pj2_12b .section}

``` {#codeblock_rgp_l0u_sni}
https://rds.aliyuncs.com/?Action=DescribeImportsForSQLServer
        &DBInstanceId=rianeurbfaeuq2u2a1370572118496
        &StartTime=2014-06-11T15:00Z
        &EndTime=2014-06-11T16:00Z
        &<Common request parameters>
```

## Sample responses {#section_xtg_rj2_12b .section}

-   `XML` format

    ``` {#codeblock_qb6_n6w_m1q}
    <DescribeImportsForSQLServerResponse> 
            <RequestId>08A3B71B-FE08-4B03-974F-CC7EA6DB1828</RequestId>
            <TotalRecordCount>1</TotalRecordCount>
            <PageNumber>1</PageNumber>
            <PageRecordCount>1<PageRecordCount>
            <Items>
            <SQLServerImport>
            <DBName>testdb01</DBName>
            <FileName>testdb01_1370572475975.bak</FileName>
            <ImportStatus>Success</ImportStatus>
            <StartTime>2014-06-11T15:11:40Z</StartTime>
            </SQLServerImport>
            </Items>
            </DescribeImportsForSQLServerResponse>
    ```

-   `JSON` format

    ``` {#codeblock_zhz_1nz_7pn}
    {
            "PageNumber":1,
            "TotalRecordCount":1,
            "PageRecordCount":1
            "Items":
            {"SQLServerImport":
            [
            {
            "DBName":"testdb01"
            "FileName":"testdb01_1370572475975.bak"
            "ImportStatus":"Success"
            "StartTime": "Innodb"
            }
            ]
            },
            "RequestId": "08A3B71B-FE08-4B03-974F-CC7EA6DB1828"
            }
    ```


