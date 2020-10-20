# 连接PostgreSQL实例

初始化配置后，您可以让ECS连接PostgreSQL实例，也可以本地连接到PostgreSQL实例，实现业务目标。

若您要使用云数据库RDS，可以通过阿里云数据管理（DMS）或通过客户端连接RDS实例。本章将介绍如何通过DMS和pgAdmin 4客户端连接RDS实例。

## 背景信息

您可以通过RDS管理控制台先登录DMS，然后再连接需要访问的RDS实例。

[数据管理](https://dms-intl.console.aliyun.com/#/dms/login)（Data Management，简称DMS）是一种集数据管理、结构管理、访问安全、BI图表、数据趋势、数据轨迹、性能与优化和服务器管理于一体的数据管理服务。支持MySQL、SQL Server、PostgreSQL、MongoDB、Redis等关系型数据库和NoSQL的数据库管理，同时还支持Linux服务器管理。

您也可以使用客户端连接RDS实例。由于RDS提供的关系型数据库服务与原生的数据库服务完全兼容，所以对用户而言，连接数据库的方式也基本类似。本文以pgAdmind 4客户端为例介绍RDS实例的连接方法，其它客户端可参见此方法。用客户端连接RDS实例时，请注意选择内外网地址：

-   若您的客户端部署在ECS实例上，且ECS实例与要访问的RDS实例的地域、网络类型相同，请使用内网地址。例如ECS实例和RDS实例都是华东1的专有网络实例，使用内网地址连接能提供安全高效的访问。
-   其它情况请使用外网地址。

## 通过DMS连接实例

您可以在**数据库管理**页面右侧单击**SQL查询**登录数据库。

![SQL查询](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6122613061/p174701.png)

具体操作请参见[通过DMS登录RDS数据库](/intl.zh-CN/RDS PostgreSQL 数据库/数据库连接/通过DMS登录RDS数据库.md)。

## 通过客户端登录

1.  将要访问RDS实例的IP地址加入RDS白名单中。关于如何设置白名单，请参见[设置白名单](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/设置白名单.md)。
2.  启动[pgAdmin 4客户端](https://www.pgadmin.org/download/)。

    **说明：** 高版本客户端首次登录需要设置Master Password用于保护保存的密码和其他凭据。

3.  右击**Servers**，选择**Create** \> **Server...**。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6077559951/p2963.png)

4.  在**General**页签设置连接名称。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6077559951/p2964.png)

5.  选择**Connection**标签页，输入要连接的实例信息。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6077559951/p2965.png)

    |参数|说明|
    |--|--|
    |**Hostname/address**|主机名称/地址。若通过内网连接，需输入RDS实例的内网连接地址；若使用外网连接，需输入RDS实例的外网连接地址。查看RDS实例的内外网地址及端口请参见[查看或修改内外网地址和端口](/intl.zh-CN/RDS PostgreSQL 数据库/数据库连接/查看或修改内外网地址和端口.md)。|
    |**Port**|连接地址对应的端口。|
    |**Username**|RDS实例的账号名称。|
    |**Password**|账号对应的密码。|

6.  单击**Save**。
7.  若连接信息无误，会出现如下界面，则表示连接成功。

    **说明：** postgres是RDS实例默认的系统数据库，请勿在该数据库中进行任何操作。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6077559951/p2967.png)


## 常见问题

Q：我使用函数计算，想获取RDS的数据，要怎么操作呢？

A：您可以为函数安装第三方依赖，使用内置模块获取RDS数据，详情请参见[为函数安装第三方依赖](https://www.alibabacloud.com/help/zh/doc-detail/74571.htm)。

