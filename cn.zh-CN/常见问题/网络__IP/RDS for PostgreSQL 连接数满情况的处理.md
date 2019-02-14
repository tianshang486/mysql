# RDS for PostgreSQL 连接数满情况的处理 {#concept_41742_zh .concept}

连接数满会导致客户端无法连接到RDS for PostgreSQL数据库。

## 问题现象 {#section_ik1_svb_5gb .section}

无法连接RDS for PostgreSQL数据库，报错如下：

```
FATAL: remaining connection slots are reserved for non-replication superuser connections
```

## 问题原因 {#section_hns_tvb_5gb .section}

连接数满导致无法连接。

## 解决方法 {#section_kws_tvb_5gb .section}

1.  [通过DMS登录RDS数据库](../../../../../cn.zh-CN/RDS for MySQL 用户指南/附录/通过DMS登录RDS数据库.md#)。
2.  选择**SQL操作** \> **SQL窗口**，通过如下命令检查当前连接数的限制。

    ```
    show max_connections;
    ```

    ![查看连接数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8369/155011229838811_zh-CN.jpg)

3.  使用如下命令查看当前连接，记下想要终止的连接的PID。

    ```
    select * from pg_stat_activity;
    ```

    ![查看连接](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8369/155011229838812_zh-CN.jpg)

4.  使用如下命令终止连接。

    ```
    SELECT pg_terminate_backend(<PID>) FROM pg_stat_activity;
    ```

    ![终止连接](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8369/155011229838813_zh-CN.jpg)


如果问题还未能解决，请通过[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)联系售后服务。

