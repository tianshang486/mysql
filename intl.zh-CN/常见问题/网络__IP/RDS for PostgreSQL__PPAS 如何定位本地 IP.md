# RDS for PostgreSQL/PPAS 如何定位本地 IP {#concept_59014_zh .concept}

## 问题描述 {#section_f4x_fg5_42b .section}

-   已经将本地设备的公网IP地址添加到RDS白名单，但是仍然无法访问RDS实例，而其他设备能访问该RDS实例。
-   已经将本地设备的公网IP地址添加到RDS白名单，但是仍然无法访问RDS实例，而将RDS白名单设置为公司的网段或者0.0.0.0/0后，该设备可以访问RDS实例。

以上的任意一种情形，都很可能是因为您添加到白名单的本地设备公网IP地址不正确，本文介绍如何查询到本地设备的真实出口IP地址。

**说明：** 本文只适用于ECS以外的设备访问RDS实例的情况。如果是ECS实例访问RDS实例，可以在ECS实例的详情页面查看准确的公网IP地址和内网IP地址。

## 注意事项 {#section_nby_fjp_yfb .section}

如果您发现您本地设备的公网IP地址会变化，而且建立的连接是用于生产环境，则建议您改为使用内网连接，或者在白名单中配置合理的公网IP段，确保不会因为IP地址改变而断连。

## 处理步骤 { .section}

1.  将 IP 地址 0.0.0.0/0 加入 RDS for PostgreSQL/PPAS 的白名单，操作方法请参见[设置白名单](../../../../../intl.zh-CN/RDS for PostgreSQL 快速入门/初始化配置/设置白名单.md)。
2.  使用 pgAdmin 4客户端连接[RDS for PostgreSQL](../../../../../intl.zh-CN/RDS for PostgreSQL 快速入门/连接实例.md#)或者[RDS for PPAS](../../../../../intl.zh-CN/RDS for PPAS 快速入门/连接实例.md#)实例。
3.  在左侧展开**数据库**，选择**postgres**，单击上方**工具** \> **查询工具**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8222/155384537133854_zh-CN.png)

4.  输入如下查询命令并执行。

    ```
    select datname, pid, usename,client_addr, client_hostname, client_port,query  from pg_stat_activity;
    
    ```

5.  查看结果里query列是select所对应的client\_addr列的IP，即为真实的出口IP。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8222/155384537133855_zh-CN.png)

6.  将步骤 **1** 在白名单中添加的 0.0.0.0/0 条目删除，添加上真实的出口IP。

