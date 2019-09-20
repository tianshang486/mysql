# Read and write external data files by using the oss\_fdw plugin {#concept_d23_m3g_wdb .concept}

This topic describes how to read and write external data files by using the oss\_fdw plugin. In Alibaba Cloud, you can use this plugin to load data from OSS to an RDS for PostgreSQL or RDS for PPAS instance. You can also write data from an RDS for PostgreSQL or RDS for PPAS instance to OSS.

## oss\_fdw parameters {#section_cvf_43g_wdb .section}

Similar to other fdw interfaces, oss\_fdw can encapsulate data stored on OSS \(external data sources\), allowing you to read files on OSS. The process is like reading data from a table. oss\_fdw provides unique parameters used for connecting to and parsing file data on OSS.

**Note:** 

-   Currently, oss\_fdw can read and write the following file types in OSS: .text/.csv files and .text/.csv files in GZIP format.
-   The value of each parameter needs to be quoted and cannot contain any useless spaces.

## CREATE SERVER parameters {#section_smy_p3g_wdb .section}

-   ossendpoint: Address \(host\) used to access OSS from a private network
-   id: OSS account ID
-   key: OSS account key
-   bucket: OSS bucket, assigned after an OSS account is created

The following parameters are related to error tolerance in import and export modes. If network connectivity is poor, you can reconfigure these parameters to facilitate successful imports and exports.

-   oss\_connect\_timeout: Connection expiration time, measured in seconds. Default value: 10s.
-   oss\_dns\_cache\_timeout: DNS expiration time, measured in seconds. Default value: 60s.
-   oss\_speed\_limit: Minimum tolerable rate. Default value: 1,024 byte/s \(1 Kbit/s\).
-   oss\_speed\_time: Maximum tolerable time. Default value: 15s.

If the default values of the oss\_speed\_limit and oss\_speed\_time parameters are used, a timeout error occurs when the transmission rate is smaller than 1 Kbit/s for 15 consecutive seconds.

## CREATE FOREIGN TABLE parameters {#section_hhj_r3g_wdb .section}

-   filepath: File name including a path on OSS.
    -   A file name contains a path but not a bucket name.
    -   This parameter matches multiple files in the corresponding path on OSS, and supports file loading to a database.
    -   Files named in the format of filepath or filepath.x can be imported to a database. x in filepath.x must start from 1 and be consecutive.

        For example, if there are five files, filepath, filepath.1, filepath.2, filepath.3, and filepath.5, then the first four files are matched and imported, but the file named filepath.5 is not.

-   dir: Virtual directory on OSS.
    -   The value of this parameter must end with a slash \(/\).
    -   All files \(excluding subfolders and files in subfolders\) in the virtual directory indicated by this parameter are matched and imported to a database.
-   prefix: Prefix of the path in the data file. Regular expressions are not supported. You can set only one of the these parameters: prefix, filepath, and dir.
-   format: File format, which can only be CSV currently.
-   encoding: File data encoding format. It supports common PostgreSQL encoding formats, such as UTF-8.
-   parse\_errors: Parsing in error tolerance mode. The errors that occur during the file parsing process are ignored by row.
-   delimiter: Delimiter specified for columns.
-   quote: Quote character for a specified file.
-   escape: Escape character for a specified file.
-   null: Used to nullify the column matching a specified string. For example, `null 'test'` is used to set the column whose value is test to null.
-   force\_not\_null: Used to un-nullify the value of one or more columns. For example, `force_not_null 'id'` is used to set the values of the id column to empty strings.
-   compressiontype: Used to set whether the file read or written on OSS is compressed and set the compression format. Values:
    -   none: Uncompressed \(default value\)
    -   gzip: compressed gzip file
-   compressionlevel: Used to set the compression level of the compression format written to OSS. Value range: 1 to 9. Default value: 6.

**Note:** 

-   The filepath and dir parameters need to be specified in the OPTIONS parameter.
-   Either the filepath or dir parameter must be specified, and they cannot be specified at the same time.
-   The export mode currently only supports virtual folders, that is, only the dir parameter is supported.

## Export mode parameters for CREATE FOREIGN TABLE {#section_sxg_t3g_wdb .section}

-   oss\_flush\_block\_size: Buffer size for the data written to OSS at a time. Its default value is 32 MB, and the value range is 1 MB to 128 MB.
-   oss\_file\_max\_size: Maximum file size for the data written to OSS \(subsequent data is written in another file when the maximum file size is exceeded\). Its default value is 1,024 MB, and the value range is 8 MB to 4,000 MB.
-   num\_parallel\_worker: The number of parallel compression threads in the compression mode in which the OSS data is written, ranging from 1 to 8. Its default value is 3.

## Auxiliary function {#section_uw1_x3g_wdb .section}

FUNCTION oss\_fdw\_list\_file \(relname text, schema text DEFAULT 'public'\)

-   Used to obtain the name and size of the OSS file that an external table matches.
-   The unit of file size is byte.

``` {#codeblock_wmk_05e_ik4}
select * from oss_fdw_list_file('t_oss');
              name | size    

 oss_test/test.gz. 1 | 739698350
 oss_test/test.gz. 2 | 739413041
 oss_test/test.gz. 3 | 739562048
(3 rows)
```

