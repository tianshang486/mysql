# 使用 psql 命令迁移自建PostgreSQL 数据库数据 {#concept_qhq_gbw_ydb .concept}

本例介绍通过 psql 命令将 PostgreSQL 数据备份文件恢复到目标 RDS 中。

## 背景信息 {#section_rdh_5bw_ydb .section}

PostgreSQL 支持逻辑备份。我们使用 pg\_dump 逻辑备份功能，导出备份文件，再通过 psql 导入到 RDS 中，实现将 PostgreSQL 的数据导入到 RDS 中。

## 前提条件 {#section_pbc_vbw_ydb .section}

已完成 RDS 实例数据库的准备，可参见[申请外网地址](../../../../intl.zh-CN/RDS for PostgreSQL 快速入门/初始化配置/申请外网地址.md#)和[创建账号和数据库](../../../../intl.zh-CN/RDS for PostgreSQL 快速入门/初始化配置/创建账号和数据库.md#)。

## 准备本地数据 {#section_us5_vbw_ydb .section}

1.  通过 PostgreSQL 客户端，连接本地 PostgreSQL 数据库。
2.  执行如下命令，备份数据。

    ```
    pg_dump -U username -h hostname -p port databasename -f filename
    ```

    参数说明如下：

    -   username：本地数据库用户名
    -   hostname：本地数据库主机名，如果是在本地数据库主机登录，可以使用 *localhost*
    -   port：本地数据库端口号
    -   databasename：要备份的本地数据库名
    -   filename：要生成的备份文件名称
    例如，数据库用户 William 要备份本地 PostgreSQL 数据库，登录 PostgreSQL 主机后，通过如下命令备份数据。

    ```
    pg_dump -U William -h localhost -p 3433 pg001 -f pg001.sql
    ```


## 正式迁移操作 {#section_d1b_1cw_ydb .section}

**说明：** 通过 RDS 内网恢复数据，网络更稳定，数据更安全。建议您将数据上传到云服务器 ECS 上，然后通过内网将数据恢复到目标 RDS上。如果数据文件太大，可以先压缩后再上传。本例以该方式为例进行说明。

1.  登录云服务器 ECS。
2.  通过 PostgreSQL 客户端，执行如下命令将数据导入到 RDS 中。

    ```
    psql -U username -h hostname -d desintationdb -p port -f dumpfilename.sql
    ```

    参数说明如下：

    -   username：RDS 上的 PostgreSQL 数据库用户名
    -   hostname：RDS 上的 PostgreSQL 数据库地址
    -   port：RDS 上的 PostgreSQL 数据库端口号
    -   databasename：RDS 上的 PostgreSQL 数据库名
    -   filename：本地备份数据文件名
    如：

    ```
    psql -U William -h postgresql.rds.aliyuncs.com -d pg001 -p 3433 -f pg001.sql
    ```

    由于 RDS 数据库的权限设置和本地数据库不一致，在数据导入过程当中可能会出现一些与权限相关的 WARNING 或 ERROR，可以忽略，如：

    ```
    WARNING:  no privileges could be revoked for "xxxxx"
    ERROR:  role "xxxxx" does not exist
    ```


