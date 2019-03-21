# MySQL 5.5升级版本 {#concept_gnx_vgj_wdb .concept}

您可以将RDS for MySQL实例的引擎从低版本升级到高版本。

**说明：** 不支持数据库引擎版本的降级。

## 注意事项 {#section_b5p_fhj_wdb .section}

-   目前仅支持从MySQL 5.5升级到MySQL 5.6。
-   升级版本前，建议先购买目标版本实例，并测试兼容性。
-   在数据库升级过程中，RDS服务可能会出现一次30秒的闪断，请您尽量在业务低峰期执行升级操作，或确保您的应用有自动重连机制。

## 操作步骤 {#section_or5_ghj_wdb .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/155313506937169_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  单击**升级数据库版本**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7888/15531350693026_zh-CN.png)

5.  在弹出的对话框中，选择目标版本，单击**开始升级**。

