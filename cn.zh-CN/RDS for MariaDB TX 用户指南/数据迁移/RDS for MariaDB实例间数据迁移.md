# RDS for MariaDB实例间数据迁移 {#concept_287066 .concept}

DTS暂不支持迁移MariaDB实例，因此RDS for MariaDB实例间的数据迁移可以使用mysqldump工具，本文将介绍详细的操作步骤。

## 背景信息 {#section_ivh_3w1_wfb .section}

本文以MariaDB 10.3版本为例，演示RDS for MariaDB实例间的数据迁移。

## 前提条件 {#section_bd4_5gz_5fb .section}

-   本地主机或阿里云ECS实例安装Linux7系统并安装MySQL 5.7。
-   两个RDS for MariaDB实例[设置白名单](../cn.zh-CN/RDS for MariaDB TX 快速入门/初始化配置/设置白名单.md#)放通Linux7所在主机或实例的外网IP地址。
-   两个RDS for MariaDB实例都已[申请外网地址](../cn.zh-CN/RDS for MariaDB TX 快速入门/初始化配置/申请外网地址.md#)。

## 操作步骤 {#section_lcm_tqt_vfb .section}

1.  使用客户端工具[登录目的MariaDB实例](../cn.zh-CN/RDS for MariaDB TX 快速入门/连接实例.md#)，创建空数据库。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64517/155860348540891_zh-CN.png)

2.  在Linux7使用自带的mysqldump工具将源MariaDB实例的数据库导出为数据文件。

    ```
    mysqldump -h <源实例外网地址> -P <源实例端口> -u <源实例高权限账号> -p<源实例高权限账号密码> --opt --default-character-set=utf8 --hex-blob <要迁移的数据库名称> --skip-triggers > /tmp/<要迁移的数据库名称>.sql
    ```

    **示例**

    ``` {#codeblock_ibm_0dq_a0v}
    mysqldump -h rm-xxx.mariadb.rds.aliyuncs.com -P 3306 -u test -pTestxxx --opt --default-character-set=utf8 --hex-blob testdb --skip-triggers > /tmp/testdb.sql
    ```

    **说明：** 导出期间请勿进行数据更新。本步骤仅导出数据，不包括存储过程、触发器及函数。

3.  使用mysqldump导出存储过程、触发器和函数。

    ```
    mysqldump -h <源实例外网地址> -P <源实例端口> -u <源实例高权限账号> -p<源实例高权限账号密码> --opt --default-character-set=utf8 --hex-blob <要迁移的数据库名称> -R > /tmp/<要迁移的数据库名称>trigger.sql
    ```

    **示例**

    ``` {#codeblock_r19_wex_az4}
    mysqldump -h rm-xxx.mariadb.rds.aliyuncs.com -P 3306 -u test -pTestxxx --opt --default-character-set=utf8 --hex-blob testdb -R > /tmp/testdbtrigger.sql
    ```

    **说明：** 若数据库中没有使用存储过程、触发器和函数，可跳过此步骤。

4.  通过如下命令将数据文件、存储过程、触发器和函数导入到目标RDS for MariaDB实例中。

    ```
    mysql -h <目的实例外网地址> -P <目的实例端口> -u <目的实例高权限账号> -p<目的实例高权限账号密码> <目的实例数据库名称> < /tmp/<要迁移的数据库名称>.sql
    mysql -h <目的实例外网地址> -P <目的实例端口> -u <目的实例高权限账号> -p<目的实例高权限账号密码> <目的实例数据库名称> < /tmp/<要迁移的数据库名称>trigger.sql
    ```

    **示例**

    ``` {#codeblock_mcf_ms8_boy}
    mysql -h rm-xxx.mariadb.rds.aliyuncs.com -P 3306 -u test2 -pTest2xxx test001 < /tmp/testdb.sql
    mysql -h rm-xxx.mariadb.rds.aliyuncs.com -P 3306 -u test2 -pTest2xxx test001 < /tmp/testdbtriggertrigger.sql
    ```


