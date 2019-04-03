# 解决SQL Server实例空间满自动锁的问题 {#concept_ygc_prm_hhb .concept}

SQL Server实例可能会由于SQL语句、外部攻击等原因导致实例空间满，为避免数据丢失，RDS会对实例进行自动锁定，磁盘锁定之后，将无法进行写入操作。

## 背景信息 {#section_m3j_zlb_3gb .section}

当实例由于实例空间满自动锁定时，控制台可以在**基本信息** \> **运行状态**看到如下信息：

![锁定截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8352/155426074243180_zh-CN.png)

本文将介绍造成实例空间满的常见原因及其相应的解决方法。

## 常见原因 {#section_d2l_4zp_yfb .section}

造成SQL Server实例空间满的主要有如下三种原因：

-   日志文件占用量高。
-   数据文件占用量高。
-   临时文件占用量高。

## 查看空间使用状况 {#section_dng_qzp_yfb .section}

**方法一**

通过RDS管理控制台的监控页面查看空间使用情况，详情请参见[查看资源和引擎监控](../../../../../cn.zh-CN/RDS for SQL Server 用户指南/监控与报警/查看资源和引擎监控.md#)

![查看空间状况](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8352/155426074243181_zh-CN.png)

|参数|说明|
|--|--|
|**磁盘空间总体使用量**|所有用户数据库的数据文件和日志文件的大小。|
|**数据空间使用量**|所有用户数据库的数据文件（mdf和ndf文件）的大小。|
|**日志空间使用量**|所有用户数据库的日志文件（ldf文件）。|
|**临时文件空间使用量**|tempdb的所有mdf、ndf和ldf文件的大小。|
|**系统文件空间使用量**|master、msdb和model数据库的数据文件和日志文件，以及SQL Server实例目录下面的一些系统文件（错误日志和dll文件等）的大小。|

**方法二**

通过SQL语句查看所有数据库的数据文件（mdf和ndf文件）和日志文件（ldf文件）的大小，详情请参见[RDS for SQL Server如何查看实例、数据库及表占用的空间大小](cn.zh-CN/常见问题/空间__内存/RDS for SQL Server如何查看实例、数据库及表占用的空间大小.md#)。

## 解决方法 {#section_ecg_2mb_3gb .section}

-   **升级实例的存储空间**

    升级实例存储空间后即可解锁实例，关于如何升级实例存储空间，请参见[变更配置](../../../../../cn.zh-CN/RDS for SQL Server 用户指南/实例管理/变更配置.md#)，若实例存储空间已到最大值，请提交工单联系客服临时解锁实例，再进行后续操作。

-   **日志文件占用量高的解决方法**

    **原因**

    如果应用程序中有大量的大事务操作，就会导致事务日志持续增长，并且有可能会导致超过实例磁盘空间上限而使实例被锁定。

    **解决方法一**

    1.  客户端连接实例后执行如下命令。

        ```
        select name,log_reuse_wait,log_reuse_wait_desc from sys.databases
        ```

    2.  若**log\_reuse\_wait\_desc**的值是**LOG\_BACKUP**，请[收缩事务日志](cn.zh-CN/.md#)。

        **说明：** 若日志文件非常大，日志备份的时间会比较长，并且在收缩日志文件时，如果遇到未提交的事务，会导致单次收缩效果不明显。在单次收缩效果不明显的情况下，建议您再次收缩事务日志。

    **解决方法二**

    事务日志增长过快的根本原因是事务较多或者有大事务。例如，一个事务中操作了500万行数据，在有这种大事务的情况下，建议您将事务拆分，每个事务操作10万行数据，分50次执行。

-   **数据文件占用量高的解决方法**

    如果数据库文件占用空间比较多，可以先检查数据文件的使用率。对于文件大但使用率低的数据库，可以进行相应处理。详细步骤如下：

    1.  执行如下命令，查看数据库的空闲空间。

        ```
        USE <数据库名>
        GO  
        SELECT SUM(unallocated_extent_page_count) AS [free pages],   
        (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
        FROM sys.dm_db_file_space_usage;
        ```

    2.  找到空间使用率较高的数据库，然后执行如下命令，收缩该数据库。

        ```
        DBCC SHRINKDATABASE(<数据库名>)
        ```

        **说明：** 您也可以执行如下命令来收缩单个文件。

        ```
        DBCC SHRINKFILE(file_id,size)
        ```

        **size**为收缩以后的大小，而不是要收缩多少，单位：MB。

-   **临时文件用量高的解决方法**

    您可以从实例监控中初步判定临时文件是否占用太多空间。另外，如果临时文件的空间不够，Error Log中也会有相应的记录。关于如何排查临时文件空间不足的情况，请参见[Troubleshooting Insufficient Disk Space in tempdb](https://technet.microsoft.com/en-us/library/ms176029?spm=a2c4g.11186623.2.25.56d542bdJNQtfe)。

    建议您执行如下操作：

    -   重启实例来快速释放临时文件的空间。
    -   及时释放临时表、行版本、表变量等。

