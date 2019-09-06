# 通过DMS登录RDS数据库 {#concept_cml_x4v_ydb .concept}

您可以通过阿里云的[数据管理DMS](https://help.aliyun.com/document_detail/47550.html)登录RDS实例的数据库。本文将介绍从RDS控制台，通过DMS登录RDS实例的方法。

## 注意事项 {#section_yj4_kfv_cgb .section}

-   只能使用内网地址登录DMS，暂时不支持使用申请的外网地址登录DMS。
-   如下版本实例暂不支持DMS：
    -   MariaDB实例
    -   MySQL 8.0版本实例

## 操作步骤 {#section_obw_z4v_ydb .section}

1.  登录 [RDS 管理控制台](https://rds.console.aliyun.com/)。
2.  选择目标实例所在地域。

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156774768937169_zh-CN.png)

3.  单击目标实例的ID，进入基本信息页面。
4.  单击页面右上角的**登录数据库**，如下图所示，进入数据管理控制台的快捷登录页面。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8006/15677476894253_zh-CN.png)

5.  在快捷登录页面，设置如下参数：

    -   实例的内网地址和内网端口，格式为`<内网地址>:<端口号>`，例如rm-bpxxxxxxx.rds.aliyuncs.com:3433。关于如何查看实例的内网地址和端口信息，请参见[查看实例的内外网地址及端口信息](cn.zh-CN/用户指南/数据库连接/查看实例的内外网地址及端口信息.md#)。
    -   实例的账号名称。
    -   实例的账号密码。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8006/15677476894254_zh-CN.png)

6.  单击**登录**。

    **说明：** 若您希望浏览器记住该账号的密码，可以先勾选**记住密码**，再单击**登录**。

7.  若出现将DMS服务器的IP段加入到RDS白名单中的提示，单击**设置所有实例**或者**设置本实例**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8006/15677476904255_zh-CN.png)

8.  成功添加白名单后，单击**登录**。

## 下一步 {#section_srk_1jh_uxk .section}

登录DMS后您可以进行数据库管理操作，建议您先查看[功能总览](https://help.aliyun.com/document_detail/47593.html)。

