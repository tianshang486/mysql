# RDS for SQL Server常用视图 {#concept_hvf_51w_hhb .concept}

本文将介绍RDS for SQL Server日常使用和维护时，常用的系统视图及相关查询语句。

## 前提条件 {#section_y3q_x1w_hhb .section}

使用客户端连接实例，请参见[连接实例](../../../../../cn.zh-CN/RDS for SQL Server 快速入门/连接实例.md#)。

## 查询语句 {#section_qqd_z1w_hhb .section}

-   **查看系统参数配置**

    ```
    use master
    select * from sys.configurations
    ```

    ![系统参数配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8353/155436747143431_zh-CN.png)

    **说明：** 参数详细解释请参见[sys.configurations](https://msdn.microsoft.com/en-us/library/ms188345.aspx?spm=a2c4g.11186623.2.12.525121435hM7rO)。

-   **查看数据库的文件相关信息**

    ```
    use <数据库名>
    select * from sys.sysfiless
    ```

    ![数据库文件信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8353/155436747143432_zh-CN.png)

    **查看数据库文件大小**

    ```
    select name, convert(float,size) * (8192.0/1024.0)/1024 AS Size_MB,*  from <数据库名>.dbo.sysfiles
    ```

    ![数据库文件大小](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8353/155436747143433_zh-CN.png)

    **查看数据库文件的I/O统计信息**

    ```
    select * from sys.dm_io_virtual_file_stats(DB_ID('<数据库名>'),<file_id>)
    ```

    ![I/O统计信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8353/155436747143434_zh-CN.png)

-   **查看实例中的所有未提交的事务及其执行的语句**

    ```
    SELECT DB_NAME(dbid) AS DBNAME, 
    (SELECT text FROM sys.dm_exec_sql_text(sql_handle)) AS SQLSTATEMENT 
    FROM master..sysprocesses WHERE open_tran > 0
    ```

    ![事务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8353/155436747243436_zh-CN.png)

-   **查看数据和索引的碎片**

    `DBCC SHOWCONTIG`显示了指定表或者视图的数据以及索引的碎片情况，详细解释请参考[DBCC SHOWCONTIG](https://msdn.microsoft.com/en-us/library/ms175008.aspx?spm=a2c4g.11186623.2.23.525121435hM7rO)。

    ```
    DBCC SHOWCONTIG
    ```

    ![DBCC SHOWCONTIG](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8353/155436747243437_zh-CN.png)

    **查看数据库中的索引碎片**

    ```
    select * from sys.dm_db_index_physical_stats(DB_ID(N'<数据库名>'),NULL,NULL,NULL,DEFAULT)
    ```

    ![查看数据库中的索引碎片](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8353/155436747243439_zh-CN.png)

-   **查看近期执行语句**

    ```
    SELECT
        p.spid, p.status, p.hostname, p.loginame, p.cpu, r.start_time, r.command,
        p.program_name, text
    FROM
        sys.dm_exec_requests AS r,
        master.dbo.sysprocesses AS p
        CROSS APPLY sys.dm_exec_sql_text(p.sql_handle)
    WHERE
        p.status NOT IN ('sleeping', 'background')
    AND r.session_id = p.spid
    ```

    ![查看近期执行语句](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8353/155436747243440_zh-CN.png)


