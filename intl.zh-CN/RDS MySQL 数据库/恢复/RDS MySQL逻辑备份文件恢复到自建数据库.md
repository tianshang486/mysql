# RDS MySQL逻辑备份文件恢复到自建数据库

使用MySQL自带的mysqldump工具可以通过逻辑备份文件恢复数据库，本文将介绍详细的逻辑备份恢复数据库操作步骤。

实例版本如下：

-   MySQL 8.0高可用本地盘版
-   MySQL 5.7高可用本地盘版
-   MySQL 5.6
-   MySQL 5.5

**说明：**

-   通过物理备份文件恢复到自建数据库请参见[RDS MySQL物理备份文件恢复到自建数据库](/intl.zh-CN/RDS MySQL 数据库/恢复/RDS MySQL物理备份文件恢复到自建数据库.md)。
-   关于云数据库MySQL版如何备份数据，请参见[备份RDS数据]()。

## 演示环境

本地MySQL数据库安装在64位的Linux系统中，且与云数据库MySQL版的版本相同。本文使用Linux7的操作系统以及MySQL5.7版本为例进行演示。

## 逻辑备份恢复操作步骤

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏中单击**备份恢复**。

5.  选择查询的时间范围，然后单击**确定**。

6.  在数据备份列表中，找到要下载的逻辑备份，并单击其右侧的**下载**。

    **说明：** 如果没有**下载**按钮，请确认您的实例版本是否支持[下载逻辑备份文件](/intl.zh-CN/RDS MySQL 数据库/备份/下载数据备份和日志备份.md)。

7.  在实例备份文件下载窗口，单击**复制外网地址**最右侧的![复制图标](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9313729951/p130030.png)，获取数据备份文件外网下载地址。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9313729951/p32292.png)

8.  登录自建数据库所在Linux系统，执行如下命令下载逻辑备份文件。

    ```
    wget -c '<数据备份文件外网下载地址>' -O <自定义文件名>.tar
    ```

    **说明：**

    -   -c：启用断点续传模式。
    -   -O：将下载的结果保存为指定的文件。
9.  执行如下命令解压缩逻辑备份文件，包括系统默认的数据库压缩文件以及自行创建的数据库压缩文件。

    ```
    tar xvf <数据备份文件名>.tar
    ```

10. 根据需要恢复的数据库再次解压缩对应的数据库压缩文件。

    ```
    gzip -d <数据库压缩文件名>.gz
    ```

11. 登录数据库创建对应的空数据库。命令如下：

    ```
    mysql -u root -p<数据库密码>
    create database <数据库名>;
    exit
    ```

12. 使用如下命令将.sql文件导入对应数据库。

    ```
    mysql -u root -p<数据库密码> <创建的空数据库名> < ~/<解压缩后数据库名\>.sql
    ```

13. 登录数据库后查看表，已经有了数据，说明已经迁移成功。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9313729951/p32293.png)


## 常见问题

为什么实例没有逻辑备份？

系统发起的备份默认为物理备份，如果需要逻辑备份，需要手动发起备份。详情请参见[手动备份MySQL数据](/intl.zh-CN/RDS MySQL 数据库/备份/备份MySQL数据.md)。

