# 创建数据库和账号SQL Server 2017版 {#concept_d2l_nlh_wfb .concept}

对于SQL Server 2017版本的实例，您需要通过RDS控制台创建一个初始账号，再通过DMS或客户端创建和管理数据库。

**说明：** 本文仅适用于SQL Server 2017版本的实例。其他SQL Server 版本请参见文档[创建数据库和账号SQL Server 2012/2016版](intl.zh-CN/RDS for SQL Server 快速入门/初始化配置/创建数据库和账号/创建数据库和账号SQL Server 2012__2016版.md)和[创建数据库和账号SQL Server 2008 R2版](intl.zh-CN/RDS for SQL Server 快速入门/初始化配置/创建数据库和账号/创建数据库和账号SQL Server 2008 R2版.md#)。

## 注意事项 {#section_ash_fph_wfb .section}

-   同一实例下的数据库共享该实例下的所有资源。您可以通过SQL命令管理普通账号和数据库。

-   分配数据库账号权限时，请按最小权限原则和业务角色创建账号，并合理分配只读和读写权限。必要时可以把数据库账号和数据库拆分成更小粒度，使每个数据库账号只能访问其业务之内的数据。如果不需要数据库写入操作，请分配只读权限。

-   为保障数据库的安全，请将数据库账号的密码设置为强密码，并定期更换。


## 操作步骤 {#section_csh_fph_wfb .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  选择目标实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156109880836543_zh-CN.png)

3.  单击目标实例的ID，进入基本信息页面。
4.  在左侧导航栏中，选择**账号管理**，进入账号管理页面。
5.  单击**创建初始账号**。
6.  输入要创建的账号信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64588/156109880832576_zh-CN.png)

    参数说明：

    -   **数据库账号**：长度为2~16个字符，由小写字母、数字或下划线组成。但开头需为字母，结尾需为字母或数字。

**说明：** test、root等为保留关键字，不能设置为账号名。

    -   **密码**：

-   长度为8~32个字符。
-   由大写字母、小写字母、数字、特殊字符中的任意三种组成。
-   特殊字符为!@\#$%^&\*\(\)\_+-=
    -   **确认密码**：输入与密码一致的字段，以确保密码正确输入。

7.  单击**确定**。
8.  单击页面右上角的**登录数据库**，进入[数据管理控制台](https://dms-intl.console.aliyun.com/#/dms/rsList)的RDS数据库登录页面。
9.  确保连接地址、端口、数据库用户名和密码填写正确。
    -   参数说明：

        -   1：实例的连接地址和端口信息。可以在实例的**基本信息**或**数据库连接**页面查看。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64588/156109880832577_zh-CN.png)

        -   2：要访问数据库的账号名称。

        -   3：上述账户所对应的密码。

10. 单击**登录**。

    **说明：** 若您希望浏览器记住该账号的密码，可以先勾选**记住密码**，然后再单击**登录**。

11. 若出现将DMS服务器的IP段加入到RDS白名单中的提示，单击**设置白名单**，如下图所示。若需手动添加，请参见[设置白名单](../intl.zh-CN/用户指南/数据安全性/设置白名单.md#)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7839/15610988092774_zh-CN.png)

12. 成功添加白名单后，单击**登录**。
13. 成功登录RDS实例后，在页面上方的菜单栏中，选择**SQL操作** \> **SQL窗口** 。
14. 在SQL窗口中输入如下命令，创建数据库。

    ``` {#codeblock_nfh_r3x_j6d}
    create database <database name>;
    ```

15. 单击**执行**，完成创建数据库。
16. 在SQL窗口中输入如下命令，创建普通账号。

    ``` {#codeblock_xst_2vh_233}
    CREATE LOGIN <login name> WITH PASSWORD = '<password>';
    ```

17. 单击**执行**，完成创建普通账号。

    **说明：** 在DMS中通过T-SQL创建的普通账号不会显示在控制台的账号列表中，但是可以使用普通账号来登录数据库。

18. 在SQL窗口中输入如下命令，创建数据库用户，并且关联刚创建的普通账号。

    ``` {#codeblock_cwu_n1f_ntj}
    USE <database name>;
    CREATE USER <user name> FOR LOGIN <login name>;
    ```

19. 单击**执行**，完成数据库用户创建，至此普通账号就可以访问对应数据库。

## 常见问题 {#section_znt_2jv_fhb .section}

创建的账号在只读实例上可以用吗？

答：主实例创建的账号会同步到只读实例，只读实例无法管理账号。账号在只读实例上只能进行读操作，不能进行写操作。

## 相关API {#section_hcn_555_jgb .section}

|API|描述|
|---|--|
|[CreateAccount](../intl.zh-CN/API参考/账号管理/CreateAccount.md#)|创建账号|
|[CreateDatabase](../intl.zh-CN/API参考/数据库管理/CreateDatabase.md#)|创建数据库|

