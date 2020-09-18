# Binlog in Redo

Binlog in Redo功能指在事务提交时将Binlog内容同步写入到Redo Log中，减少对磁盘的操作，提高数据库性能。

实例版本为MySQL 8.0（内核小版本20200430或以上）。

在MySQL关键业务场景中，为了业务数据的安全，事务提交时必须实时保存对应的Binlog和Redo Log，即以下两个参数必须同时设置为1：

```
sync_binlog = 1;
innodb_flush_log_at_trx_commit = 1;
```

由于每个事务提交会对磁盘进行两次I/O操作，虽然Binlog采用了Group Commit的方式合并I/O来提升效率，但两次I/O等待的本质没有改变，影响事务处理的效率，当使用云盘存储时，影响会更明显。I/O合并的效率是由同时提交的并发事务数量决定的，当并发量不够时I/O合并的效果也不理想，表现为少量的写操作事务提交时所需要的时间比较久，响应时间较长。

为了提高事务提交效率，AliSQL精心设计了Binlog in Redo机制（设置参数`persist_binlog_to_redo = on`开启），即在事务提交时将Binlog内容同步写入到Redo Log中。当事务提交时，只需要将Redo Log保存到磁盘中，从而减少一次对磁盘的操作，而Binlog文件则采用异步的方式，用单独的线程周期性的保存到磁盘中。在异常重启后，系统会用Redo Log中的Binlog内容来补齐Binlog文件。由于减少了一次I/O操作，性能得到了提升，响应时间变的更短，同时Binlog文件保存次数的减少，极大地降低了文件系统因文件长度实时变化带来的文件同步（fsync）压力，也提升了文件系统的性能。

Binlog in Redo功能不会改变Binlog的格式，基于Binlog的复制及第三方工具也不会受任何影响。

## 参数介绍

-   persist\_binlog\_to\_redo

    Binlog in Redo功能开关。全局系统变量，取值：on或off。修改本参数立刻生效，不需要重启实例。

    **说明：** 您只需要设置`persist_binlog_to_redo = on`即可正常使用Binlog in Redo功能，不需要修改其他参数（`sync_binlog = 1`自动失效）。

-   sync\_binlog\_interval

    Binlog异步保存的间隔。全局系统变量，当`persist_binlog_to_redo = on`时生效。默认值：50，单位：毫秒（ms），通常使用默认值即可。修改本参数立刻生效，不需要重启实例。


## 性能压力测试

-   测试环境
    -   应用服务器：阿里云ECS实例
    -   RDS实例规格： 32核、64 GB内存、ESSD云盘
    -   实例类型：高可用版（数据复制方式为异步复制）
-   测试用例

    使用的Sysbench内置用例如下：

    -   oltp\_update\_non\_index
    -   oltp\_insert
    -   oltp\_write\_only
-   测试结果
    -   oltp\_update\_non\_index

        开启Binlog in Redo后，QPS在低并发场景下提升显著，延迟也较低。

        ![oltp_update_non_index-QPS](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2720649951/p129994.png)

        ![oltp_update_non_index-laterncy](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2720649951/p129995.png)

    -   oltp\_insert

        开启Binlog in Redo后，QPS在低并发场景下提升显著，延迟也较低。

        ![oltp_insert-QPS](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2720649951/p129996.png)

        ![oltp_insert-latency](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2720649951/p129997.png)

    -   oltp\_write\_only

        开启Binlog in Redo后，QPS在低并发场景下有所提升，延迟也较低。

        ![oltp_write_only-QPS](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2720649951/p129998.png)

        ![oltp_write_only-latency](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2720649951/p129999.png)

    -   Binlog Fsync次数对比

        开启Binlog in Redo后，Binlog fsync的次数大幅降低。

        ![Binlog Fsync](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2720649951/p130000.png)


## 测试总结

-   oltp\_update\_non\_index和oltp\_insert只包含单语句事务，事务提交次数多，而oltp\_write\_only包含多语句事务（2个UPDATE、1个DELETE、1个INSERT），相比oltp\_update\_non\_index和oltp\_insert，事务提交次数较少，所以oltp\_update\_non\_index和oltp\_insert的性能提升比oltp\_write\_only更为明显。
-   在低于256并发时，Binlog in Redo功能可以明显提升性能和降低延迟。对绝大多数的实际使用场景来说，Binlog in Redo效果显著。
-   Binlog in Redo功能开启后会大幅降低Binlog fsync的次数，可以提升文件系统的性能。

