# 迁移 RDS for PostgreSQL 数据到本地 PostgreSQL {#concept_jzm_bzv_ydb .concept}

阿里云数据库 PostgreSQL 版支持通过逻辑备份文件将云上数据迁移到本地数据库。

## 操作步骤 {#section_ysb_qzv_ydb .section}

1.  通过 PostgreSQL 客户端，连接云数据库。
2.  执行如下命令，备份数据。

    ``` {#codeblock_sf7_3t5_jem}
    pg_dump -U username -h hostname -p port databasename -f filename
    ```

    参数说明如下：

    -   username：云数据库用户名
    -   hostname：云数据库主机名
    -   port：云数据库端口号
    -   databasename：要备份的数据库名
    -   filename：要生成的备份文件名称
    例如：

    ``` {#codeblock_b3i_33q_b3s}
    pg_dump -U myuser -h rds2z2tp80v3752wb455.pg.rds.aliyuncs.com -p 3433 pg001 -f pg001.sql
    ```

3.  将备份文件pg001.sql放到目标服务器中。
4.  执行如下命令将数据恢复到本地数据库。

    ``` {#codeblock_03w_5tn_q5s}
    psql -U username -h hostname -d desintationdb -p port -f dumpfilename.sql
    ```

    参数说明如下：

    -   username：本地数据库用户名
    -   hostname：本地数据库地址
    -   port：本地数据库端口号
    -   desintationdb：目的数据库名
    -   dumpfilename：备份文件名称
    如：

    ``` {#codeblock_io8_ukn_5sx}
    psql -U myuser -h localhost -d pg001 -p 5432 -f pg001.sql
    ```

    由于 RDS 数据库的权限设置和本地数据库不一致，在数据导入过程当中可能会出现一些与权限相关的 WARNING 或 ERROR，可以忽略，如：

    ``` {#codeblock_qrh_q0u_6rm}
    WARNING:  no privileges could be revoked for "xxxxx"
    ERROR:  role "xxxxx" does not exist
    ```


