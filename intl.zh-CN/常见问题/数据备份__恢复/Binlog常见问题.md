# Binlog常见问题 {#concept_e2j_rsq_s2b .concept}

1.  问：Binlog文件记录的开始时间与结束时间中，有两个文件相差不大，为什么出现这种情况？每个文件的起始时间都是连续的吗？

    答：这两个文件分别是从主、备节点备份的Binlog，所以两个文件相差不会很大。每个文件起始时间是不同的。

2.  问：Binlog文件大小有压缩吗？

    答：Binlog文件没有压缩。

3.  问：Binlog生成、清理和上传的机制是什么？

    答：Binlog写满500MB就会生成新的Binlog日志文件继续写入，同时会根据本地备份设置将备份日志上传到OSS，并清理本地日志。详情请参见[MySQL设置本地Binlog](../../../../intl.zh-CN/RDS for MySQL 用户指南/备份数据/MySQL设置本地Binlog.md#)。


