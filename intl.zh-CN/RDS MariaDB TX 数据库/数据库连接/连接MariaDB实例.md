# 连接MariaDB实例

初始化配置后，您可以让ECS连接MariaDB实例，也可以本地连接到MariaDB实例，实现业务目标。

## 前提条件

已完成如下操作：

-   [创建RDS MariaDB实例](/intl.zh-CN/RDS MariaDB TX 数据库/快速入门/创建RDS MariaDB实例.md)
-   [设置白名单](/intl.zh-CN/RDS MariaDB TX 数据库/快速入门/设置白名单.md)
-   [创建账号](/intl.zh-CN/RDS MariaDB TX 数据库/快速入门/创建数据库和账号.md)

## 使用DMS连接实例

DMS是阿里云提供的图形化的数据管理工具，可用于管理关系型数据库和NoSQL数据库，支持数据管理、结构管理、用户授权、安全审计、数据趋势、数据追踪、BI图表、性能与优化等功能。

您可以在**数据库管理**页面右侧单击**SQL查询**登录数据库。

![SQL查询](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8414713061/p174701.png)

## 方法二：使用客户端连接实例

RDS与原生的数据库服务完全兼容，所以您可以使用任何通用的数据库客户端连接到RDS实例，且连接方法类似。下文以[HeidiSQL](https://www.heidisql.com/)为例。

1.  启动HeidiSQL客户端。
2.  在左下角单击**新建**。
3.  输入要连接的RDS实例信息，参数说明如下。

    ![连接信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3885675061/p54911.png)

    |参数|说明|
    |--|--|
    |**网络类型**|连接数据库的形式。选择**MySQL（TCP/IP）**。|
    |**Library**|动态链接库。保持默认值即可。|
    |**主机名/IP地址**|输入RDS实例的内网地址或外网地址，例如`rm-bp1xxxxxxxxxxxxxx.mysql.rds.aliyuncs.com`。 关于如何查看地址信息，请参见[查看或修改内外网地址和端口](/intl.zh-CN/RDS MySQL 数据库/数据库连接/查看或修改内外网地址和端口.md)。    -   若您的客户端部署在ECS实例上，且ECS实例与要访问的RDS实例的地域、网络类型相同，请使用内网地址。例如ECS实例和RDS实例都是华东1的专有网络实例，使用内网地址连接能提供安全高效的访问。
    -   其它情况只能使用外网地址。 |
    |**用户**|RDS实例中创建的账号名称。关于如何创建账号，请参见[创建数据库和账号](/intl.zh-CN/RDS MySQL 数据库/快速入门/创建数据库和账号.md)。|
    |**密码**|账号对应的密码。|
    |**端口**|若使用内网连接，需输入RDS实例的内网端口。若使用外网连接，需输入RDS实例的外网端口。更多信息，请参见[查看或修改内外网地址和端口](/intl.zh-CN/RDS MySQL 数据库/数据库连接/查看或修改内外网地址和端口.md)。|

4.  单击**打开**。

    若连接信息无误，即会成功连接实例。

    ![连接成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9613729951/p2610.png)


常见报错说明如下：

-   `Unknown MySQL server hose 'xxxxxxxxx'(11001)`

    请检查**主机名/IP地址**是否填写正确，常见错误是填写为实例ID或IP地址。应该填写内网或外网连接地址。

    ![地址](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3885675061/p183795.png)

-   `Access denied for user 'xxxxx'@'xxxxx'(using password:YES)`

    请检查账号密码是否填写正确，常见错误为填写阿里云账号。应该填写实例的**账号管理**页面创建的账号。

    ![账号](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3885675061/p183797.png)

-   响应很慢并返回`Can't connect to MySQL server on 'rm-bp1xxxxxxxxxxxxxx.mysql.rds.aliyuncs.com'(10060)`

    请检查是否白名单是否设置正确，需要将该软件所在主机的对外公网IP填写在白名单中。如何设置白名单，请参见[设置白名单](/intl.zh-CN/RDS MySQL 数据库/快速入门/设置白名单.md)。

    **说明：** 您可以临时设置白名单为0.0.0.0/0，用来排查是否是白名单设置问题导致的连接报错，如果确定是白名单设置问题，再定位正确的IP地址。具体操作，请参见[外网无法连接RDS MySQL或MariaDB：如何正确填写本地设备的公网IP地址](/intl.zh-CN/常见问题/连接/网络/外网无法连接RDS MySQL或MariaDB：如何正确填写本地设备的公网IP地址.md)。


## 常见问题

Q：我使用函数计算，想获取RDS的数据，要怎么操作呢？

A：您可以为函数安装第三方依赖，使用内置模块获取RDS数据，详情请参见[为函数安装第三方依赖](https://www.alibabacloud.com/help/zh/doc-detail/74571.htm)。

