# RDS for MySQL如何查看消耗内存高的事件和线程 {#concept_1426145 .concept}

本文介绍如何查看消耗内存高的事件和线程，为您解决内存相关问题提供参考。

内存是重要的性能参数，内存使用率过高会导致系统响应速度变慢，严重时内存耗尽实例会进行主备切换，导致业务中断。因此我们需要在内存异常升高时及时排查问题，避免影响业务。

## 前提条件 {#section_7bg_dqy_bej .section}

实例版本如下：

-   MySQL 5.7
-   MySQL 8.0

## 操作步骤 {#section_i32_2n6_op9 .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156471003936543_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**参数设置**。
5.  修改参数**performance\_schema**为**ON**，如果已经为**ON**请忽略此步骤。

    **说明：** 该操作会重启实例造成连接中断，重启前请做好业务安排，谨慎操作。

    1.  单击![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135180/156471003953730_zh-CN.png)，修改值为**ON**，单击**确定**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135180/156471003953729_zh-CN.png)

    2.  单击右上角**提交参数**，等待实例重启完成。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135180/156471003953732_zh-CN.png)

6.  使用DMS或客户端[连接MySQL实例](../cn.zh-CN/RDS for MySQL 快速入门/连接MySQL实例.md#)。
7.  执行如下命令打开内存监控：

    ``` {#codeblock_tb4_8hk_sct}
    update performance_schema.setup_instruments set enabled = 'yes' where name like 'memory%';
    select * from performance_schema.setup_instruments where name like 'memory%innodb%' limit 5;
    ```

    **说明：** 该命令是在线打开内存统计，所以只会统计打开后新增的内存对象，打开前的内存对象不会统计，建议您打开后等待一段时间再执行后续步骤，便于找出内存使用高的线程。

8.  您可以执行命令统计事件和线程的内存消耗量，并进行排序展示。

    -   统计事件消耗内存：

        ``` {#codeblock_4rc_s3n_zfe}
        select event_name,SUM_NUMBER_OF_BYTES_ALLOC  from 
          performance_schema.memory_summary_global_by_event_name 
            order by SUM_NUMBER_OF_BYTES_ALLOC desc LIMIT 10;
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135180/156471003953733_zh-CN.png)

    -   统计线程消耗内存：

        ``` {#codeblock_tjc_iws_wx1}
        select thread_id,event_name, SUM_NUMBER_OF_BYTES_ALLOC from 
          performance_schema.memory_summary_by_thread_by_event_name 
            order by SUM_NUMBER_OF_BYTES_ALLOC desc limit 20;
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135180/156471004053734_zh-CN.png)

    **说明：** 您也可以执行如下命令查看详细的监控信息：

    ``` {#codeblock_hkp_2z9_7bd}
    select * from sys.x$memory_by_host_by_current_bytes   ;
    select * from sys.x$memory_by_thread_by_current_bytes ;
    select * from sys.x$memory_by_user_by_current_bytes   ;
    select * from sys.x$memory_global_by_current_bytes    ;
    select * from sys.x$memory_global_total               ;
    
    select * from performance_schema.memory_summary_by_account_by_event_name;
    select * from performance_schema.memory_summary_by_host_by_event_name;
    select * from performance_schema.memory_summary_by_thread_by_event_name;
    select * from performance_schema.memory_summary_by_user_by_event_name;
    select * from performance_schema.memory_summary_global_by_event_name;
    
    select event_name,current_alloc from sys.memory_global_by_current_bytes where event_name like '%innodb%';
    select event_name,current_alloc from sys.memory_global_by_current_bytes limit 5;
    select m.thread_id tid,   USER,   esc.DIGEST_TEXT,   total_allocated  FROM   sys.memory_by_thread_by_current_bytes m,   performance_schema.events_statements_current esc WHERE m.`thread_id` = esc.THREAD_ID \G
    ```


## 下一步 {#section_ltr_n10_700 .section}

找到问题事件或线程后，您可以排查业务代码和环境，解决内存高的问题。

