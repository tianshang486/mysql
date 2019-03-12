# 复制数据库SQL Server 2008 R2版 {#concept_o5v_vlq_wdb .concept}

若您需要创建一个与现有数据库数据完全相同的数据库，您可以使用复制数据库的方式。本文介绍如何通过RDS控制台复制并创建新的数据库，仅适用于SQL Server 2008 R2版本的实例。对于SQL Server 2012及以上版本的实例，只能通过SQL命令复制数据库，详情请参见[复制数据库SQL Server 2012及以上版本](cn.zh-CN/RDS for SQL Server 用户指南/数据库管理/SQL Server复制数据库/复制数据库SQL Server 2012及以上版本.md#)。

## 注意事项 {#section_xy3_ylq_wdb .section}

-   每次只能复制一个数据库。

-   新建数据库的名称必须和现有数据库的名称不同。


## 操作步骤 {#section_egc_1mq_wdb .section}

1.  登录[RDS管理控制台](https://rdsnew.console.aliyun.com/console/index#/rdsList/)。
2.  在页面左上角，选择实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/155237823636543_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧菜单栏中单击**数据库管理**。
5.  单击**复制数据库**。
6.  填写新建数据库的信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7938/15523782363112_zh-CN.png)

    **参数说明：**

    |参数名称|说明|
    |----|--|
    |指定新数据库名称|新建数据库的名称，由小写字母、数字、下划线、中划线组成，以字母开头，以字母或数字结尾，最长64个字符。|
    |选择要复制的数据库|在现有数据库中选择要复制的数据库。|
    |是否保留源数据库内账号信息|是否要在新建数据库中保留源库中的账号和授权信息。系统默认**保留**，您可以根据需求选择合适的选项。|
    |备注说明|可以备注该数据库的相关信息，便于后续数据库管理，最多支持256个英文字符（1个汉字等于3个英文字符）。|

7.  单击**确定**。

