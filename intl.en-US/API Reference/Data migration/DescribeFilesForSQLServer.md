# DescribeFilesForSQLServer {#reference_ifs_4bm_12b .reference}

You can call this operation to view the list of files on the file server.

You can obtain your account to upload data files to the file server through this operation. After the data files are uploaded, RDS updates their status. You can also call this operation to check whether the data files are available. If they are available, you can import data and obtain the information about the import process.

**Note:** This operation is applicable only to RDS for SQL Server instances, except for SQL Server 2017 Cluster Edition instances.

## Request parameters {#section_qzx_w32_12b .section}

|Parameter|Type|Required?|Description|
|---------|----|---------|-----------|
|Action|String|Yes| The operation that you want to perform. Set this parameter to DescribeFilesForSQLServer.

 |
|DBInstanceId|String|Yes|The ID of the instance.|
|StartTime|String|Yes|The start time of the query. Format: YYYY-MM-DDThh:mmZ, for example, 2011-06-11T15:00Z.|
|EndTime|String|Yes|The end time of the query. It must be later than the query start time. Format: YYYY-MM-DDThh:mmZ, for example, 2011-06-11T16:00Z.|
|PageSize|Integer|No|The number of records on each page. Valid values: 30 | 50 | 100. Default value: 30.|
|PageNumber|Integer|No|The page number. It must be greater than 0 and cannot exceed the maximum value of the given Integer. Default value: 1.|

## Response parameters {#section_a5x_zlh_12b .section}

The following table describes the response parameters.

|Parameter|Type|Description|
|---------|----|-----------|
|DBInstanceId|String|The ID of the instance.|
|TotalRecordCount|Integer|The total number of records.|
|PageNumber|Integer|The page number.|
|PageRecordCount|Integer|The number of SQL statements on the current page.|
|Items|List<SQLServerUploadFile\>|None.|

The following table describes the parameters in the SQLServerUploadFile field.

|Parameter|Type|Description|
|---------|----|-----------|
|DBName|String|The name of the database.|
|FileName|String|The name of the data file, with the extension.|
|FileSize|Long|The size of the data file. Unit: byte.|
|InternetFtpServer|String|The file server on the public network.|
|InternetPort|Integer|The port of the file server on the public network.|
|IntranetFtpserver|String|The IP address of the file server on the internal network.|
|Intranetport|Integer|The port of the file server on the internal server.|
|UserName|String|The username used to log on to the file server.|
|Password|String|The password used to log on to the file server.|
|FileStatus|String|The status of files. Valid values: -   Unavailable
-   Available
-   NotStarted
-   UploadFailed
-   Virus
-   Success

 |
|CreationTime|String|The generation time of the FTP file. Format: YYYY-MM-DD’T’HH:mm:ssZ, for example, 2011-05-30 T12:11:4Z.|

## Sample requests {#section_l4g_pj2_12b .section}

``` {#codeblock_98e_ddo_qm2}
https://rds.aliyuncs.com/?Action=DescribeFilesForSQLServer
        &DBInstanceId=rm-uf6wjk5xxxx
        &StartTime=2014-06-11T15:00Z
        &EndTime=2014-06-11T16:00Z 
        &<Common request parameters>
```

## Sample responses {#section_xtg_rj2_12b .section}

-   `XML` format

    ``` {#codeblock_wla_1er_cgz}
    < DescribeFilesForSQLServerResponse> 
            <RequestId>08A3B71B-FE08-4B03-974F-CC7EA6DB1828</RequestId>
            <TotalRecordCount>1</TotalRecordCount>
            <PageNumber>1</PageNumber>
            <PageRecordCount>1<PageRecordCount>
            <Items>
            <SQLServerUploadFile>
            <DBName>testdb01</DBName>
            <FileName>testdb01_1370572475975.bak</FileName>
            <FileSize>1243435</FileSize>
            <InternetFtpServer>10.230.239.1</InternetFtpServer>
            <InternetPort>3021</InternetPort>
            <IntranetFtpServer></IntranetFtpServer>
            <IntranetPort></IntranetPort>
            <UserName>MKExxxxx</UserName>
            <Password>aT2Y_Xxxxxx</Password>
            <FileStatus>Success</FileStatus>
            <CreationTime>2014-06-11T15:02:40Z</CreationTime>
            </SQLServerUploadFile>
            </Items>
            </DescribeFilesForSQLServerResponse>
    ```

-   `JSON` format

    ``` {#codeblock_3e3_ov2_l32}
    {
            "PageNumber":1,
            "TotalRecordCount":1,
            "PageRecordCount":1
            "Items":
            {"SQLServerUploadFile":
            [
            {
            "DBName":"testdb01"
            "FileName":"testdb01_1370572475975.bak"
            "FileSize ":"1243435"
            "InternetFtpServer ":"10.230.239.1"
            "InternetPort":3021
            "IntranetFtpServer":""
            "IntranetPort":
            "UserName":"MKExxxxx"
            "Password":"aT2Y_Xxxxxx"
            "FileStatus": "Success "
            "CreationTime": "2014-06-11T15:02:40Z"
            } 
            ]
            },
            "RequestId": "08A3B71B-FE08-4B03-974F-CC7EA6DB1828"
            }
    ```


