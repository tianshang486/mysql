# MySQL系统文件导致实例空间满的解决办法 {#concept_j21_knj_3gb .concept}

MySQL实例可能会由于长时间不结束的查询导致 ibdata1 文件过大且无法收缩，导致实例空间满，为避免数据丢失，RDS会对实例进行自动锁定，磁盘锁定之后，将无法进行写入操作。

## 背景信息 {#section_tsc_ny1_3gb .section}

当实例由于实例空间满自动锁定时，控制台可以在**基本信息** \> **运行状态**看到如下信息。

![实例空间满](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85053/156894552835652_zh-CN.png)

## 前提条件 {#section_xgd_ny1_3gb .section}

-   对于MySQL 5.6版本的实例，升级实例存储空间后即可解锁实例，关于如何升级实例配置，请参见[变更配置](../../../../cn.zh-CN/RDS for MySQL 用户指南/实例管理/变更配置.md#)，若实例存储空间已到最大值，请提交工单联系客服临时解锁实例，再进行后续操作。
-   对于MySQL 5.5/5.7版本的实例，请提交工单联系客服临时解锁实例，再进行后续操作。

## 实施步骤 {#section_ayd_ny1_3gb .section}

注意事项

-   清理临时文件有延迟，请耐心等待实例已使用空间的下降。
-   由于MySQL 5.7开始采用独立的临时表空间ibtmp1，可以通过重启实例的方式释放空间。对于MySQL5.5/5.6实例，在不升级磁盘空间的前提下，比较好的解决方法是在同地域同可用区购买相同配置的RDS实例，通过 DTS 工具将数据迁移到新实例中。

操作步骤

1.  在同地域同可用区购买相同配置的RDS实例，具体请参见[创建RDS for MySQL实例](../../../../cn.zh-CN/RDS for MySQL 快速入门/创建RDS for MySQL实例.md#)。
2.  登录[RDS管理控制台](https://rdsnext.console.aliyun.com/)。
3.  在右上角单击**迁移数据库**。

    ![迁移数据库](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/86146/156894552835952_zh-CN.png)

4.  具体迁移配置请参见[RDS实例间的数据迁移](https://help.aliyun.com/document_detail/26626.html)。

## 后续维护 {#section_lbp_rh3_3gb .section}

-   避免出现执行效率很差的SQL大量执行的情况。
-   尽量在业务低峰期进行索引创建删除、表结构修改、表维护和表删除操作。
-   建议您监控和清理执行时间过长的会话或事务。

## 更多信息 {#section_gxp_4y1_3gb .section}

-   [数据文件导致实例空间满的解决办法](cn.zh-CN/常见问题/空间__内存/MySQL数据文件导致实例空间满的解决办法.md#)
-   [Binlog文件导致实例空间满的解决办法](cn.zh-CN/常见问题/空间__内存/MySQL Binlog文件导致实例空间满的解决办法.md#)
-   [临时文件导致实例空间满的解决办法](cn.zh-CN/常见问题/空间__内存/MySQL临时文件导致实例空间满的解决办法.md#)

