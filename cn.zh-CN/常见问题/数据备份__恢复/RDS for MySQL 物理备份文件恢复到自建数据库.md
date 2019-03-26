# RDS for MySQL 物理备份文件恢复到自建数据库 {#concept_41817_zh .concept}

开源软件Percona Xtrabackup可以用于对数据库进行备份恢复，您可以使用该软件将云数据库MySQL的备份文件恢复到自建数据库中，本文将介绍详细的操作步骤。

**说明：** 

-   通过逻辑备份文件恢复到自建数据库请参见[RDS for MySQL 逻辑备份文件恢复到自建数据库](intl.zh-CN/常见问题/数据备份__恢复/RDS for MySQL 逻辑备份文件恢复到自建数据库.md#)。
-   关于云数据库MySQL版如何备份数据，请参见[备份 RDS 数据](../../../../../intl.zh-CN/用户指南/备份数据/备份 RDS 数据.md#)。
-   由于Percona Xtrabackup不支持Windows，Windows系统下的备份恢复请参见[使用 mysqldump 迁移 MySQL 数据](../../../../../intl.zh-CN/RDS for MySQL 用户指南/数据迁移/使用 mysqldump 迁移 MySQL 数据.md#)。

## 注意事项 {#section_bd4_5gz_5fb .section}

本文使用Linux7的操作系统以及MySQL5.7版本为例进行演示。

-   2019年2月20日后创建的MySQL 5.6实例，数据备份文件的格式为xbstream文件包 \(\_qp.xb 后缀\)。
-   本地MySQL数据库安装在64位的Linux系统中，且与云数据库MySQL版的版本相同。

**说明：** 由于软件限制，目前只支持将云数据库MySQL的备份文件恢复到安装在Linux系统中的自建MySQL数据库中。

-   操作系统中已安装数据恢复工具Percona XtraBackup。MySQL 5.6及之前的版本需要安装 Percona XtraBackup 2.3。MySQL 5.7版本需要安装 Percona XtraBackup 2.4。可以从Percona XtraBackup官网下载安装，安装指导请参见官方文档 [Percona XtraBackup 2.3](https://www.percona.com/doc/percona-xtrabackup/2.3/installation.html)、[Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html)。

## 备份恢复操作步骤 { .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com)。
2.  在页面左上角，选择实例所在地域。
3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**备份恢复**。
5.  选择数据备份标签页。
6.  选择查询的时间范围，然后单击**查询**。
7.  在数据备份列表中，找到要下载的数据备份，并单击其右侧的**下载**。

    ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/41817/cn_zh/1501083530582/%E4%B8%8B%E8%BD%BD%E6%95%B0%E6%8D%AE%E5%A4%87%E4%BB%BD.png)

8.  在实例备份文件下载窗口，单击**复制外网地址**，获取数据备份文件外网下载地址。

    ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/41817/cn_zh/1501083680218/%E5%A4%8D%E5%88%B6%E5%A4%96%E7%BD%91%E4%B8%8B%E8%BD%BD%E5%9C%B0%E5%9D%80.png)

9.  登录云服务器ECS。
10. 执行如下命令，下载数据备份文件。

    ```
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

    ```
    tar -izxvf <数据备份文件名>.tar.gz -C /home/mysql/data
    ```

    对于xbstream 压缩包 （.xb.gz 后缀），使用命令：

    ```
    gzip -d -c <数据备份文件名>.xb.gz | xbstream -x -v -C /home/mysql/data
    ```

    对于xbstream 文件包 \(\_qp.xb 后缀\)，使用命令：

    ```
    ## 解包
    cat <数据备份文件名>_qp.xb | xbstream -x -v -C /home/mysql/data
    ## 解压
    innobackupex --decompress --remove-original /home/mysql/data
    ```

    **说明：** -C：指定文件要解压到的目录。可选参数，若不指定就解压到当前目录。

12. 执行如下命令，查询解压后生成的文件。

    ```
    ls -l /home/mysql/data
    
    ```

    命令执行成功后，系统会返回如下结果，其中蓝色字体为生成备份文件时RDS实例所包含的数据库。

    ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/41817/cn_zh/1500456508697/%E6%9F%A5%E7%9C%8B%E8%A7%A3%E5%8E%8B%E6%96%87%E4%BB%B6.jpg)

13. 执行如下命令，恢复解压好的备份文件。

    ```
    innobackupex --defaults-file=/home/mysql/data/backup-my.cnf --apply-log /home/mysql/data
    
    ```

    若系统返回如下类似结果，则说明备份文件已成功恢复到本地数据库。

    ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/41817/cn_zh/1500455730336/%E6%81%A2%E5%A4%8D%E6%88%90%E5%8A%9F.jpg)

14. 为避免版本问题，需修改backup-my.cnf参数，具体操作步骤如下。
    1.  执行如下命令，以文本方式编辑backup-my.cnf文件。

        ```
        vi /home/mysql/data/backup-my.cnf
        
        ```

    2.  执行如下命令，注释掉如下参数。

        ```language-bash
        #innodb_fast_checksum
        #innodb_page_size
        #innodb_log_block_size
        
        ```

        **说明：** 如果本地使用的是MyISAM引擎，和阿里云的InnoDB不兼容，需要多注释掉如下参数并增加skip-grant-tables参数：

        ```
        #innodb_log_checksum_algorithm=strict_crc32
        #redo_log_version=1
        skip-grant-tables
        ```

    3.  按**Esc**键，然后输入`:wq`并回车进行保存。
15. 执行如下命令，修改文件属主，并确定文件所属为MySQL用户。

    ```language-bash
    chown -R mysql:mysql /home/mysql/data
    
    ```

16. 执行如下命令，启动MySQL进程。

    ```
    mysqld_safe --defaults-file=/home/mysql/data/backup-my.cnf --user=mysql --datadir=/home/mysql/data &
    
    ```

17. 执行如下命令，登录MySQL数据库以验证进程启动成功。

    ```
    mysql -uroot -p<数据库密码>
    
    ```

    若系统返回如下结果，进程启动成功，则说明已成功执行参数注释和修改文件属主。

    ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/41817/cn_zh/1500458262047/%E5%90%AF%E5%8A%A8%E6%88%90%E5%8A%9F.jpg)


