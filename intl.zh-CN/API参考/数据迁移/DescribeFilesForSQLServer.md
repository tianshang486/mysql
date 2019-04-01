# DescribeFilesForSQLServer {#reference_ifs_4bm_12b .reference}

查看文件服务器的文件列表。

通过该接口，您可以得到文件服务器上传账号。在数据文件上传结束后，RDS会更新数据文件状态。通过改接口，也可以查看数据文件是否可用。如果文件可用，则可以进行数据导入，并得到导入过程信息。

**说明：** 该接口只适用于RDS for SQL Server（除SQL Server 2017集群版）的实例。

## 请求参数 {#section_qzx_w32_12b .section}

|名称|类型|是否必须|描述|
|--|--|----|--|
|Action|String|是| 要执行的操作，取值：

 DescribeFilesForSQLServer

 |
|DBInstanceId|String|是|实例ID。|
|StartTime|String|是|查询开始时间，格式如：2011-06-11T15:00Z。|
|EndTime|String|是|查询结束时间，格式如：2011-06-11T16:00Z，大于查询开始时间。|
|PageSize|Integer|否|每页记录数，取值：30/50/100，默认值：30。|
|PageNumber|Integer|否|页码，大于0且不超过Integer的最大值，默认值：1。|

## 返回参数 {#section_a5x_zlh_12b .section}

|名称|类型|描述|
|--|--|--|
|DBInstanceId|String|实例ID。|
|TotalRecordCount|Integer|总记录数。|
|PageNumber|Integer|页码。|
|PageRecordCount|Integer|本页SQL语句个数。|
|Items|List<SQLServerUploadFile\>|-|

**SQLServerUploadFile参数**

|名称|类型|描述|
|--|--|--|
|DBName|String|数据库名。|
|FileName|String|数据文件名，带扩展名。|
|FileSize|Long|数据文件大小，单位：Byte。|
|InternetFtpServer|String|外网服务器。|
|InternetPort|Integer|外网服务器端口。|
|IntranetFtpserver|String|内网服务器地址。|
|Intranetport|Integer|内网服务器端口。|
|UserName|String|文件服务器账号。|
|Password|String|文件服务器账号密码。|
|FileStatus|String|文件状态。-   Unavailable：不可用；
-   Available：可用
-   NotStarted：未开始；
-   Uploading：正在上传；
-   UploadFailed：上传失败；
-   Virus：有病毒；
-   Deleted：文件被删除；
-   Success：上传成功。

|
|CreationTime|String|FTP文件生成时间，格式为YYYY-MM-DD’T’HH:mm:ssZ，如2011-05-30 T12:11:4Z。|

## 请求示例 {#section_l4g_pj2_12b .section}

```
https://rds.aliyuncs.com/?Action=DescribeFilesForSQLServer
        &DBInstanceId=rm-uf6wjk5xxxx
        &StartTime=2014-06-11T15:00Z
        &EndTime=2014-06-11T16:00Z
        &<公共请求参数>
```

## 返回示例 {#section_xtg_rj2_12b .section}

-   **XML格式**

    ```
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

-   **JSON格式**

    ```
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


