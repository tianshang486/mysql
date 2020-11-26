# RDS MySQL物理备份文件恢复到自建数据库

开源软件Percona Xtrabackup可以用于对数据库进行备份恢复，您可以使用该软件将云数据库MySQL的备份文件恢复到自建数据库中，本文将介绍详细的操作步骤。

**说明：**

-   通过逻辑备份文件恢复到自建数据库请参见[RDS MySQL逻辑备份文件恢复到自建数据库](/cn.zh-CN/RDS MySQL 数据库/恢复/RDS MySQL逻辑备份文件恢复到自建数据库.md)。
-   关于云数据库MySQL版如何备份数据，请参见[备份RDS数据]()。
-   由于Percona Xtrabackup不支持Windows，Windows系统下的备份恢复请参见[使用mysqldump迁移MySQL数据](/cn.zh-CN/RDS MySQL 数据库/数据迁移/从自建数据库迁移至RDS/使用mysqldump迁移MySQL数据.md)。

## 前提条件

-   实例版本如下：

    -   MySQL 8.0高可用版（本地SSD盘）
    -   MySQL 5.7高可用版（本地SSD盘）
    -   MySQL 5.6
    -   MySQL 5.5
    **说明：** 基础版实例仅提供快照备份，无法下载。您可以参见[基础版实例的备份怎么恢复或迁移](#section_ohm_rf7_3mx)。

-   操作系统中已安装数据恢复工具Percona XtraBackup，您可以从Percona XtraBackup官网下载安装。
    -   MySQL 5.6及之前的版本需要安装 Percona XtraBackup 2.3，安装指导请参见官方文档[Percona XtraBackup 2.3](https://www.percona.com/doc/percona-xtrabackup/2.3/installation.html)。
    -   MySQL 5.7版本需要安装 Percona XtraBackup 2.4，安装指导请参见官方文档[Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html)。
    -   MySQL 8.0版本需要安装 Percona XtraBackup 8.0，安装指导请参见官方文档[Percona XtraBackup 8.0](https://www.percona.com/doc/percona-xtrabackup/8.0/installation.html)。
-   innobackupex解压命令需要安装qpress，您可以前往[QuickLZ网站](http://www.quicklz.com/?spm=a2c4g.11186623.2.20.3fe22124ul9npf)，下载qpress工具，然后使用如下命令安装：

    ```
    tar xvf qpress-11-linux-x64.tar
    chmod 775 qpress
    cp qpress /usr/bin
    ```


## 注意事项

本文使用Linux7的操作系统以及MySQL5.7版本为例，演示如何通过外网下载备份文件并恢复数据。

-   2019年2月20日后创建的MySQL 5.6实例，数据备份文件的格式为xbstream文件包（\_qp.xb后缀）。
-   自建MySQL数据库安装在64位的Linux系统中，且与云数据库MySQL版的版本相同。

**说明：** 由于软件限制，目前只支持将云数据库MySQL的备份文件恢复到安装在Linux系统中的自建MySQL数据库中。


## 备份恢复操作步骤

1.  登录[RDS管理控制台](https://rds.console.aliyun.com)。
2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。
3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**备份恢复**。
5.  选择**数据备份**标签页。
6.  选择查询的时间范围。
7.  在数据备份列表中，找到要下载的数据备份，并单击其右侧的**下载**。

    **说明：** 如果没有**下载**按钮，请确认您的实例版本是否支持[下载物理备份文件](/cn.zh-CN/RDS MySQL 数据库/备份/下载数据备份和日志备份.md)。

    ![下载数据备份](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8313729951/p47407.png)

8.  在实例备份文件下载窗口，单击**复制外网地址**旁的![复制图标](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8313729951/p112560.png)，获取数据备份文件外网下载地址。

    ![复制外网下载地址](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8313729951/p47408.png)

9.  登录云服务器ECS。
10. 执行如下命令，下载数据备份文件。

    ```
    wget -c '<数据备份文件外网下载地址>' -O <自定义文件名>.<后缀>
    ```

    示例

    ```
    wget -c 'http://.../hinsxxxx_data_20201123215531_qp.xb?...' -O test1_qp.xb
    ```

    ![下载截图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9660726061/p184686.png)

    **说明：**

    -   -c：启用断点续传模式。
    -   -O：将下载的结果保存为指定的文件（使用URL中包含的文件名后缀 .tar.gz 、.xb.gz 或 \_qp.xb）。
11. 执行如下命令，解压已下载的数据备份文件。

    **说明：** 本文以自定义路径/home/mysql/data为例，您可以根据实际情况将其替换成实际路径。创建/home/mysql/data目录的命令为`mkdir -p /home/mysql/data`。

    目前物理备份集文件有3种格式：

    -   tar 压缩包 （.tar.gz 后缀）
    -   xbstream 压缩包 （.xb.gz 后缀）
    -   xbstream 文件包（\_qp.xb 后缀）
    **说明：** 2019年2月20日后创建的MySQL 5.6实例，数据备份文件的格式为xbstream文件包（\_qp.xb 后缀）。

    -   对于tar 压缩包 （.tar.gz 后缀），使用命令：

        ```
        tar -izxvf <数据备份文件名> -C /home/mysql/data
        ```

        示例

        ```
        tar -izxvf test1.tar.gz -C /home/mysql/data
        ```

    -   对于xbstream 压缩包 （.xb.gz 后缀），使用命令：

        ```
        gzip -d -c <数据备份文件名> | xbstream -x -v -C /home/mysql/data
        ```

        示例

        ```
        gzip -d -c test1.xb.gz | xbstream -x -v -C /home/mysql/data
        ```

    -   对于xbstream 文件包（\_qp.xb 后缀），使用命令：

        ```
        ## 解包
        cat <数据备份文件名> | xbstream -x -v -C /home/mysql/data
        
        ## MySQL 5.6/5.7解压
        innobackupex --decompress --remove-original /home/mysql/data
        ## MySQL 8.0解压
        xtrabackup --decompress --remove-original --target-dir=/home/mysql/data
                            
        ```

        示例

        ```
        ## 解包
        cat test1_qp.xb | xbstream -x -v -C /home/mysql/data
        
        ## MySQL 5.6/5.7解压
        innobackupex --decompress --remove-original /home/mysql/data
        ## MySQL 8.0解压
        xtrabackup --decompress --remove-original --target-dir=/home/mysql/data
                            
        ```

    **说明：** -C：指定文件要解压到的目录。可选参数，若不指定就解压到当前目录。

12. 执行如下命令，查询解压后生成的文件。

    ```
    ls -l /home/mysql/data
    ```

    命令执行成功后，系统会返回如下结果，其中蓝色字体为生成备份文件时RDS实例所包含的数据库。

    ![查看解压文件](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8313729951/p47410.jpg)

13. 执行如下命令，恢复解压好的备份文件。

    ```
    ## MySQL 5.6/5.7
    innobackupex --defaults-file=/home/mysql/data/backup-my.cnf --apply-log /home/mysql/data
    
    ## MySQL 8.0
    xtrabackup --prepare --target-dir=/home/mysql/data
    xtrabackup --datadir=/var/lib/mysql --copy-back --target-dir=/home/mysql/data
    ```

    若系统返回如下类似结果，则说明备份文件已成功恢复到自建数据库。

    ![恢复成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8313729951/p47412.jpg)

    **说明：** 请确保您的Percona XtraBackup版本正确：

    -   MySQL 5.6及之前的版本需要安装 Percona XtraBackup 2.3，安装指导请参见官方文档[Percona XtraBackup 2.3](https://www.percona.com/doc/percona-xtrabackup/2.3/installation.html)。
    -   MySQL 5.7版本需要安装 Percona XtraBackup 2.4，安装指导请参见官方文档[Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html)。
    -   MySQL 8.0版本需要安装 Percona XtraBackup 8.0，安装指导请参见官方文档[Percona XtraBackup 8.0](https://www.percona.com/doc/percona-xtrabackup/8.0/installation.html)。
14. 为避免版本问题，需修改backup-my.cnf参数，具体操作步骤如下。
    1.  执行如下命令，以文本方式编辑backup-my.cnf文件。

        ```
        vi /home/mysql/data/backup-my.cnf
        ```

    2.  自建数据库不支持如下参数，需要注释掉。

        ```
        #innodb_log_checksum_algorithm
        #innodb_fast_checksum
        #innodb_log_block_size
        #innodb_doublewrite_file
        #innodb_encrypt_algorithm
        #rds_encrypt_data
        #redo_log_version
        #master_key_id
        #server_uuid
        ```

        **说明：**

        -   如果自建数据库使用的是MyISAM引擎，和阿里云的InnoDB不兼容，需要多注释掉如下参数并增加skip-grant-tables参数：

            ```
            #innodb_log_checksum_algorithm=strict_crc32
            #redo_log_version=1
            skip-grant-tables
            ```

        -   如果自建数据库使用的是MyIAM引擎，且对系统表进行操作时报错（存储引擎相关），请按如下操作进行存储引擎的转换：

            ```
            alter table <表名> engine=myisam;
            ```

    3.  按**Esc**键，然后输入`:wq`并回车进行保存。
15. 执行如下命令，修改文件属主，并确定文件所属为MySQL用户。

    ```
    chown -R mysql:mysql /home/mysql/data
    ```

16. 执行如下命令，启动MySQL进程。

    ```
    mysqld --defaults-file=/home/mysql/data/backup-my.cnf --user=mysql --datadir=/home/mysql/data &
    ```

    **说明：** 建议您参考[官方文档](https://dev.mysql.com/doc/refman/8.0/en/resetting-permissions.html)重置root账户的密码。

    常见错误

    如果报如下错误，请在/home/mysql/data/backup-my.cnf文件中添加`lower_case_table_names=1`。

    ![报错](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7719536061/p185240.png)

17. 执行如下命令，登录MySQL数据库以验证进程启动成功。

    ```
    mysql -u<源RDS实例账号> -p<对应密码>
    ```

    您可以使用`show databases;`查看数据库，确认是否恢复成功。

    ![启动成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7719536061/p47413.jpg)


## 常见问题

-   除了下载备份文件恢复之外，还有其他方法可以将实例的数据快速恢复到自建数据库吗？

    您可以使用DTS将[RDS MySQL迁移至自建MySQL](https://help.aliyun.com/document_detail/144555.html)。

-   为什么下载数据备份文件会报错？

    使用`wget -c '<数据备份文件外网下载地址>' -O <自定义文件名>.tar.gz`命令下载时用2个英文单引号（'）将下载地址包含起来，便于程序识别具体的地址，防止出错。

-   下载的备份文件解压缩报错怎么办？
    1.  确认您下载的文件是否为物理备份文件。
    2.  压缩文件保存的名称后缀是否正确（使用URL中包含的文件名后缀 .tar.gz 、.xb.gz 或 \_qp.xb）。
    3.  针对不同格式的压缩文件，使用正确的解压命令。详情请参见本文操作步骤第11步。
-   基础版实例的备份怎么恢复或迁移呢？

    基础版实例仅支持快照备份，您可以使用以下方法：

    -   [使用mysqldump迁移MySQL数据](/cn.zh-CN/RDS MySQL 数据库/数据迁移/从自建数据库迁移至RDS/使用mysqldump迁移MySQL数据.md)
    -   用DTS将数据从RDS导出到本地
-   下载的备份能恢复到另一个RDS MySQL实例上吗？

    暂不支持此操作。建议您使用DTS[迁移RDS实例数据到另一个RDS实例](https://help.aliyun.com/document_detail/26626.html)上。


## 相关文档

-   [恢复MySQL数据](/cn.zh-CN/RDS MySQL 数据库/恢复/恢复MySQL数据.md)
-   [MySQL单库单表恢复](/cn.zh-CN/RDS MySQL 数据库/恢复/MySQL单库单表恢复.md)
-   [跨地域恢复数据](/cn.zh-CN/RDS MySQL 数据库/恢复/跨地域恢复数据.md)

