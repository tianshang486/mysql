# RDS for MySQL 物理备份文件恢复到自建数据库 {#concept_41817_zh .concept}

开源软件Percona Xtrabackup可以用于对数据库进行备份恢复，您可以使用该软件将云数据库MySQL的备份文件恢复到自建数据库中，本文将介绍详细的操作步骤。

**说明：** 

-   通过逻辑备份文件恢复到自建数据库请参见[RDS for MySQL 逻辑备份文件恢复到自建数据库](intl.zh-CN/常见问题/备份__恢复__迁移/RDS for MySQL 逻辑备份文件恢复到自建数据库.md#)。
-   关于云数据库MySQL版如何备份数据，请参见[备份RDS数据](../../../../intl.zh-CN/用户指南/备份数据/备份RDS数据.md#)。
-   由于Percona Xtrabackup不支持Windows，Windows系统下的备份恢复请参见[使用 mysqldump 迁移 MySQL 数据](../../../../intl.zh-CN/用户指南/数据迁移/使用 mysqldump 迁移 MySQL 数据.md#)。

## 注意事项 {#section_bd4_5gz_5fb .section}

本文使用Linux7的操作系统以及MySQL5.7版本为例进行演示。

-   操作系统中已安装数据恢复工具Percona XtraBackup，您可以从Percona XtraBackup官网下载安装。

    MySQL 5.6及之前的版本需要安装 Percona XtraBackup 2.3，安装指导请参见官方文档[Percona XtraBackup 2.3](https://www.percona.com/doc/percona-xtrabackup/2.3/installation.html)。

    MySQL 5.7版本需要安装 Percona XtraBackup 2.4，安装指导请参见官方文档[Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html)。

-   2019年2月20日后创建的MySQL 5.6实例，数据备份文件的格式为xbstream文件包 \(\_qp.xb 后缀\)。
-   本地MySQL数据库安装在64位的Linux系统中，且与云数据库MySQL版的版本相同。

**说明：** 由于软件限制，目前只支持将云数据库MySQL的备份文件恢复到安装在Linux系统中的自建MySQL数据库中。


## 前提条件 {#section_hqi_9kq_hlg .section}

实例版本如下：

-   MySQL 5.7高可用本地盘版
-   MySQL 5.6
-   MySQL 5.5

## 备份恢复操作步骤 {#section_ooe_3fz_r97 .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com)。
2.  在页面左上角，选择实例所在地域。
3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**备份恢复**。
5.  选择数据备份标签页。
6.  选择查询的时间范围，然后单击**查询**。
7.  在数据备份列表中，找到要下载的数据备份，并单击其右侧的**下载**。

    **说明：** 如果没有**下载**按钮，请确认您的实例版本是否支持[下载物理备份文件](../../../../intl.zh-CN/用户指南/备份数据/下载数据备份和日志备份.md#)。

    ![下载数据备份](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8199/156704635047407_zh-CN.png)

8.  在实例备份文件下载窗口，单击**复制外网地址**，获取数据备份文件外网下载地址。

    ![复制外网下载地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8199/156704635047408_zh-CN.png)

9.  登录云服务器ECS。
10. 执行如下命令，下载数据备份文件。

    ``` {#codeblock_8q1_jx0_mvl}
    wget -c '<数据备份文件外网下载地址>' -O <自定义文件名>.tar.gz
    					
    ```

    **说明：** 

    -   -c：启用断点续传模式。
    -   -O：将下载的结果保存为指定的文件（使用URL中包含的文件名后缀 .tar.gz 、.xb.gz 或 \_qp.xb）。
11. 执行如下命令，解压已下载的数据备份文件。

    **说明：** 本文以自定义路径/home/mysql/data为例，您可以根据实际情况将其替换成实际路径。

    目前物理备份集文件有3种格式：

    -   tar 压缩包 （.tar.gz 后缀）
    -   xbstream 压缩包 （.xb.gz 后缀）
    -   xbstream 文件包 \(\_qp.xb 后缀\)
    **说明：** 2019年2月20日后创建的MySQL 5.6实例，数据备份文件的格式为xbstream文件包 \(\_qp.xb 后缀\)。

    对于tar 压缩包 （.tar.gz 后缀），使用命令：

    ``` {#codeblock_xpo_vum_r09}
    tar -izxvf <数据备份文件名>.tar.gz -C /home/mysql/data
    ```

    对于xbstream 压缩包 （.xb.gz 后缀），使用命令：

    ``` {#codeblock_o3v_gfv_syk}
    gzip -d -c <数据备份文件名>.xb.gz | xbstream -x -v -C /home/mysql/data
    ```

    对于xbstream 文件包 \(\_qp.xb 后缀\)，使用命令：

    ``` {#codeblock_y11_9a2_tgq}
    ## 解包
    cat <数据备份文件名>_qp.xb | xbstream -x -v -C /home/mysql/data
    ## 解压
    innobackupex --decompress --remove-original /home/mysql/data
    ```

    **说明：** -C：指定文件要解压到的目录。可选参数，若不指定就解压到当前目录。

12. 执行如下命令，查询解压后生成的文件。

    ``` {#codeblock_0eg_uzq_fls}
    ls -l /home/mysql/data
    					
    ```

    命令执行成功后，系统会返回如下结果，其中蓝色字体为生成备份文件时RDS实例所包含的数据库。

    ![查看解压文件](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8199/156704635047410_zh-CN.jpg)

13. 执行如下命令，恢复解压好的备份文件。

    ``` {#codeblock_1pd_fvx_w4h}
    innobackupex --defaults-file=/home/mysql/data/backup-my.cnf --apply-log /home/mysql/data
    					
    ```

    若系统返回如下类似结果，则说明备份文件已成功恢复到本地数据库。

    ![恢复成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8199/156704635047412_zh-CN.jpg)

    **说明：** 请确保您的Percona XtraBackup版本正确，MySQL 5.6及之前的版本需要安装 Percona XtraBackup 2.3，MySQL 5.7版本需要安装 Percona XtraBackup 2.4，MySQL 8.0版本需要安装 Percona XtraBackup 8.0。

14. 为避免版本问题，需修改backup-my.cnf参数，具体操作步骤如下。
    1.  执行如下命令，以文本方式编辑backup-my.cnf文件。

        ``` {#codeblock_62v_93u_j4y}
        vi /home/mysql/data/backup-my.cnf
        							
        ```

    2.  自建数据库不支持如下参数，需要注释掉。

        ``` {#codeblock_nl2_snh_63t .language-bash}
        #innodb_log_checksum_algorithm
        #innodb_fast_checksum
        #innodb_log_block_size
        #innodb_doublewrite_file
        #rds_encrypt_data
        #innodb_encrypt_algorithm
        #redo_log_version
        #master_key_id
        ```

        **说明：** 

        -   如果本地使用的是MyISAM引擎，和阿里云的InnoDB不兼容，需要多注释掉如下参数并增加skip-grant-tables参数：

            ``` {#codeblock_a4z_eiq_jli}
            #innodb_log_checksum_algorithm=strict_crc32
            #redo_log_version=1
            skip-grant-tables
            ```

        -   如果本地使用的是MyIAM引擎，且对系统表进行操作时报错（存储引擎相关），请按如下操作进行存储引擎的转换：

            ``` {#codeblock_ksm_3u3_jrp}
            alter engine <表名> engine=myisam;
            ```

    3.  按**Esc**键，然后输入`:wq`并回车进行保存。
15. 执行如下命令，修改文件属主，并确定文件所属为MySQL用户。

    ``` {#codeblock_nat_wuy_eou .language-bash}
    chown -R mysql:mysql /home/mysql/data
    					
    ```

16. 执行如下命令，启动MySQL进程。

    ``` {#codeblock_s00_cqo_7pc}
    mysqld_safe --defaults-file=/home/mysql/data/backup-my.cnf --user=mysql --datadir=/home/mysql/data &
    					
    ```

    **说明：** 

    -   如果提示没有找到mysqld\_safe，请确认您的数据库引擎是否为MySQL。
    -   建议您参考[官方文档](https://dev.mysql.com/doc/refman/8.0/en/resetting-permissions.html)重置root账户的密码。
17. 执行如下命令，登录MySQL数据库以验证进程启动成功。

    ``` {#codeblock_o16_aau_cpg}
    mysql -uroot -p<数据库密码>
    					
    ```

    若系统返回如下结果，进程启动成功，则说明已成功执行参数注释和修改文件属主。

    ![启动成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8199/156704635047413_zh-CN.jpg)


