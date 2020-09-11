# 迁移RDS PostgreSQL数据到本地PostgreSQL

阿里云数据库PostgreSQL版支持通过逻辑备份文件将云上数据迁移到本地数据库。

## 操作步骤

1.  通过[PostgreSQL客户端](https://www.pgadmin.org/download/)，连接云数据库。
2.  执行如下命令，备份数据。

    ```
    pg_dump -U username -h hostname -p port databasename -f filename --exclude-table=public.ha_health_check
    ```

    参数说明如下：

    -   username：云数据库用户名。
    -   hostname：云数据库主机名。
    -   port：云数据库端口号。
    -   databasename：要备份的数据库名。
    -   filename：要生成的备份文件名称。
    -   --exclude-table=public.ha\_health\_check：用于跳过高可用检查表。
    示例

    ```
    pg_dump -U myuser -h rds2z2tp80v3752wb455.pg.rds.aliyuncs.com -p 3433 pg001 -f pg001.sql --exclude-table=public.ha_health_check
    ```

3.  将备份文件pg001.sql上传到目标服务器中。
4.  执行如下命令将数据恢复到本地数据库。

    ```
    psql -U username -h hostname -d desintationdb -p port -f dumpfilename.sql
    ```

    参数说明如下：

    -   username：本地数据库用户名。
    -   hostname：本地数据库地址。
    -   port：本地数据库端口号。
    -   desintationdb：目的数据库名。
    -   dumpfilename：备份文件名称。
    示例

    ```
    psql -U myuser -h localhost -d pg001 -p 5432 -f pg001.sql
    ```

    由于 RDS 数据库的权限设置和本地数据库不一致，在数据导入过程当中可能会出现一些与权限相关的 WARNING 或 ERROR，可以忽略，例如：

    ```
    WARNING:  no privileges could be revoked for "xxxxx"
    ERROR:  role "xxxxx" does not exist
    ```


