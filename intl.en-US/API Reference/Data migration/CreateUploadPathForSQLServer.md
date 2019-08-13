# CreateUploadPathForSQLServer {#reference_t52_1bm_12b .reference}

You can call this operation to create a username and password to log on to the file server, and a path to upload files. You can upload data files based on this information. After uploading these data files, you can migrate the external data.

The operation must meet the following requirements:

-   The instance is an RDS for SQL Server instance.
-   The instance must be in the running state.
-   The database must be in the running state.
-   Up to 20 files can be created for a single database every day. A 24-hour period is considered as a single day. For example, if the last creation time was 2012-03-15 18:30:12, the next creation time must be later than 2012-03-16 18:30:12.

**Note:** This operation is not applicable to SQL Server 2017 Cluster Edition instances.

## Request parameters {#section_qzx_w32_12b .section}

|Parameter|Type|Required?|Description|
|---------|----|---------|-----------|
|Action|String|Yes| The operation that you want to perform. Set this parameter to CreateUploadPathForSQLServer.

 |
|DBInstanceId|String|Yes|The ID of the instance.|
|DBName|String|Yes|The name of the database.|

## Response parameters {#section_a5x_zlh_12b .section}

|Parameter|Type|Description|
|---------|----|-----------|
|<Common response parameters\>|N/A|For more information, see [Public parameters](intl.en-US/API Reference/Use APIs/Public parameters.md#).|
|InternetFtpServer|String|The IP address of the file server on the public network.|
|InternetPort|Integer|The port of the file server on the public network.|
|IntranetFtpServer|String|The IP address of the file server on the internal network.|
|IntranetPort|Integer|The port of the file server on the internal network.|
|UserName|String|The username used to log on to the file server.|
|Password|String|The password used to log on to the file server.|
|FileName|String|The name of the data file, with the extension.|

## Sample requests {#section_l4g_pj2_12b .section}

``` {#codeblock_87j_jbg_npr}
https://rds.aliyuncs.com/?Action= CreateUploadPathForSQLServer
        &DBInstanceId=rianeurbfaeuq2u2a1370572118496
        &DBName=testdb01 
        &<Common request parameters>
```

## Sample responses {#section_xtg_rj2_12b .section}

-   `XML` format

    ``` {#codeblock_joh_q9o_zmy}
    <CreateUploadPathForSQLServerResponse>
            <RequestId>66816822-CEC1-4C8D-AB26-2530A7D4DCA5</RequestId>
            <InternetFtpServer>10.230.239.1</InternetFtpServer>
            <InternetPort>3021</InternetPort>
            <IntranetFtpServer></IntranetFtpServer>
            <IntranetPort></IntranetPort>
            <UserName>MKEakJbyG</UserName>
            <Password>aT2Y_XN1GGnOLzm</Password>
            <FileName>testdb01_1370572475975.bak</FileName>
            </CreateUploadPathForSQLServerResponse>
    ```

-   `JSON` format

    ``` {#codeblock_pzz_07u_iz3}
    {
            "RequestId":"66816822-CEC1-4C8D-AB26-2530A7D4DCA5"
            "InternetFtpServer ":"10.230.239.1"
            "InternetPort":3021
            "IntranetFtpServer":""
            "IntranetPort":
            "UserName":"MKEakJbyG"
            "Password":"aT2Y_XN1GGnOLzm"
            "FileName":"testdb01_1370572475975.bak"
            }
    ```


