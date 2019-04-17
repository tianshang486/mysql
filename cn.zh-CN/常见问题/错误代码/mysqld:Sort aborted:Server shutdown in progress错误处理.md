# mysqld:Sort aborted:Server shutdown in progress错误处理 {#concept_185531 .concept}

## 错误信息 {#section_g71_pc2_mwb .section}

在控制台查看**日志管理** \> **错误日志**，出现类似如下错误。

![错误信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8267/155547024244639_zh-CN.png)

## 错误原因及解释 {#section_bw2_zes_o0v .section}

-   在查询执行排序的过程中实例进行了重启，导致查询中断。

    由于重启导致的查询中断是正常现象。

-   在查询执行排序的过程中，通过kill命令或者DMS实例会话功能终止了查询会话。

    这是由于MySQL的bug导致输出的错误信息，可以忽略。详情请参见[MySQL BUG](https://bugs.mysql.com/bug.php?id=18256)。


