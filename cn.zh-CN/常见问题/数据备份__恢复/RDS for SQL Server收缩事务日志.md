# RDS for SQL Server收缩事务日志 {#concept_wdv_z1n_hhb .concept}

RDS for SQL Server实例可以收缩事务日志，减少日志文件大小。

## 操作步骤 {#section_gb4_lu9_h9r .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/155505460036543_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧导航栏单击**备份恢复**。
5.  在右上角单击**收缩事务日志**。

    ![收缩事务日志](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8339/155505460044310_zh-CN.png)


**说明：** 清理后需要等待事务结束，一般需要20分钟左右。另外每次备份时SQL Server也会收缩事务日志。

