# 定时任务（pg\_cron）

本文介绍如何通过RDS PostgreSQL提供的pg\_cron插件设置定时任务。

pg\_cron是基于cron的作业调度插件，语法与常规cron相同，但它可以直接从数据库执行PostgreSQL命令。

每一个定时任务分为两部分：

-   定时计划

    规定使用插件的计划，例如每隔1分钟执行一次该任务。

    定时计划使用标准的cron语法，其中**\***表示**任意时间都运行**，特定数字表示**仅在这个时间时运行**。

    ```
     ┌───────────── 分钟： 0 ~ 59
     │ ┌────────────── 小时： 0 ~ 23
     │ │ ┌─────────────── 日期： 1 ~ 31
     │ │ │ ┌──────────────── 月份： 1 ~ 12
     │ │ │ │ ┌───────────────── 一周中的某一天 ：0 ~ 6，0表示周日。
     │ │ │ │ │                  
     │ │ │ │ │
     │ │ │ │ │
     * * * * *
    ```

    如

    例如每周六3:30am（GMT）的语法为：

    ```
    30 3 * * 6
    ```

-   定时任务

    用户具体的任务内容，例如`select * from some_table`。


## 注意事项

-   定时任务执行的时间是GMT时间，请注意换算时间。
-   定时任务都储存于默认数据库postgres中，但是您可以在其他数据库上查询定时任务。
-   由于pg\_cron插件已升级，如果您在升级[内核小版本](/intl.zh-CN/自研内核 AliPG/AliPG 小版本 Release Nostes.md)20201130之前已经在使用pg\_cron，请重新创建插件来使用新的特性，但是重新创建后原有定时任务会丢失。

## 使用方法

-   创建插件

    ```
    CREATE EXTENSION pg_cron;
    ```

    **说明：** 仅高权限账号可以执行此命令。

-   删除插件

    ```
    DROP EXTENSION pg_cron;
    ```

    **说明：** 仅高权限账号可以执行此命令。

-   执行某个任务

    ```
    SELECT cron.schedule('<定时计划>', '<定时任务>')
    ```

    示例

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

-   指定数据库执行任务

    ```
    SELECT cron.schedule('<定时计划>', '<定时任务>', '<指定数据库>')
    ```

    **说明：** 不指定数据库时会使用配置文件中的默认数据库postgres。

-   删除某个任务

    ```
    SELECT cron.unschedule(<定时任务ID>)
    ```

    示例

    ```
    SELECT cron.unschedule(43);
    ```

-   查看当前任务列表

    ```
    SELECT * FROM cron.job;
    ```

-   查看任务执行记录

    ```
    SELECT * FROM cron.job_log;
    ```


