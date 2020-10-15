# 连接SQL Server实例

初始化配置后，您可以让ECS连接SQL Server实例，也可以本地连接到SQL Server实例，实现业务目标。

-   [创建RDS SQL Server实例](/cn.zh-CN/RDS SQL Server 数据库/快速入门/创建RDS SQL Server实例.md)
-   [设置白名单](/cn.zh-CN/RDS SQL Server 数据库/快速入门/设置白名单.md)
-   [创建账号](/cn.zh-CN/RDS SQL Server 数据库/账号/创建账号.md)

## 使用DMS连接实例

DMS是阿里云提供的图形化的数据管理工具，可用于管理关系型数据库和NoSQL数据库，支持数据管理、结构管理、用户授权、安全审计、数据趋势、数据追踪、BI图表、性能与优化等功能。

具体操作请参见[通过DMS登录RDS数据库](/cn.zh-CN/RDS SQL Server 数据库/数据库连接/通过DMS登录RDS数据库.md)。

## 使用客户端连接实例

下面以[Microsoft SQL Server Management Studio](https://docs.microsoft.com/zh-cn/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)（SSMS）客户端为例介绍如何连接到RDS实例。

1.  在ECS或本地电脑上启动Microsoft SQL Server Management Studio客户端。

2.  选择**连接** \> **数据库引擎** 。

3.  在弹出的连接到服务器对话框中输入登录信息。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8503729951/p2831.png)

    |参数|说明|
    |--|--|
    |**服务器类型**|选择**数据库引擎**。|
    |**服务器名称**|输入RDS实例的连接地址和端口号，连接地址与端口号之间用英文逗号隔开，如`rm-bptest.sqlserver.rds.aliyuncs.com,3433`。 查看RDS实例的内外网地址及端口信息请参见[查看或修改内外网地址和端口](/cn.zh-CN/RDS SQL Server 数据库/数据库连接/查看或修改内外网地址和端口.md)。 |
    |**身份验证**|选择**SQL Server身份验证**。|
    |**登录名**|RDS实例的账号名称。|
    |**密码**|RDS实例的账号密码。|

4.  单击**连接**，即可连接到实例。


## 连接失败的解决办法

请参见[解决无法连接实例问题](/cn.zh-CN/常见问题/连接/网络/解决无法连接RDS实例的问题.md)。

## 操作视频

[ECS连接RDS](https://help.aliyun.com/video_detail/54680.html)

## 常见问题

Q：我使用函数计算，想获取RDS的数据，要怎么操作呢？

A：您可以为函数安装第三方依赖，使用内置模块获取RDS数据，详情请参见[为函数安装第三方依赖](https://help.aliyun.com/document_detail/74571.html)。

