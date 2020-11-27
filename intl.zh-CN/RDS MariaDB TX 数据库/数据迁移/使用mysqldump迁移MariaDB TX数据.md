# 使用mysqldump迁移MariaDB TX数据

使用mysqldump工具可以迁移数据库，本文将介绍详细的操作步骤。

## 背景信息

由于RDS提供的关系型数据库服务与原生的数据库服务完全兼容，所以对用户来说，将原有数据库迁移到RDS实例的过程，与从一个MariaDB服务器迁移到另外一台MariaDB服务器的过程基本类似。

本文以本地Linux7和MariaDB 10.2.4版本为例，演示如何从本地迁移到RDS MariaDB TX。

## 注意事项

迁移后的表不区分大小写，统一变为小写。

## 前提条件

已对RDS实例[设置白名单](/intl.zh-CN/RDS MariaDB TX 数据库/快速入门/设置白名单.md)和[申请外网地址](/intl.zh-CN/RDS MariaDB TX 数据库/数据库连接/申请或释放外网地址.md)。

## 操作步骤

1.  使用远程工具[登录RDS MariaDB TX实例](/intl.zh-CN/RDS MariaDB TX 数据库/快速入门/连接MariaDB实例.md)，创建空数据库（例如test001）。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0803377951/p40891.png)

2.  登录本地Linux服务器，使用自带的mysqldump工具将本地数据库数据导出为数据文件。

    ```
    mysqldump -h localhost -u <本地数据库用户名> -p --opt --default-character-set=utf8 --hex-blob <想要迁移的数据库名> --skip-triggers > /tmp/<想要迁移的数据库名>.sql
    ```

    示例

    ```
    mysqldump -h localhost -u root -p --opt --default-character-set=utf8 --hex-blob testdb --skip-triggers > /tmp/testdb.sql
    ```

    **说明：** 导出期间请勿进行数据更新。本步骤仅仅导出数据，不包括存储过程、触发器及函数。

3.  使用 mysqldump 导出存储过程、触发器和函数。

    ```
    mysqldump -h localhost -u <本地数据库用户名> -p --opt --default-character-set=utf8 --hex-blob <想要迁移的数据库名> -R | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' > /tmp/<想要迁移的数据库名>_trigger.sql
    ```

    示例

    ```
    mysqldump -h localhost -u root -p --opt --default-character-set=utf8 --hex-blob testdb -R | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' > /tmp/testdb_trigger.sql
    ```

    **说明：** 若数据库中没有使用存储过程、触发器和函数，可跳过此步骤。在导出存储过程、触发器和函数时，需要将definer去掉，以兼容RDS。

4.  通过如下命令将数据文件和存储过程文件导入到目标 RDS 中。

    ```
    mysql -h <RDS实例外网地址> -P <RDS实例外网端口> -u <RDS实例高权限账号> -p <RDS上数据库名> < /tmp/<想要迁移的数据库名>.sql
    mysql -h <RDS实例外网地址> -P <RDS实例外网端口> -u <RDS实例高权限账号> -p <RDS上数据库名> < /tmp/<想要迁移的数据库名>trigger.sql
    ```

    示例

    ```
    mysql -h rm-bpxxxxx.mariadb.rds.aliyuncs.com -P 3306 -u testuser -p test001 < /tmp/testdb.sql
    mysql -h rm-bpxxxxx.mariadb.rds.aliyuncs.com -P 3306 -u testuser -p test001 < /tmp/testdb_trigger.sql
    ```

5.  刷新远程工具后查看表，已经有了数据，说明已经迁移成功。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1803377951/p40892.png)


