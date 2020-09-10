# Thread Pool

为了发挥出RDS的最佳性能，阿里云提供线程池（Thread Pool）功能，将线程和会话分离，在拥有大量会话的同时，只需要少量线程完成活跃会话的任务即可。

## 优势

MySQL默认的线程使用模式是会话独占模式，每个会话都会创建一个独占的线程。当有大量的会话存在时，会导致大量的资源竞争，大量的系统线程调度和缓存失效也会导致性能急剧下降。

阿里云RDS的线程池实现了不同类型SQL操作的优先级及并发控制机制，将连接数始终控制在最佳连接数附近，使RDS数据库在高连接大并发情况下始终保持高性能。线程池的优势如下：

-   当大量线程并发工作时，线程池会自动调节并发的线程数量在合理的范围内，从而避免线程调度工作过多和大量缓存失效。
-   大量的事务并发执行时，线程池会将语句和事务分为不同的优先级，分别控制语句和事务的并发数量，从而减少资源竞争。
-   线程池给予管理类的SQL语句更高的优先级，保证这些语句优先执行。这样在系统负载很高时，新建连接、管理、监控等操作也能够稳定执行。
-   线程池给予复杂查询SQL语句相对较低的优先级，并且有最大并发数的限制。这样可以避免过多的复杂SQL语句将系统资源耗尽，导致整个数据库服务不可用。

## 前提条件

实例版本为RDS MySQL 5.6/5.7/8.0。

## 使用Thread Pool

Thread Pool设计了如下三个参数，您可以在控制台进行修改。详情请参见[设置实例参数](/cn.zh-CN/RDS MySQL 数据库/实例参数/参数模板/设置实例参数.md)。

|参数|说明|
|--|--|
|loose\_thread\_pool\_enabled|是否开启线程池功能。取值： -   ON
-   OFF

默认值：ON。

**说明：**

-   开启/关闭线程池功能使用本参数即可，不再使用参数**thread\_handling**进行控制。
-   开启/关闭线程池功能无需重启实例。 |
|loose\_thread\_pool\_size|分组的数量，默认值：4。线程池中的线程被平均分到多个组中进行管理。|
|loose\_thread\_pool\_oversubscribe|每个组中允许的活跃线程的数量，默认值：32。活跃线程是指正在执行SQL语句的线程，但是不包括以下两种情形： -   SQL语句在等待磁盘IO；
-   SQL语句在等待事务提交。 |

## 查询Thread Pool状态

您可以通过如下命令查询Thread Pool状态：

```
show status like "thread_pool%";
```

示例：

```
mysql> show status like "thread_pool%";

+----------------------------+-------+
| Variable_name              | Value |
+----------------------------+-------+
| thread_pool_active_threads | 1     |
| thread_pool_big_threads    | 0     |
| thread_pool_dml_threads    | 0     |
| thread_pool_idle_threads   | 19    |
| thread_pool_qry_threads    | 0     |
| thread_pool_total_threads  | 20    |
| thread_pool_trx_threads    | 0     |
| thread_pool_wait_threads   | 0     |
+----------------------------+-------+
8 rows in set (0.00 sec)            
```

参数说明如下。

|参数|说明|
|--|--|
|thread\_pool\_active\_threads|线程池中的活跃线程数。|
|thread\_pool\_big\_threads|线程池中正在执行复杂查询的线程数。复杂查询包括有子查询、聚合函数、group by、limit等的查询语句。|
|thread\_pool\_dml\_threads|线程池中的在执行DML的线程数。|
|thread\_pool\_idle\_threads|线程池中的空闲线程数。|
|thread\_pool\_qry\_threads|线程池中正在执行简单查询的线程数。|
|thread\_pool\_total\_threads|线程池中的总线程数。|
|thread\_pool\_trx\_threads|线程池中正在执行事务的线程数。|
|thread\_pool\_wait\_threads|线程池中正在等待磁盘IO、事务提交的线程数。|

## Sysbench测试

如下是开启线程池和不开启线程池的性能对比。从测试结果可以看出线程池在高并发的情况下有着明显的性能优势。

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6620649951/p55473.png)

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6620649951/p55474.png)

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6620649951/p55475.png)

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6620649951/p55476.png)

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6620649951/p55479.png)

