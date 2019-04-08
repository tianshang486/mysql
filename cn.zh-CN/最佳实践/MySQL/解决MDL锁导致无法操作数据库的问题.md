# 解决MDL锁导致无法操作数据库的问题 {#concept_csn_5tt_4fb .concept}

异常情况下的元数据锁MDL（metadata lock）会阻塞后续对表的操作，本文介绍通过DMS工具解决该问题。

## 背景信息 {#section_gd3_s2x_3hb .section}

MySQL 5.5版本开始，引入了MDL锁，用于解决或者保证DDL操作与DML操作之间的一致性，但是在部分场景下会出现阻塞，例如执行DML操作时执行ALTER操作、存在长时间查询时执行ALTER操作等等。

## 出现场景 {#section_usb_t2x_3hb .section}

-   创建、删除索引。
-   修改表结构。
-   表维护操作（optimize table、repair table 等）。
-   删除表。
-   获取表级写锁 。

## 原因 {#section_rvn_sfx_3hb .section}

-   当前有对表的长时间查询。
-   显示或者隐式开启事务后未提交或回滚，比如查询完成后未提交或者回滚。
-   表上有失败的查询事务。

## 操作步骤 {#section_w3f_m2x_3hb .section}

1.  使用DMS登录[RDS数据库](https://dms.console.aliyun.com/#/dms/login)。

    **说明：** 网络地址:端口需要输入对应RDS实例的内网地址及内网端口，可在RDS实例基本信息页面查看。

2.  在首页上方选择**SQL操作** \> **SQL窗口**。
3.  在命令行输入show full processlist;并执行，查看所有线程状态，在**State**列发现大量**Waiting for table metadata lock**即表示出现阻塞，在对应的**Info**列可以查看到是对哪个表的操作，找到正在对该表进行操作的会话，记下**Id**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24465/155469081214301_zh-CN.png)

    **说明：** 

    -   这里需要找到的是一直在占用该表的会话，而不是正在等待MDL锁解除的会话，注意区分。可以根据**State**列的状态和**Info**列的命令内容来进行分析判断。
    -   您也可以用如下命令查询长时间未完成的事务，如果导致阻塞的语句的用户与当前用户不同，请使用导致阻塞的语句的用户登录来终止会话。

        ```
        select concat('kill ',i.trx_mysql_thread_id,';') from information_schema.innodb_trx i,
          (select 
                 id, time
             from
                 information_schema.processlist
             where
                 time = (select 
                         max(time)
                     from
                         information_schema.processlist
                     where
                         state = 'Waiting for table metadata lock'
                             and substring(info, 1, 5) in ('alter' , 'optim', 'repai', 'lock ', 'drop ', 'creat'))) p
          where timestampdiff(second, i.trx_started, now()) > p.time
          and i.trx_mysql_thread_id  not in (connection_id(),p.id);
        ```

4.  在命令行输入kill**Id数字**，例如 kill 267，即可中断会话，解除MDL锁。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24465/155469081214302_zh-CN.png)


## 后续维护 {#section_imb_ygx_3hb .section}

-   在业务低峰期执行相关场景操作，例如创建索引、删除索引等。
-   开启事务自动提交autocommit。
-   设置参数lock\_wait\_timeout为较小值。
-   考虑使用事件来终止长时间运行的事务，比如下面的例子中会终止执行时间超过60分钟的事务。

    ```
    create event my_long_running_trx_monitor
    on schedule every 60 minute
    starts '2015-09-15 11:00:00'
    on completion preserve enable do
    begin
      declare v_sql varchar(500);
      declare no_more_long_running_trx integer default 0; 
      declare c_tid cursor for
        select concat ('kill ',trx_mysql_thread_id,';') 
        from information_schema.innodb_trx 
        where timestampdiff(minute,trx_started,now()) >= 60;
      declare continue handler for not found
        set no_more_long_running_trx=1;
      open c_tid;
      repeat
        fetch c_tid into v_sql;
     set @v_sql=v_sql;
     prepare stmt from @v_sql;
     execute stmt;
     deallocate prepare stmt;
      until no_more_long_running_trx end repeat;
      close c_tid;
    end;
    ```


