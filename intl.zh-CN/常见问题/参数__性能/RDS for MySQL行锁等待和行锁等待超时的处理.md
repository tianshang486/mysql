# RDS for MySQL行锁等待和行锁等待超时的处理 {#concept_ns4_pxy_3hb .concept}

## 出现场景 {#section_jpn_5zy_3hb .section}

当一个连接会话等待另外一个会话持有的互斥行锁时，就会发生行锁等待情况。

通常情况下，持有该互斥行锁的会话会迅速的执行完相关操作并释放掉持有的互斥锁（事务提交或者回滚），然后等待的会话在行锁等待超时时间内获得该互斥行锁，进行下一步操作。

但在某些情况下，比如一个实例未感知到的来自客户端应用的数据库会话中断，持有该互斥行锁的会话长时间不释放该互斥行锁，此时如果有其他会话申请该互斥行锁，则会导致大量的行锁等待与行锁等待超时。

行锁等待超时的报错如下：

```
ERROR 1205 (HY000): Lock wait timeout exceeded; try restarting transaction
```

## 处理方法 {#section_zkh_bbz_3hb .section}

本文提供的检查和处理方法，仅当正在发生行锁等待的情况下才成立。因为RDS for MySQL行锁等待默认超时时间为50秒，通常情况下不容易观察到行锁等待的现场，可以通过将**innodb\_lock\_wait\_timeout**参数设置为较大值来复现问题（生产环境不推荐使用过大的**innodb\_lock\_wait\_timeout**参数值）。

1.  [通过DMS登录RDS数据库](../../../../../intl.zh-CN/RDS for MySQL 用户指南/附录/通过DMS登录RDS数据库.md#)。
2.  单击**性能** \> **InnoDB锁等待**，检查导致锁等待和锁超时的会话。

    ![InnoDB锁等待](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8271/155471254743494_zh-CN.png)

3.  对于标识为**Blocker**的会话（持有锁阻塞其他会话的DML操作，导致行锁等待和行锁等待超时），确认可以接受其对应的事务回滚的情况下，可以将其终止。

