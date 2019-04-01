# RDS for MySQL备份、SQL审计相关问题 {#concept_fjx_2jz_ghb .concept}

1.  备份使用量在哪里查看？

    答：可以在实例的基本信息页面查看。

    ![备份使用量](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8256/155409855142107_zh-CN.png)

2.  备份使用量是如何构成的？

    答：备份使用量等于保存时间内备份集和binlog日志相加的大小。

3.  备份文件是否可以删除？

    答：请参见[删除备份数据](../../../../../cn.zh-CN/RDS for MySQL 用户指南/备份数据/删除备份数据.md#)。

4.  已经通过**一键上传Binlog**上传了Binlog日志，为什么备份使用量没有减少？

    答：**一键上传Binlog**功能是从当前实例存储空间中，将已经不再写入的Binlog文件上传到备份空间中，并且从RDS本地实例空间中删除Binlog文件，因此该功能不能减少备份使用量。

5.  如何减少备份使用量？

    答：

    -   考虑减少备份的保存天数。
    -   考虑减少备份的频率。
    -   考虑升级实例磁盘规格。
6.  SQL审计是否会影响实例性能？

    答：开通SQL审计功能不会影响实例性能，请放心使用。

7.  SQL审计采集量在哪里查看？

    答：可以在实例的基本信息页面查看。

    ![SQL审计采集量](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8256/155409855142105_zh-CN.png)

8.  是否可以删除部分SQL审计内容？

    答：目前还没有此功能，可以通过关闭SQL审计功能避免产生费用。

9.  SQL审计功能是否默认关闭？

    答：2016年2月25日后新购RDS实例会默认关闭SQL审计功能，存量实例需要用户手动关闭SQL审计，避免产生费用。

10. SQL 审计功能如何关闭？

    答：在SQL审计页面单击**关闭SQL审计**并**确定**。

    ![关闭SQL审计](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8256/155409855142106_zh-CN.png)

11. 关闭SQL审计功能后是否还可以查看已有的SQL审计内容？

    答：关闭SQL审计功能后，不能再查看SQL审计内容。


