# MySQL Binlog文件导致实例空间满的解决办法 {#concept_smh_123_3gb .concept}

MySQL实例可能会由于大事务快速生成Binlog文件，导致实例空间满，为避免数据丢失，RDS会对实例进行自动锁定，磁盘锁定之后，将无法进行写入操作。

## 背景信息 {#section_tsc_ny1_3gb .section}

当实例由于实例空间满自动锁定时，控制台可以在**基本信息** \> **运行状态**看到如下信息：

![实例空间满](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85053/155425504035652_zh-CN.png)

## 前提条件 {#section_xgd_ny1_3gb .section}

-   对于MySQL 5.6版本的实例，升级实例存储空间后即可解锁实例，关于如何升级实例配置，请参见[变更配置](../../../../../cn.zh-CN/RDS for MySQL 用户指南/实例管理/变更配置.md#)，若实例存储空间已到最大值，请提交工单联系客服临时解锁实例，再进行后续操作。
-   对于MySQL 5.5/5.7版本的实例，请提交工单联系客服临时解锁实例，再进行后续操作。

## 实施步骤 {#section_ayd_ny1_3gb .section}

**注意事项**

-   Binlog 文件记录实例的事务信息，是MySQL实例高可用性、可恢复性的基础，建议不要关闭。可以通过[一键上传Binlog](https://help.aliyun.com/knowledge_detail/60546.html)到阿里云OSS来释放磁盘空间或者修改[本地Binlog设置](../../../../../cn.zh-CN/RDS for MySQL 用户指南/备份数据/MySQL设置本地Binlog.md#)。
-   清理Binlog文件有延迟，请耐心等待实例已使用空间的下降。
-   **一键上传Binlog**会在后台异步提交清理任务，清理任务会将已写入的Binlog上传到OSS （非用户购买的 OSS）上，然后再从实例空间中删除Binlog文件，当前正在被写入的Binlog文件由于未完成写入，是不可以被清理的。因此，清理过程会有一定延迟，建议您单击**一键上传 Binlog**后耐心等待一定时间，请勿多次单击该按钮，可以到基本信息页中查看已用空间是否减小。
-   由于 DML 等操作（比如涉及大字段的 DML 操作）导致快速生成Binlog，可能会出现上传Binlog文件到备份空间并且从实例空间中删除的处理速度跟不上实例生成Binlog文件的速度，在这种情况下，建议考虑升级磁盘空间，并且排查Binlog快速生成的原因。

**一键上传Binlog**

1.  登录[RDS管理控制台](https://rdsnext.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。
3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**备份恢复**。
5.  在右上角单击**一键上传Binlog**，在弹出的对话框中单击**确定**。

    ![一键上传Binlog](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85438/155425504035873_zh-CN.png)


**修改本地Binlog设置**

1.  登录[RDS管理控制台](https://rdsnext.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。
3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**备份恢复**。
5.  选择本地日志设置页签，单击**编辑**，将空间使用率不超过设置为30%，**可用空间保护**设置为开启。

    **说明：** 

    -   **保留时长**为每隔多久上传一次Binlog日志到OSS，并清理本地Binlog日志。若设置为0，表示本地不保存Binlog日志，直接上传到OSS。
    -   本地Binlog空间使用率 = 本地Binlog大小 / 实例总可用（购买）空间大小。此为循环使用空间，超出后，则从最早的Binlog开始清理，直到空间使用率低于该比例。
    -   当实例总空间使用率超过80%或剩余空间不足5GB时，会强制清理Binlog。从最早的开始清理，直到总空间使用率降到80%以下且剩余空间大于5GB。
    ![本地日志设置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85438/155425504035874_zh-CN.png)


## 更多信息 {#section_gxp_4y1_3gb .section}

-   [数据文件导致实例空间满的解决办法](cn.zh-CN/常见问题/空间__内存/MySQL数据文件导致实例空间满的解决办法.md#)
-   [临时文件导致实例空间满的解决办法](cn.zh-CN/常见问题/空间__内存/MySQL临时文件导致实例空间满的解决办法.md#)
-   [系统文件导致实例空间满的解决办法](cn.zh-CN/常见问题/空间__内存/MySQL系统文件导致实例空间满的解决办法.md#)

