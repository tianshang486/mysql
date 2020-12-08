# 通过DMS登录RDS数据库

您可以通过阿里云的数据管理服务DMS登录RDS实例的数据库。

数据管理DMS是一种集数据管理、结构管理、用户授权、安全审计、数据趋势、数据追踪、BI图表、性能与优化和服务器管理于一体的数据管理服务。

## 新版DMS登录RDS数据库

前提条件

登录新版DMS的账号为主账号，或已申请相应数据库权限的子账号。申请权限请参见[权限管理](~~60371~~)。

1.  登录[新版DMS管理控制台](https://dms.aliyun.com/)。

2.  在左侧菜单栏选择目标实例，单击**请先登录**。

    **说明：** 管控模式为**安全协同**的实例是授权登录，无需输入账号密码，在**免登录实例**菜单里双击目标数据库即可登录。

    ![请先登录](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9077559951/p113304.png)

3.  输入登录实例数据库的账号密码，单击**确认**。

    **说明：** 请确保登录的数据库账号拥有目标数据库的权限，否则在左侧菜单里看不到目标数据库。修改数据库账号权限请参见[修改账号权限](/cn.zh-CN/RDS SQL Server 数据库/账号/修改账号权限.md)。

4.  登录后在左侧**已登录实例**菜单双击目标数据库，即可切换到目标数据库。


## 通过旧版DMS登录RDS数据库

**说明：** DMS已经升级为新版，建议您使用新版DMS登录RDS数据库。

1.  登录[RDS 管理控制台](https://rds.console.aliyun.com/)。
2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。
4.  单击页面右上角的**登录数据库**，如下图所示，进入DMS的快捷登录页面。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9822472061/p4253.png)

    **说明：** 此链接会根据您之前登录的习惯决定跳转到旧版DMS或者新版DMS。

5.  设置如下参数。

    |参数|说明|
    |--|--|
    |**网络地址:端口**|格式为`<连接地址>:<连接端口>`，例如rm-bpxxxxxxx.rds.aliyuncs.com:3433。关于如何查看实例的地址和端口信息，请参见[查看或修改内外网地址和端口](/cn.zh-CN/RDS MySQL 数据库/数据库连接/查看或修改内外网地址和端口.md)。|
    |**数据库用户名**|实例的账号名称。|
    |**密码**|实例账号对应的密码。|

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9077559951/p4254.png)

6.  单击**登录**。

    **说明：** 若您希望浏览器记住该账号的密码，可以先勾选**记住密码**，再单击**登录**。

7.  若出现将DMS服务器的IP段加入到RDS白名单中的提示，单击**设置所有实例**或者**设置本实例**。

    ![白名单设置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9077559951/p4255.png)

8.  成功添加白名单后，单击**登录**。

