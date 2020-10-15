# 使用mysqldump迁移MySQL数据

使用mysqldump工具的优点是简单易用、容易上手，缺点是停机时间较长，因此它适用于数据量不大，或者允许停机的时间较长的情况。

## 背景信息

由于RDS提供的关系型数据库服务与原生的数据库服务完全兼容，所以对用户来说，将原有数据库迁移到RDS实例的过程，与从一台MySQL服务器迁移到另外一台MySQL服务器的过程基本类似。

**说明：** mysqldump迁移复杂，建议您使用DTS迁移数据，详情请参见[DTS数据迁移方案概览](/cn.zh-CN/数据迁移/DTS数据迁移方案概览.md)。

## 注意事项

迁移后的表不区分大小写，统一变为小写。

## 前提条件

-   已对RDS实例设置白名单，申请外网地址，以及创建数据库和账号。具体可参见[快速入门](/cn.zh-CN/RDS MySQL 数据库/快速入门/使用流程.md)。
-   已购买云服务器 ECS。

## 操作步骤

在正式迁移之前，需要先在本地数据库中创建迁移账号，并将要迁移的数据库的读写权限授权给迁移账号。

1.  在本地数据库中创建迁移账号。

    ```
    CREATE USER'username'@'host' IDENTIFIED BY 'password';
    ```

    参数说明：

    -   username：要创建的账号。
    -   host：指定该账号登录数据库的主机。如果是本地用户可以使用localhost，如果想让该用户从任意主机登录，可以使用通配符%。
    -   password：该账号的登录密码。
    例：要创建账号为William，密码为Changme123的账号从任意主机登录本地数据库，命令如下：

    ```
    CREATE USER'William'@'%' IDENTIFIED BY 'Changme123';
    ```

2.  在本地数据库中给迁移账号授权。

    ```
    GRANT SELECT ON databasename.tablename TO 'username'@'host' WITH GRANT OPTION;
    GRANT REPLICATION SLAVE ON databasename.tablename TO 'username'@'host' WITH GRANT OPTION;
    ```

    参数说明：

    -   SELECT、REPLICATION SLAVE：该账号的权限，如果要授权所有权限，使用ALL。
    -   databasename：数据库名。如果要授权该账号所有的数据库权限，则使用通配符\*。
    -   tablename：表名。如果要授权该账号所有的表权限，则使用通配符\*。
    -   username：要授权的账号名。
    -   host：授权登录数据库的主机名。如果是本地用户可以使用localhost，如果想让该用户从任意主机登录，可以使用通配符%。
    -   WITH GRANT OPTION：授权该账号能使用GRANT命令，该参数为可选。
    例：授权账号William对所有数据库和表的所有权限，并可以从任意主机登录本地数据库，命令如下。

    ```
    GRANT ALL ON*.* TO 'William'@'%';
    ```

3.  使用mysqldump将本地数据库数据导出为数据文件。

    **说明：** 导出期间请勿进行数据更新。本步骤仅仅导出数据，不包括存储过程、触发器及函数。

    ```
    mysqldump -h localIp -u userName -p --opt --default-character-set=utf8 --hex-blob dbName --skip-triggers --skip-lock-tables > /tmp/dbName.sql
    ```

    参数说明：

    -   localIp：本地数据库服务器IP地址。
    -   userName：本地数据库的迁移账号。
    -   dbName：需要迁移的数据库名。
    -   /tmp/dbName.sql：备份生成的文件名。
4.  使用mysqldump导出存储过程、触发器和函数。

    **说明：** 若数据库中没有使用存储过程、触发器和函数，可跳过此步骤。在导出存储过程、触发器和函数时，需要将definer去掉，以兼容RDS。

    ```
    mysqldump -h localIp -u userName -p --opt --default-character-set=utf8 --hex-blob dbName -R | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' > /tmp/triggerProcedure.sql
    ```

    参数说明：

    -   localIp：本地数据库服务器IP地址。
    -   userName：本地数据库的迁移账号。
    -   dbName：需要迁移的数据库名。
    -   /tmp/triggerProcedure.sql：备份生成的文件名。
5.  将数据文件和存储过程文件上传到ECS上。

    本例以文件上传到如下路径为例。

    ```
    /tmp/dbName.sql
    /tmp/triggerProcedure.sql
    ```

6.  登录ECS，将数据文件和存储过程文件导入到目标RDS中。

    ```
    mysql -h intranet4example.mysql.rds.aliyuncs.com -u userName -p dbName < /tmp/dbName.sql
    mysql -h intranet4example.mysql.rds.aliyuncs.com -u userName -p dbName < /tmp/triggerProcedure.sql
    ```

    参数说明：

    -   intranet4example.mysql.rds.aliyuncs.com：RDS实例连接地址，本例以内网地址为例。
    -   userName：RDS数据库的高权限账号或具有读写权限的账号。
    -   dbName：需要导入的数据库名。
    -   /tmp/dbName.sql：要导入的数据文件名。
    -   /tmp/triggerProcedure.sql：要导入的存储过程文件名。

## 常见问题

`OPERATION need to be executed set by ADMIN`报错怎么解决？

答：可能是SQL脚本里面包括视图，触发器，存储过程等对象的definer问题，或者含有set global类SQL导致。详情请参见[RDS MySQL出现“OPERATION need to be executed set by ADMIN”报错](~~41701~~)。

