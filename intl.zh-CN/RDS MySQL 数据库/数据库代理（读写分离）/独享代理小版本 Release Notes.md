# 独享代理小版本 Release Notes

本文介绍数据库独享代理的小版本更新说明。

**说明：** 关于RDS MySQL内核的小版本说明请参见[AliSQL 小版本 Release Notes](/intl.zh-CN/自研内核 AliSQL/AliSQL 小版本 Release Notes.md)。

## 如何查看独享代理小版本

如果您的独享代理不是最新版本，可以在实例的**数据库代理**页面单击**升级独享代理小版本**查看**当前版本**和**可升级到版本**。

**说明：** 如果独享代理是最新版本，不会显示升级按钮。您也可以通过调用API接口查看独享代理小版本，详情请参见[查询独享代理设置](/intl.zh-CN/API 参考/数据库代理/查询独享代理设置.md)。

![查看独享代理版本](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1416182061/p173582.png)

## 小版本更新说明

|小版本|说明|
|---|--|
|1.12.7|-   新功能
    -   支持`show full processlist`语法。
    -   支持XA事务语法。
-   Bug修复
    -   修复MySQL 8.0的`show processlist`报错问题。
    -   修复若干事务级连接池的问题。
    -   修复若干建立连接失败的问题。 |
|1.11.12|-   新功能

支持[事务级连接池](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/连接池.md)。

-   Bug修复
    -   优化长连接的负载均衡，当节点从异常状态变成正常后，旧的长连接新请求可以再次路由到该节点。
    -   优化Prepare语法，支持Prepare单播。
    -   修复当MySQL 5.7连接MySQL 5.6数据库，开启Deprecate EOF导致连接失败的问题。
    -   修复存储过程中更改数据库时导致连接断开的问题。
    -   修复当结果集里大报文单行超过16 MB数据时，客户端报`Packets out of order`错误的问题。
    -   修复只读实例通过`set autocommit=0`打开的事务未及时关闭问题。
    -   修复`lock in shared mode`语句被路由到只读实例的问题。
    -   修复`select handler from abc for update`语句被路由到只读实例的问题。
    -   修复同个用户多个host的认证失败问题。 |
|1.10.7|Bug修复

修复会话级连接池的若干问题。 |
|1.9.23|-   新功能
    -   支持root账号连接。
    -   支持SSL连接。
-   Bug修复
    -   修复`change user`失败问题。
    -   修复`load file`失败问题。
    -   修复客户端收到sequence错误报文，导致应用报`Exception: Packets out of order`错误的问题。
    -   修复主实例异常时只读实例的连接被断开问题。 |
|1.9.14|-   新功能

支持hint语法：`/*FORCE_SLAVE*/, /*FORCE_MASTE*/`。

-   Bug修复
    -   修复charset默认值获取错误导致的乱码问题。
    -   修复返回MySQL版本号的String不正确问题。 |

