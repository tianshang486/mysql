# 数据库定时任务（pg\_cron插件）

RDS PostgreSQL提供pg\_cron插件，可以设置定时任务。

实例为RDS PostgreSQL 11。

**说明：** 仅新购实例支持，存量实例请[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)开通。

pg\_cron是基于cron的作业调度插件，与常规cron保持相同的语法，但它可以直接从数据库安排PostgreSQL命令。

每一个定时任务分为两部分：

-   定时计划

    规定了用户使用插件的计划，例如每隔1分钟执行一次该任务。

-   定时任务

    用户具体的任务内容，例如`select * from some_table`。


## 语法

pg\_cron使用标准的cron语法，其中**\***表示**任意时间都运行**，特定数字表示**仅在这个数字时运行**。

```
 ┌───────────── 分钟 (0 - 59)
 │ ┌────────────── 小时 (0 - 23)
 │ │ ┌─────────────── 日期 (1 - 31)
 │ │ │ ┌──────────────── 月份 (1 - 12)
 │ │ │ │ ┌───────────────── 一周中的某一天 (0 - 6) (0表示周日）
 │ │ │ │ │                  
 │ │ │ │ │
 │ │ │ │ │
 * * * * *
```

## 示例

-   创建插件

    ```
    CREATE EXTENSION pg_cron;
    ```

-   增加任务项

    ```
    -- 周六3:30am (GMT) 删除过期数据。 
    SELECT cron.schedule('30 3 * * 6', $$DELETE FROM events WHERE event_time < now() - interval '1 week'$$);
    
    ----------
    
    -- 每天的10:00am (GMT) 执行磁盘清理。
    SELECT cron.schedule('0 10 * * *', 'VACUUM');
    
    ----------
    
    -- 每分钟执行指定脚本。
    SELECT cron.schedule('* * * * *', 'select 1;')；
    
    ----------
    
    -- 每个小时的23分执行指定脚本。
    SELECT cron.schedule('23 * * * *', 'select 1;')；
    
    ----------
    
    -- 每个月的4号执行指定脚本。
    SELECT cron.schedule('* * 4 * *', 'select 1;')；
    ```

-   查看当前任务

    ```
    SELECT * FROM cron.job;
    
     jobid | schedule   |  command  | nodename  | nodeport | database | username | active 
    -------+------------+-----------+-----------+----------+----------+----------+--------
        43 | 0 10 * * * |   VACUUM; | localhost |     5433 | postgres | test     | t
    ```

-   删除任务项

    ```
    SELECT cron.unschedule(43);
    ```

    **说明：** 43为jobid。


