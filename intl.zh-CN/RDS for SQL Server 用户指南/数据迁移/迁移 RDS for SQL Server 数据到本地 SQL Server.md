# 迁移 RDS for SQL Server 数据到本地 SQL Server {#concept_dqz_lyv_ydb .concept}

阿里云数据库 SQL Server 版支持通过物理备份文件将云上数据迁移到本地数据库。

除了本文介绍的迁移方法外，您还可以使用数据传输服务DTS（Data Transmission Service），将RDS for SQL Server增量迁移至自建SQL Server。详情请参见[迁移RDS for SQL Server至本地SQL Server](https://help.aliyun.com/document_detail/126227.html)。

## 操作步骤 {#section_eyt_dzv_ydb .section}

1.  下载云数据库全量和增量物理备份文件并上传至目标服务器。

    备份文件获取方法请参见 [下载数据备份和日志备份](intl.zh-CN/RDS for SQL Server 用户指南/备份数据/下载数据备份和日志备份.md#)。

    如果目标服务器可以访问源实例，您也可以使用`wget "url"`下载备份文件。其中 url 为备份文件下载地址。

2.  下载完成后，解压全量物理备份文件和增量物理备份文件。

    **说明：** 由于解压后的全量和增量文件名相同，建议按**数据库名+备份方式+日期**的规则进行重命名，方便后续维护，例如：

    -   **testdb\_datafull\_201901071320.bak**，datafull代表全量备份。
    -   **testdb\_datadiff\_201901071330.bak**，datadiff代表增量备份。
3.  获取解压后的全量备份文件和增量备份文件，本例以如下路径为例。
    -   全量备份文件存放路径：/tmp/testdb\_datafull\_201901071320.bak
    -   增量备份文件存放路径：/tmp/testdb\_datadiff\_201901071330.bak
4.  登录本地 SQL Server 控制台，通过备份文件查询云数据库的文件逻辑名。

    ``` {#codeblock_cob_bot_fwe}
    restore filelistonly from disk='/tmp/testdb_datafull_201901071320.bak'  
    go
    ```

    系统显示如下，红框中为数据文件逻辑名testdb 和日志文件逻辑名testdb\_log。

    ![数据和日志文件](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41615/156888692336252_zh-CN.png)

5.  加载全量备份文件。

    ``` {#codeblock_f62_2cv_l0v}
    restore database testdb from disk='/tmp/testdb_datafull_201901071320.bak' with   replace,norecovery,stats=10,  
    move 'testdb' to '/var/opt/mssql/data/testdb.mdf',  
    move 'testdb_log' to '/var/opt/mssql/data/testdb_log.ldf'  
    go
    ```

    **说明：** 

    -   /var/opt/mssql/data/testdb.mdf 为数据地址，testdb.mdf为数据文件逻辑名。
    -   /var/opt/mssql/data/testdb\_log.ldf 为日志地址，testdb\_log.ldf为日志文件逻辑名。
    在目的数据库的**属性** \> **文件**中可以查看到目的的数据地址和日志地址。

    ![目的数据库文件路径](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41615/156888692436253_zh-CN.png)

    执行完成后，数据库testdb将显示正在还原状态。

    **说明：** 如果只需恢复全量备份数据，无需执行步骤 6，请直接跳至步骤 7。如果还需要恢复增量备份数据，请执行步骤 6。

6.  加载增量备份文件。

    ``` {#codeblock_kvo_a1i_mn9}
    restore database testdb from disk='/tmp/testdb_datadiff_201901071330.bak' with   replace,norecovery,stats=10,  
    move 'testdb' to '/var/opt/mssql/data/testdb.mdf',  
    move 'testdb_log' to '/var/opt/mssql/data/testdb_log.ldf'
    go
    ```

    执行完成后，数据库testdb将显示正在还原状态。

7.  恢复数据库。

    ``` {#codeblock_mey_s62_oij}
    restore database testdb with recovery  
    go
    ```

    执行完成后，数据库testdb将显示可用状态。


