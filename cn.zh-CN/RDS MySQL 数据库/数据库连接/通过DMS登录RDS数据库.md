# 通过DMS登录RDS数据库

您可以通过阿里云的数据管理服务DMS登录RDS数据库。

数据管理DMS是一种集数据管理、结构管理、用户授权、安全审计、数据趋势、数据追踪、BI图表、性能与优化和服务器管理于一体的数据管理服务。

为提供更好的数据管理体验，DMS已升级新版，提供更多功能，同时下调企业版DMS价格。详情请参见[DMS升级说明](~~153131~~)。

## 通过新版DMS登录RDS数据库

前提条件

-   登录新版DMS的账号为主账号，或已申请相应数据库权限的子账号。申请权限请参见[权限管理](~~60371~~)。
-   云数据库已经被管理员录入。录入云数据库请参见[云数据库录入](~~159708~~)。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏中单击**数据库管理**。

5.  在右侧单击**SQL查询**。

    ![SQL查询](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8414713061/p174701.png)

6.  在DMS的**登录实例**页面，输入实例数据库的账号密码，单击**登录**。

    **说明：** 请确保登录的数据库账号拥有目标数据库的权限，否则在左侧菜单里看不到目标数据库。修改数据库账号权限请参见[修改账号权限](/cn.zh-CN/RDS MySQL 数据库/账号/账号权限/修改账号权限.md)。

    ![登录数据库](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6122613061/p174718.png)

7.  登录后请刷新页面，然后在左侧**已登录实例**菜单双击目标数据库，即可切换到目标数据库。


**说明：** 除了通过RDS控制台跳转到DMS进行登录，您还可以登录DMS控制台直接录入RDS实例，录入后可以在DMS控制台快速登录数据库。详情请参见[云数据库录入]()。

## 通过旧版DMS登录RDS数据库

**说明：** DMS已经升级为新版，建议您使用新版DMS登录RDS数据库。

1.  登录[RDS 管理控制台](https://rds.console.aliyun.com/)。
2.  选择目标实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  单击目标实例的ID，进入基本信息页面。
4.  单击页面右上角的**登录数据库**，如下图所示，进入DMS的快捷登录页面。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9822472061/p4253.png)

    **说明：** 此链接会根据您之前登录的习惯决定跳转到旧版DMS或者新版DMS。

5.  设置如下参数。

    |参数|说明|
    |--|--|
    |**网络地址:端口**|格式为`<连接地址>:<连接端口>`，例如rm-bpxxxxxxx.rds.aliyuncs.com:3433。关于如何查看实例的地址和端口信息，请参见[查看或修改内外网地址和端口](/cn.zh-CN/RDS MySQL 数据库/数据库连接/查看或修改内外网地址和端口.md)。|
    |**数据库用户名**|实例的账号名称。|
    |**密码**|实例账号对应的密码。|

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9077559951/p4254.png)

6.  单击**登录**。

    **说明：** 若您希望浏览器记住该账号的密码，可以先勾选**记住密码**，再单击**登录**。

7.  若出现将DMS服务器的IP段加入到RDS白名单中的提示，单击**设置所有实例**或者**设置本实例**。

    ![白名单设置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9077559951/p4255.png)

8.  成功添加白名单后，单击**登录**。