## Auxiliary feature {#section_tn2_z3g_wdb .section}

oss\_fdw.rds\_read\_one\_file: In read mode, it is used to specify a file that matches the external table. Once it is set, the external table matches only one file that is set during data import.

For example, set oss\_fdw.rds\_read\_one\_file = ‘oss\_test/example16.csv. 1’;

``` {#codeblock_fsc_75f_qgz}
set oss_fdw.rds_read_one_file = 'oss_test/test.gz. 2';
select * from oss_fdw_list_file('t_oss');
              name | size    

  oss_test/test.gz. 2 | 739413041
(1 rows)
```

## oss\_fdw example {#section_pgb_bjg_wdb .section}

``` {#codeblock_5aa_3a7_v8a}
# (PostgreSQL) Create the plugin
create extension oss_fdw;  ----For PPAS, run: select rds_manage_extension('create','oss_fdw');
# Create a server instance  
CREATE SERVER ossserver FOREIGN DATA WRAPPER oss_fdw OPTIONS 
     (host 'oss-cn-hangzhou.aliyuncs.com' ， id 'xxx'， key 'xxx'，bucket 'mybucket');
# Create an OSS external table
CREATE FOREIGN TABLE ossexample 
    (date text， time text， open float，
     high float， low float， volume int) 
     SERVER ossserver 
     OPTIONS ( filepath 'osstest/example.csv'， delimiter '，' ，
         format 'csv'， encoding 'utf8'， PARSE_ERRORS '100');
# Create a table, to which data is loaded
create table example
        (date text， time text， open float，
         high float， low float， volume int);
# Load data from ossexample to example.
insert into example select * from ossexample;
# As you can see
# oss_fdw estimates the file size on OSS and formulates a query plan correctly.
explain insert into example select * from ossexample;
                             QUERY PLAN                              

 Insert on example (cost=0.00.. 1.60 rows=6 width=92)
   -> Foreign Scan on ossexample (cost=0.00.. 1.60 rows=6 width=92)
         Foreign OssFile: osstest/example.csv. 0
         Foreign OssFile Size: 728
(4 rows)
# Write the data in the example table to OSS.
insert into ossexample select * from example;
explain insert into ossexample select * from example;
                           QUERY PLAN

 Insert on ossexample  (cost=0.00..16.60 rows=660 width=92)
   ->  Seq Scan on example  (cost=0.00..16.60 rows=660 width=92)
(2 rows)
```

## oss\_fdw usage tips {#section_frx_cjg_wdb .section}

-   oss\_fdw is an external table plugin developed based on the PostgreSQL FOREIGN TABLE framework.
-   The data import performance is related to the PostgreSQL cluster resources \(CPU I/O MEM MET\) and OSS.
-   For expected data import performance, ossendpoint in ossprotocol must match the region where PostgreSQL is located in Alibaba Cloud. For more information, see [Endpoints](https://www.alibabacloud.com/help/doc-detail/31834.htm).
-   If the error "oss endpoint userendpoint not in aliyun white list" is triggered during reading of SQL statements for external tables, use these [regions and endpoints](https://www.alibabacloud.com/help/doc-detail/31837.htm). If the problem persists, submit a trouble ticket.

## Error handling {#section_owy_djg_wdb .section}

When an import or export error occurs, the error log contains the following information:

-   code: HTTP status code of the erroneous request.
-   error\_code: Error code returned by OSS.
-   error\_msg: Error message provided by OSS.
-   req\_id: UUID that identifies the request. If you cannot solve the problem, you can seek help from OSS development engineers by providing the req\_id.

For more information about error types, see the reference links at the end of this document. Timeout errors can be handled using oss\_ext parameters.

-   [OSS help](https://www.alibabacloud.com/help/product/31815.htm)
-   [PostgreSQL CREATE FOREIGN TABLE](http://www.postgresql.org/docs/9.4/static/sql-createforeigntable.html)
-   [Exception handling](https://www.alibabacloud.com/help/doc-detail/32141.htm)
-   [OSS error response](https://www.alibabacloud.com/help/doc-detail/32005.htm)

## Hide IDs and keys {#section_pmk_fjg_wdb .section}

If the id and key parameters for CREATE SERVER are not encrypted, plaintext information is displayed by using `select * from pg_foreign_server`, making the ID and key exposed. The symmetric encryption can be performed to hide the ID and key \(use different keys of different instances for further protection of your information\). However, to avoid incompatibility with old instances, you cannot use methods similar to GP to add a data type.

Encrypted information:

``` {#codeblock_i5b_pzl_t0y}
postgres=# select * from pg_foreign_server ;
  srvname  | srvowner | srvfdw | srvtype | srvversion | srvacl |                                                                              srvoptions

-----------+----------+--------+---------+------------+--------+------------------------------------------------------------------------------------------------------------------------------------
----------------------------------
 ossserver |       10 |  16390 |         |            |        | {host=oss-cn-hangzhou-zmf.aliyuncs.com，id=MD5xxxxxxxx，key=MD5xxxxxxxx，bucket=067862}
			
```

The encrypted information is preceded by MD5 \(total length: len%8==3\). Therefore, encryption is not performed again when the exported data is imported. But you cannot create the key and ID preceded by MD5.

