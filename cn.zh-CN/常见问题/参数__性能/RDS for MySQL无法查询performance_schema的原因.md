# RDS for MySQL无法查询performance\_schema的原因 {#concept_ky3_xg2_jhb .concept}

本文介绍在RDS for MySQL实例上执行`select * from performance_schema.threads`返回结果为空的原因及解决办法。

## performance\_schema介绍 {#section_fvg_dh2_jhb .section}

MySQL中的performance\_schema主要用于收集数据库服务器性能参数，它提供以下功能：

-   提供进程等待的详细信息，包括锁、互斥变量、文件信息。
-   保存历史的事件汇总信息，为优化MySQL服务器性能提供详细的数据。
-   新增和删除监控事件点，并可以随意改变MySQL服务器的监控周期。

## 故障原因 {#section_ctg_xh2_jhb .section}

在RDS for MySQL实例上执行`select * from performance_schema.threads`命令进行查询，未返回任何结果是因为开启performance\_schema后会影响实例的性能，所以RDS中该功能默认是关闭的。

![未开启performance_schema](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8274/155477456543528_zh-CN.png)

## 解决方法 {#section_hnh_432_jhb .section}

针对MySQL 5.6/5.7，可以在控制台修改performance\_schema参数值，详细步骤请参见[使用控制台设置参数](../../../../../cn.zh-CN/RDS for MySQL 用户指南/实例管理/使用控制台设置参数.md#)。MySQL 5.5暂不支持修改此参数。

**说明：** 修改performance\_schema参数需要重启实例，重启前请做好业务安排，谨慎操作。

![修改参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8274/155477456643529_zh-CN.png)

