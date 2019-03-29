# Azure Database for MySQL数据库全量迁移到阿里云RDS {#concept_q5z_vhq_ngb .concept}

## 背景信息 {#section_jph_gj5_qgb .section}

本文介绍使用阿里云[数据传输服务（DTS）](https://help.aliyun.com/product/26590.html)，从Azure Database for MySQL数据库全量迁移到阿里云RDS for MySQL数据库。

## 前提条件 {#section_irb_kfs_ngb .section}

-   已经[创建阿里云RDS实例](../cn.zh-CN/RDS for MySQL 快速入门/创建RDS for MySQL实例.md#)。
-   已经[创建拥有读写权限的账号](../cn.zh-CN/RDS for MySQL 快速入门/初始化配置/创建账号和数据库.md#)。

## 迁移限制 {#section_n1c_vfs_ngb .section}

-   结构迁移不支持 event 的迁移。
-   对于MySQL的浮点型float/double，DTS通过round\(column，precision\)来读取该列的值，若列类型没有明确定义其精度，对于float，精度为38位，对于double类型，精度为308位，请先确认DTS的迁移精度是否符合业务预期。
-   如果使用了对象名映射功能后，依赖这个对象的其他对象可能迁移失败。

**说明：** 参数的修改可以在**实例详情** \> **配置** \> **修改配置** \> **添加数据库标志**里进行修改。

## 注意事项 {#section_s1s_dgs_ngb .section}

对于七天之内的异常任务，DTS会尝试自动恢复，可能会导致迁移任务的源端数据库数据覆盖目标实例数据库中写入的业务数据，迁移任务结束后务必将DTS访问目标实例账号的**写权限**用`revoke`命令回收掉。

## 操作步骤 {#section_m5h_kgs_ngb .section}

1.  登陆Azure Database for MySQL数据库，查看概述页面的服务器名称。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115436/155383769337872_zh-CN.png)

2.  左侧菜单栏单击**连接安全性**，在防火墙规则页面放通DTS的IP地址，设置完成后单击**保存**。

    **说明：** 放通DTS的IP地址后才可以通过DTS进行数据迁移，具体需放通IP地址请参见[源库实例地区](#table_jwb_1ns_ngb)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115436/155383769337873_zh-CN.png)

3.  登录[DTS控制台](https://dts.console.aliyun.com/)。
4.  在左侧菜单栏单击**数据迁移**，单击右上角**创建迁移任务**。
5.  填写源库和目标库信息，具体参数配置说明如下：

    |库类别|参数|说明|
    |---|--|--|
    |源库|实例类型|源库实例类型，这里选择**有公网IP的自建数据库**。|
    |实例地区|如果您的实例进行了访问限制，请先放开对应地区公网IP段的访问权限后，再配置数据迁移任务。**说明：** 可以单击右侧**获取DTS IP段**查看、复制对应地区的IP段。

|
    |数据库类型|源数据库类型，这里选择**MySQL**。|
    |主机名或IP地址|Azure Database for MySQL数据库的**服务器名称**。|
    |端口|默认的3306端口。|
    |数据库账号|Azure Database for MySQL数据库的高权限账号。|
    |数据库密码|Azure Database for MySQL数据库高权限账号的密码。|
    |目标库|实例类型|目标实例的类型，这里选**RDS实例**。|
    |实例地区|目标实例的地域。|
    |RDS实例ID|对应地区下的实例ID，这里选择想要迁移到的目标实例的ID。|
    |数据库账号|目标实例的拥有读写权限的账号。|
    |数据库密码|目标实例的对应账号的密码。|
    |连接方式|有**非加密传输**和**SSL安全连接**两种连接方式。**说明：** 

    -   支持并且开启了[SSL安全连接](cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置 SSL 加密.md#)的实例才需要选择SSL安全连接。
    -   SSL安全加密连接会显著增加CPU消耗。
|

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115436/155383769437874_zh-CN.png)

6.  填写完毕后单击**测试连接**，确定源库和目标库都测试通过。
7.  单击**授权白名单并进入下一步**。
8.  勾选对应的迁移类型，在迁移对象框中将想要迁移的数据库选中，单击![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/63394/155383769431842_zh-CN.png)移动到已选择对象框。

    **说明：** 为保证迁移数据的一致性，建议迁移过程中停止数据库的使用，选择结构迁移+全量数据迁移。

    结构迁移和全量数据迁移暂不收费。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115436/155383769437875_zh-CN.png)

9.  单击**预检查并启动**，等待预检查结束。

    **说明：** 如果检查失败，可以根据错误项的提示进行修复，然后重新启动任务。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115436/155383769437876_zh-CN.png)

10. 单击**下一步**，在**购买配置确认**对话框中，勾选**《数据传输（按量付费）服务条款》**并单击**立即购买并启动**。
11. 单击目标地域，查看迁移状态。迁移完成时，状态为已完成。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115436/155383769437877_zh-CN.png)

    至此，完成 Azure Database for MySQL数据库迁移到阿里云 RDS 的数据迁移任务。


