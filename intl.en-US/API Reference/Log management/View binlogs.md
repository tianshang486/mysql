# View binlogs {#reference_dyp_zd3_12b .reference}

## Description {#section_l21_v32_12b .section}

**Note:** This API applies only to MySQL and PostgreSQL instances that use local SSDs.

This API is used to query the binlog files of an instance, supporting query by page and binlog file download.

-   When **DownloadLink** is NULL, RDS does not provide a download URL.
-   When **DownloadLink** is not NULL, you can use this URL to download the backup file through wget \(add double quotes\), a browser, or programming. The expiration time for this URL is **LinkExpiredTime**. Use it before the expiration time. If it has expired, you can see the following error code during the download:

    ```
    <? xml version="1.0" encoding="UTF-8" ? >
    <Error>
    <Code>AccessDenied</Code>
    <Message>Request has expired.</Message>
    <Expires>2012-12-25T09:47:52.000Z</Expires>
    <ServerTime>2012-12-25T09:49:00.000Z</ServerTime>
    <RequestId>50D9768CA801C2F102005C70</RequestId>
    <HostId>oss-test.aliyun-inc.com</HostId>
    </Error>
    ```


## Request parameters {#section_qzx_w32_12b .section}

|Name|Type|Required or not|Description|
|----|----|---------------|-----------|
|Action|String|Yes|Required parameter. Value: DescribeBinlogFiles.|
|DBInstanceId|String|Yes|Instance ID|
|StartTime|String|Yes|Query start time. Format: yyyy-MM-dd’T’HH:mm:ssZ.|
|EndTime|String|Yes|Query end time, which must be later than the query start time. Format: yyyy-MM-dd’T’HH:mm:ssZ.|
|PageSize|Integer|No|Number of records on every page. Values: 30, 50, and 100. Default value: 30.|
|PageNumber|Integer|No|Page number, which must be greater than 0, but must not exceed the maximum integer value. Default value: 1.|

## Return parameters {#section_a5x_zlh_12b .section}

|Name|Type|Description|
|----|----|-----------|
|<Public Return Parameters\>|-|For more information, see [Public parameters](intl.en-US/API Reference/Use APIs/Public parameters.md#).|
|TotalRecordCount|Integer|Total number of binlog files|
|PageNumber|Integer|Page number|
|PageRecordCount|Integer|Number of binlog files displayed on the current page|
|Items|`List<BinLogFile>`|-|

## BinLogFile parameters {#section_vgj_vc3_12b .section}

|Name|Type|Description|
|----|----|-----------|
|FileSize|Long|Binlog file size. Unit: byte.|
|LogBeginTime|String|Start time for binlog file recording|
|LogEndTime|String|End time for binlog file recording|
|DownloadLink|String|HTTP-compliant download URL. If this parameter is set to NULL, there is no download URL.|
|HostInstanceID|String|ID of the instance to which the binlog belongs. This parameter indicates whether the binlog is from the master or slave instance.|
|LinkExpiredTime|String|URL expiration time, for example, 2011-06-11T15:00:00Z.|

## Request example {#section_l4g_pj2_12b .section}

```
https://rds.aliyuncs.com/?Action=DescribeBinlogFiles
&DBInstanceId=riauvjz6zajfiq6ba137xxxxx
&StartTime=2011-06-11T15:00:00Z
&EndTime=2013-06-05T15:00:00Z
&<Public request parameters>
```

## Response example {#section_xtg_rj2_12b .section}

**XML format**

```
<DescribeBinlogFilesResponse> 
  <RequestId>66816822-CEC1-4C8D-AB26-2530A7D4DCA5</RequestId>
  <TotalRecordCount>1</TotalRecordCount>
  <PageNumber>1</PageNumber>
  <PageRecordCount>1<PageRecordCount>
  <Items>
    <BinLogFile>
    <FileSize>123</FileSize>
    <LogBeginTime>2013-06-01T15:00:00Z</LogBeginTime>
     <LogEndTime>2013-06-02T18:00:00Z</LogEndTime>
     <DownloadLink>http://rdslog- real.oss.aliyuncs.com/custins47742/hostins46770/mysql-bin. 000120.zip? spm=0.0.0.0.eMQKjs&OSSAccessKeyId=c9gzsqpauj3xxxxx&Expires=1384916927&Signature=07TMgM3G2Jw4sOOxxxxx</DownloadLink>
    <LinkExpiredTime>2013-06-09T18:00:00Z</LinkExpiredTime>
   </BinLogFile>
  </Items>
</DescribeBinlogFilesResponse>
```

**JSON format**

```
{
    "RequestId":"66816822-CEC1-4C8D-AB26-2530A7D4DCA5"
"PageNumber":1,
"TotalRecordCount":1,
"PageRecordCount":1
"Items":
{"BinLogFile":
[
{
FileSize:”123”
LogBeginTime:”2013-06-01T15:00:00Z”
LogEndTime:”2013-06-02T18:00:00Z”
DownloadLink:”http://rdslog-real.oss.aliyuncs.com/custins47742/hostins46770/mysql-bin. 000120.zip?spm=0.0.0.0.eMQKjs&OSSAccessKeyId=c9gzsqpauj3xxxxx&Expires=1384916927&Signature=07TMgM3G2Jw4sOOxxxxx”
LinkExpiredTime”2013-06-09T18:00:00Z”
}
]
}
}
```

