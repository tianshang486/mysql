# 连接MySQL实例 {#concept_n1v_qpf_vdb .concept}

初始化配置后，您可以让ECS连接MySQL实例，也可以本地连接到MySQL实例，实现业务目标。

## 背景信息 {#section_ixn_v5c_dhb .section}

完成[创建实例](cn.zh-CN/RDS for MySQL 快速入门/创建RDS for MySQL实例.md)、[设置白名单](cn.zh-CN/RDS for MySQL 快速入门/初始化配置/设置白名单.md#)和[创建账号](cn.zh-CN/RDS for MySQL 快速入门/初始化配置/创建账号和数据库.md)等操作后，您可以使用数据管理服务DMS（Data Management Service）或通用数据库客户端连接到MySQL实例，也可以在应用程序中配置地址、端口、账号信息等进行连接。

若您因业务需要使用ECS实例连接RDS实例时，请确保它们都处于经典网络或相同VPC网络中，且白名单设置正确。如有疑问，请参见[解决无法连接实例问题](../../../../cn.zh-CN/常见问题/如何连接__无法连接/解决无法连接实例问题.md#)。

## 使用DMS连接实例 {#section_pgl_xm5_vdb .section}

DMS是阿里云提供的图形化的数据管理工具，可用于管理关系型数据库和NoSQL数据库，支持数据管理、结构管理、用户授权、安全审计、数据趋势、数据追踪、BI图表、性能与优化等功能。

具体操作请参见[通过DMS登录RDS数据库](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据库连接/通过DMS登录RDS数据库.md#)。

## 使用客户端连接实例 {#section_fbz_ym5_vdb .section}

由于RDS与原生的数据库服务完全兼容，所以您可以使用任何通用的数据库客户端连接到RDS实例，且连接方法类似。下文以[HeidiSQL](https://www.heidisql.com/)为例。

1.  启动HeidiSQL客户端。
2.  在左下角单击**新建**。
3.  输入要连接的RDS实例信息，参数说明如下。

    |参数|说明|
    |--|--|
    |**网络形式**|连接数据库的形式。选择**MariaDB or MySQL（TCP/IP）**。|
    |**主机名/IP地址**|输入RDS实例的内网地址或外网地址。     -   若您的客户端部署在ECS实例上，且ECS实例与要访问的RDS实例的地域、网络类型相同，请使用内网地址。例如ECS实例和RDS实例都是华东1的专有网络实例，使用内网地址连接能提供安全高效的访问。
    -   其它情况只能使用外网地址。
 查看RDS实例的内外网地址及端口信息的步骤如下：

    1.  登录[RDS管理控制台](https://rds.console.aliyun.com)。
    2.  在页面左上角，选择实例所在地域。
    3.  找到目标实例，单击实例ID。
    4.  在**基本信息**栏中，即可查看内外网地址及内外网端口信息。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/15688001102609_zh-CN.png)

 |
    |**用户**|要访问RDS实例的账号名称。|
    |**密码**|以上账号的密码。|
    |**端口**|若使用内网连接，需输入RDS实例的内网端口。若使用外网连接，需输入RDS实例的外网端口。|

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/156880011054911_zh-CN.png)

4.  单击**打开**。

    若连接信息无误，即会成功连接实例。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/15688001102610_zh-CN.png)


## 使用命令行连接实例 {#section_5sn_ny9_2ce .section}

如果您的服务器安装了MySQL，可以通过命令行连接RDS for MySQL数据库，连接方式如下：

``` {#codeblock_nlp_l4x_t34}
mysql -h<主机名> -P<端口> -u<用户名> -p<密码> -D<数据库>
```

|选项|说明|示例|
|--|--|--|
|-h|RDS实例的内网地址或外网地址。连接地址请参见[设置连接地址](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据库连接/设置连接地址.md#)。|`rm-bpxxxxxxxxxxxxxx.mysql.rds.aliyuncs.com`|
|-P|RDS实例的端口号。 -   若使用内网连接，需输入RDS实例的内网端口。
-   若使用外网连接，需输入RDS实例的外网端口。

 **说明：** 

-   默认端口为3306。
-   如果端口号为默认端口，该参数可以不填。

 |`3306`|
|-u|要访问RDS实例的账号名称。|`root`|
|-p|以上账号的密码。 **说明：** 该参数非必填参数。

-   如果不填写该参数，后续操作中会重新要求输入密码。
-   如果填写该参数，`-p`与数据库密码之间不能有空格。

 |`password233`|
|-D|需要登录的数据库名称。 **说明：** 

-   该参数非必填参数。
-   可以不输入`-D`仅输入数据库名称。

 |`mysql`|

![](images/52311_zh-CN.png "命令行连接示例")

## 连接失败的解决办法 {#section_z11_3xz_dfb .section}

请参见[解决无法连接实例问题](../../../../cn.zh-CN/常见问题/如何连接__无法连接/解决无法连接实例问题.md#)。

## 操作视频 {#section_ub4_gdc_8bv .section}

[ECS连接RDS](https://help.aliyun.com/video_detail/54680.html)

