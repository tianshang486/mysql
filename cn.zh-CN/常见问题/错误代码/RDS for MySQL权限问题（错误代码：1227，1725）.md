# RDS for MySQL权限问题（错误代码：1227，1725） {#concept_yr5_skv_vfb .concept}

## 错误信息 {#section_ljw_xkv_vfb .section}

```
[Err] 1227 - Access denied; you need (at least one of) the SUPER privilege(s) for this operation --常见于RDS MySQL 5.6

ERROR 1725 (HY000) at line 1936: OPERATION need to be executed set by ADMIN --常见于RDS MySQL 5.5
```

## 出现场景 {#section_psv_1lv_vfb .section}

-   在创建 存储过程、函数、触发器、事件、视图的时候出现这个错误。
-   从本地数据库导出SQL，在RDS上应用该SQL的时候出现该错误。
-   从RDS for MySQL 5.6实例下载逻辑备份，导入到RDS或本地数据库中。

## 错误原因 {#section_ddw_1lv_vfb .section}

-   导RDS for MySQL实例时，SQL语句中含有需要Supper权限才可以执行的语句，而RDS for MySQL不提供Super权限，因此需要去除这类语句。
-   本地MySQL实例没有启用GTID。

## 解决办法 {#section_upw_1lv_vfb .section}

1.  去除DEFINER子句：
    1.  检查SQL文件，去除下面类似的子句。

        ```
        DEFINER=`root`@`%` 
        ```

    2.  在Linux平台下，可以尝试使用下面的语句去除。

        ```
        sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/ ' your.sql > your_revised.sql
        ```

2.  去除GTID\_PURGED子句
    1.  检查SQL文件，去除下面类似的子句。

        ```
        SET @@GLOBAL.GTID_PURGED='d0502171-3e23-11e4-9d65-d89d672af420:1-373,
        d5deee4e-3e23-11e4-9d65-d89d672a9530:1-616234';
        ```

    2.  在Linux平台下，可以尝试使用下面的语句去除。

        ```
        awk '{ if (index($0,"GTID_PURGED")) { getline; while (length($0) > 0) { getline; } } else { print $0 } }' your.sql | grep -iv 'set @@' > your_revised.sql
        ```

        **说明：** 也可以导出的时候在mysqldump命令后添加参数--set-gtid-purged=off来取消输出GTID\_PURGED子句。


