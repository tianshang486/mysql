# RDS for MySQL 连接数满情况的处理 {#concept_41714_zh .concept}

连接数满会导致客户端无法连接到RDS for MySQL数据库。

连接数满通常是两种原因导致的：

-   空闲连接过多。
-   活动连接过多。

## 空闲连接过多 {#section_ik1_svb_5gb .section}

 **原因**

-   应用使用长连接模式：对于长连接模式（比如Java应用），应用侧应该配置连接池。连接池的初始连接数设置过高，应用启动后建立多个到RDS实例空闲连接。
-   应用使用短连接模式：对于短连接模式（比如PHP应用），出现大量的空闲连接说明应用没有在查询执行完毕后**显式**的关闭连接。

![空闲连接过多](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8305/155012242838821_zh-CN.png)

 **解决方法**

-   通过DMS或者`kill`命令来终止当前空闲会话，详细步骤请参见[RDS for MySQL如何终止会话](cn.zh-CN/常见问题/网络__IP/RDS for MySQL如何终止会话.md#)。
-   修改应用，长连接模式需要启用连接池的复用功能（建议也启用连接检测功能）。
-   修改应用，短连接模式需要在代码中修改查询结束后调用关闭连接的方法。
-   对于非交互模式连接，在控制台的参数设置里设置wait\_timeout参数为较小值。wait\_timeout参数控制非交互模式连接的超时时间（单位秒，默认值为24小时即86400秒），当非交互式连接空闲时间超过wait\_timeout指定的时间后，RDS实例会主动关闭连接。

    ![修改wait_timeout](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8305/155012242838822_zh-CN.png)

-   对于交互模式连接，在控制台的参数设置里设置interactive\_timeout参数为较小值。interactive\_timeout参数控制交互模式连接的超时时间（单位秒，默认值为2小时即7200秒），当交互式连接空闲时间超过interactive\_timeout指定的时间后，RDS实例会主动关闭连接。

    ![修改interactive_timeout](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8305/155012242838823_zh-CN.png)


**说明：** 

-   在RDS for MySQL实例连接数完全打满的情况下，**通过DMS或者其他方式是无法连接实例的**；因此对于长连接模式，建议连接池的最大连接数要略小于实例规格的连接数限制，比如保留10个连接给DMS或其他管理操作使用。当发生无法连接的情况时，建议先在控制台修改wait\_timeout参数为较小值，促使RDS实例主动关闭空闲时间超过阈值的连接。
-   通常情况下，应用到RDS实例会采用非交互模式，具体采用哪个模式需要查看应用的连接方式配置，比如PHP通过传递MYSQL\_CLIENT\_INTERACTIVE常量给mysql\_connect\(\)函数即可开启连接的交互模式。
-   wait\_timeout和interactive\_timeout这两个参数的修改，修改前已经存在的会话保持修改前的设置，修改后新创建的会话使用新的参数设置。

## 活动连接过多 {#section_hns_tvb_5gb .section}

 **原因**

-   锁等待导致活动连接数堆积（包括InnoDB锁等待、表元数据锁等待）。
-   CPU使用率过高导致活动连接数堆积。
-   IOPS使用率高导致活动连接数堆积。

![活动连接过多](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8305/155012242838824_zh-CN.png)

 **解决方法**

-   InnoDB锁等待处理，请参见[RDS for MySQL InnoDB 锁等待和锁等待超时的处理](https://help.aliyun.com/knowledge_detail/41705.html)。
-   表元数据锁等待，请参见[解决MDL锁导致无法操作数据库的问题](../../../../../cn.zh-CN/最佳实践/MySQL/解决MDL锁导致无法操作数据库的问题.md#)。
-   CPU使用率高导致活动连接数堆积，请参见[MySQL CPU 使用率高的原因和解决方法](cn.zh-CN/常见问题/产品性能/MySQL CPU 使用率高的原因和解决方法.md#)。
-   IOPS使用率高导致活动连接数堆积，请参见[MySQL IOPS 使用率高的原因和解决方法](https://help.aliyun.com/knowledge_detail/51807.html)。

