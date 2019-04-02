# RDS for SQL Server如何查看实例、数据库及表占用的空间大小 {#concept_fxr_jm1_hhb .concept}

## 查看实例空间的大小 {#section_vns_4m1_hhb .section}

在控制台基本信息页面查看实例空间情况。

![实例空间](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8343/155417024042167_zh-CN.png)

## 查看数据库的大小 {#section_ec3_bn1_hhb .section}

1.  使用客户端连接实例，请参见[连接实例](../../../../../cn.zh-CN/RDS for SQL Server 快速入门/连接实例.md#)。
2.  在SQL窗口中执行以下命令。

    ```
    use <数据库名> 
    go 
    sp_spaceused @updateusage=N'true'
    ```

    ![查询数据库大小](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8343/155417024042170_zh-CN.png)

    |参数|说明|
    |--|--|
    |**database\_size**|即数据库的大小，它包含日志的大小，始终大于**reserved**+**unallocated\_space**。|
    |**unallocated space**|数据库的未分配空间。|
    |**reserved**|已分配的空间总量。|
    |**data**|数据使用的空间总量。|
    |**index\_size**|索引使用的空间。|
    |**unused**|未用的空间量。|

    **说明：** 查看所有的数据库，则需要使用脚本来实现，脚本如下：

    ```
    USE master
    go
    DECLARE @insSize TABLE(dbName sysname,checkTime VARCHAR(19),dbSize VARCHAR(50),logSize VARCHAR(50))
    INSERT INTO @insSize ( dbName, checkTime, dbSize, logSize )
    EXEC sp_msforeachdb 'select ''?'' dbName,CONVERT(VARCHAR(19),GETDATE(),120) checkTime,LTRIM(STR(SUM(CASE WHEN RIGHT(FILENAME,3)<>''ldf'' THEN convert (dec (15,2),size) * 8 / 1024 ELSE 0 END),15,2)+'' MB'') dbSize,  
                     LTRIM(STR(SUM(CASE WHEN RIGHT(FILENAME,3)=''ldf''  THEN convert (dec (15,2),size) * 8 / 1024 ELSE 0 END),15,2)+'' MB'') logSize from ?.dbo.sysfiles'
    SELECT * FROM @insSize ORDER BY CONVERT(DECIMAL,LTRIM(RTRIM(SUBSTRING(dbSize,1,LEN(dbSize)-2)))) DESC
    ```


该结果包含日志文件的大小，查看日志文件的大小的SQL语句是：

```
dbcc sqlperf(logspace)
```

![日志文件大小](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8343/155417024042172_zh-CN.png)

## 查看数据库中表的大小 {#section_a43_bn1_hhb .section}

1.  使用客户端连接实例，请参见[连接实例](../../../../../cn.zh-CN/RDS for SQL Server 快速入门/连接实例.md#)。
2.  在SQL窗口中执行以下命令。

    ```
    use <数据库名> 
    go 
    sp_spaceused N'<表名>'
    ```

    ![查询表大小](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8343/155417024042174_zh-CN.png)

    **说明：** 查看该库所有的表，则需要使用脚本来实现，脚本如下：

    ```
    use <数据库名>
    go
    declare @tabSize table(name nvarchar(100),rows char(20),reserved varchar(18) ,data varchar(18) ,index_size varchar(18) ,nnused varchar(18) )
    insert into @tabSize exec sp_msforeachtable 'sp_spaceused ''?'''
    select * from @tabSize order by convert(int,replace(data,'KB','')) desc,2 desc
    ```


