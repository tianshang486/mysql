# 使用mysqldump迁移MariaDB数据 {#concept_t3k_hjb_wfb .concept}

使用 mysqldump 工具可以迁移数据库，本文将介绍详细的操作步骤。

## 背景信息 {#section_ivh_3w1_wfb .section}

由于 RDS 提供的关系型数据库服务与原生的数据库服务完全兼容，所以对用户来说，将原有数据库迁移到 RDS 实例的过程，与从一个 MariaDB 服务器迁移到另外一台 MariaDB 服务器的过程基本类似。

使用 mysqldump 工具可以迁移数据库，本文使用Linux7和MariaDB 10.2.4版本为例演示如何将本地MariaDB数据迁移到RDS for MariaDB TX实例。

## 注意事项 {#section_hky_5sg_cgb .section}

迁移后的表不区分大小写，统一变为小写。

## 前提条件 {#section_bd4_5gz_5fb .section}

-   已对RDS 实例[设置白名单](../../../../../intl.zh-CN/RDS for MariaDB TX 快速入门/初始化配置/设置白名单.md#)和[申请外网地址](../../../../../intl.zh-CN/RDS for MariaDB TX 快速入门/初始化配置/申请外网地址.md#)。

## 操作步骤 {#section_lcm_tqt_vfb .section}

1.  使用远程工具[连接RDS for MariaDB TX实例](../../../../../intl.zh-CN/RDS for MariaDB TX 快速入门/连接实例.md#)，创建空数据库。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64517/155287178540891_zh-CN.png)

2.  登录本地Linux服务器，使用自带的mysqldump工具将本地数据库数据导出为数据文件。

    ```
    mysqldump -h localhost -u root -p<root账号密码> --opt --default-character-set=utf8 --hex-blob <想要迁移的数据库名> --skip-triggers > /tmp/<想要迁移的数据库名>.sql
    ```

    **说明：** 导出期间请勿进行数据更新。本步骤仅仅导出数据，不包括存储过程、触发器及函数。

3.  使用 mysqldump 导出存储过程、触发器和函数。

    ```
    mysqldump -h localhost -u root -p<root账号密码> --opt --default-character-set=utf8 --hex-blob <想要迁移的数据库名> -R | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' > /tmp/<想要迁移的数据库名>trigger.sql
    ```

    **说明：** 若数据库中没有使用存储过程、触发器和函数，可跳过此步骤。在导出存储过程、触发器和函数时，需要将 definer 去掉，以兼容 RDS。

4.  通过如下命令将数据文件和存储过程文件导入到目标 RDS 中。

    ```
    mysql -h <RDS实例外网地址> –u <RDS实例高权限账号> -p<RDS实例高权限账号的密码> < /tmp/<想要迁移的数据库名>.sql
    mysql -h <RDS实例外网地址> -u <RDS实例高权限账号> -p<RDS实例高权限账号的密码> < /tmp/<想要迁移的数据库名>trigger.sql
    ```

5.  刷新远程工具后查看表，已经有了数据，说明已经迁移成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64517/155287178540892_zh-CN.png)


