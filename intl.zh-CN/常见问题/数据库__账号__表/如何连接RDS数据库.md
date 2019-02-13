# 如何连接RDS数据库 {#concept_41843_zh .concept}

连接RDS数据库的方式有公网访问和内网访问两种，建议使用内网访问的方式保证传输速率和安全性。

## 公网访问 {#section_zkz_5kn_tgb .section}

公网也叫外网，通过公网访问RDS就是使用RDS实例的外网地址进行访问。RDS实例默认不提供外网地址，如果要通过公网访问，请在数据库连接页面申请外网地址。

![申请外网地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8203/155002066638726_zh-CN.png)

**说明：** 

-   外网地址会降低实例的安全性，请谨慎使用。
-   为了获得更快的传输速率和更高的安全性，建议您将应用迁移到与您的RDS实例在同一地域且网络类型相同的ECS实例，然后使用内网地址。

有了外网地址之后，就可以使用外网地址连接到RDS实例，具体请参见[如何连接实例](#)。

## 内网访问 {#section_fp5_cmn_tgb .section}

通过内网访问RDS就是使用RDS实例的内网地址进行访问。在数据库连接页面可以查看内网地址。

**内网访问的条件**

一般情况下，只有ECS可以通过内网访问RDS。如果本地机房要访问RDS，需要使用[物理专线](https://www.alibabacloud.com/help/zh/doc-detail/44844.htm)。

ECS要通过内网访问RDS，必须满足以下所有条件：

-   ECS和RDS属于同一个阿里云主账号。
-   ECS和RDS位于同一个地域。
-   ECS和RDS的网络类型相同。
-   如果ECS和RDS网络类型都是VPC，则必须处于同一个VPC。
-   ECS的私网IP已添加到RDS白名单，请参见[设置白名单](../../../../../intl.zh-CN/用户指南/数据安全性/设置白名单.md#)。

满足以上条件后，就可以使用RDS内网地址进行连接，具体的连接操作请参见[连接到RDS实例](#)。

## 常见问题 {#section_kjg_bnn_tgb .section}

-   如何禁止公网访问RDS实例？

    答：RDS的白名单设置里只放通私网IP，则公网无法访问该RDS实例，或者在数据库连接页面释放外网地址。


## 帮助文档 {#section_ofk_th4_tgb .section}

-   [连接到RDS for MySQL实例](../../../../../intl.zh-CN/RDS for MySQL 快速入门/连接实例.md#) 
-   [连接到RDS for SQL Server实例](../../../../../intl.zh-CN/RDS for SQL Server 快速入门/连接实例.md#)
-   [连接到RDS for PostgreSQL实例](../../../../../intl.zh-CN/RDS for PostgreSQL 快速入门/连接实例.md#)
-    [连接到RDS for PPAS实例](../../../../../intl.zh-CN/RDS for PPAS 快速入门/连接实例.md#)
-    [连接到RDS for MariaDB TX实例](../../../../../intl.zh-CN/RDS for MariaDB TX 快速入门/连接实例.md#)

