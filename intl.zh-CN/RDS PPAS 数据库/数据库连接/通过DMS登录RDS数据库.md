# 通过DMS登录RDS数据库

您可以通过阿里云的数据管理服务DMS登录RDS实例的数据库。

## 注意事项

只能使用内网地址登录DMS，暂时不支持使用申请的外网地址登录DMS。

## 操作步骤

1.  登录[RDS 管理控制台](https://rds.console.aliyun.com/)。
2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  单击目标实例的ID，进入基本信息页面。
4.  单击页面右上角的**登录数据库**，如下图所示，进入[数据管理控制台](https://dms.console.aliyun.com/?spm=5176.doc49015.2.5.1qi2e9&token=549cf345-ac05-455c-b3f9-75eadae023fe#/dms/login)的快捷登录页面。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9822472061/p4253.png)

5.  在快捷登录页面，设置如下参数：

    -   实例的地址和端口，格式为`<内网地址>:<内网端口号>`，例如`rm-bpxxxxxxx.rds.aliyuncs.com:3433`。关于如何查看实例的地址和端口信息，请参见[查看或修改内外网地址和端口](/intl.zh-CN/RDS PPAS 数据库/数据库连接/查看或修改内外网地址和端口.md)。
    -   实例的账号名称。
    -   实例的账号密码。
    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9077559951/p4254.png)

6.  单击**登录**。

    **说明：** 若您希望浏览器记住该账号的密码，可以先勾选**记住密码**，再单击**登录**。

7.  若出现将DMS服务器的IP段加入到RDS白名单中的提示，单击**设置所有实例**或者**设置本实例**。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9077559951/p4255.png)

8.  成功添加白名单后，单击**登录**。

