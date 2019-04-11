# RDS访问实例诊断报告 {#concept_pkl_pkc_3gb .concept}

RDS实例在DMS和CloudDBA中均提供了诊断报告的功能。

## 通过CloudDBA访问实例诊断报告 {#section_ozk_tgd_3gb .section}

**说明：** 目前仅如下版本实例支持此功能：

-   MySQL5.5高可用版
-   MySQL 5.6版
-   MySQL 5.7 高可用版
-   PostgreSQL 10.0版
-   PPAS 10.0版

1.  登录[RDS管理控制台](https://rdsnext.console.aliyun.com/)。
2.  选择目标实例所在地域。
3.  单击目标实例ID，进入基本信息页面。
4.  在左侧导航栏中，选择**CloudDBA** \> **诊断报告** ，进入诊断报告页面。
5.  点击**创建诊断报告**，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8403/155494851335776_zh-CN.png)

6.  选择诊断数据的起始时间，点击**确定**保存后单击**创建报告**，如下图所示。

    **说明：** PostgreSQL 10.0版本和PPAS 10.0版本无法选择起始时间，默认生成当前时间的诊断报告。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8403/155494851335781_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8403/155494851435782_zh-CN.png)

7.  诊断完成后，可在列表中查看诊断得分并进行查看报告或删除报告的操作，如下图所示。

    **说明：** 诊断报告列表可以保存最近30天内的诊断记录，超时数据将会被自动删除。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8403/155494851435783_zh-CN.png)

    具体操作步骤如下：

    -   查看诊断报告：单击**查看报告**。
    -   删除诊断报告：
        1.  单击**删除**。
        2.  在弹出的确认框中，单击**确认**。

## 通过DMS访问实例诊断报告 {#section_m5g_lqc_3gb .section}

**说明：** 仅支持RDS for MySQL。

1.  登录[RDS管理控制台](https://rdsnext.console.aliyun.com/)。
2.  选择目标实例所在地域。
3.  单击目标实例ID，进入基本信息页面。
4.  单击页面右上角的**登录数据库**，进入[数据管理控制台](https://dms.console.aliyun.com/#/dms/login)的快捷登录页面。
5.  选择**性能** \> **诊断报告**，或者点击界面右侧的**查看诊断报告**按钮，跳转到混合云数据库管理平台（Hybrid Cloud Database Management，HDM）。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8403/155494851435755_zh-CN.png)

    **说明：** 对于第一次进入的用户需要对HDM进行授权。

    ![HDM授权](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8403/155494851444219_zh-CN.png)

6.  查看已有的诊断报告，或者单击**发起诊断**生成新的诊断报告。

    **说明：** 如果问题正在发生，建议先点击**发起诊断**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8403/155494851435762_zh-CN.png)


如问题还未解决,请联系[售后技术支持](https://selfservice.console.aliyun.com/ticket/createIndex)。

