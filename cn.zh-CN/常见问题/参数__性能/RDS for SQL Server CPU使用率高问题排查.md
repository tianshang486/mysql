# RDS for SQL Server CPU使用率高问题排查 {#concept_x2f_35m_jhb .concept}

RDS for SQL Server使用过程中，会遇到CPU使用率过高甚至达到100%的情况。本文将介绍造成该状况的常见原因以及解决方法。

## 常见原因 {#section_nzt_55m_jhb .section}

RDS for SQL Server CPU使用率高的因素有很多，其中最常见的是应用的负载高、查询语句的成本高，或者是实例的并行度设置不合理。

## 实例的并行度设置不合理 {#section_omr_gvm_jhb .section}

**问题排查**

多线程并行处理任务时，由于每个线程处理的数据量不一致，会出现CXPACKET等待情况，CXPACKET等待发生比较多的话，造成CPU使用率高。可以通过SQL Server Management Studio的活动监视器或者下面语句（多次执行取差值），监控是否存在大量CXPACKET等待。

**说明：** CXPACKET指线程正在等待彼此完成并行处理。当SQL Server发现一条指令复杂时，会决定用多个线程并行来执行，由于某些并行线程已完成工作，在等待其它并行线程来同步，这种等待就叫CXPACKET。

```
WITH [Waits] AS
    (SELECT
        [wait_type],
        [wait_time_ms] / 1000.0 AS [WaitS],
        ([wait_time_ms] - [signal_wait_time_ms]) / 1000.0 AS [ResourceS],
        [signal_wait_time_ms] / 1000.0 AS [SignalS],
        [waiting_tasks_count] AS [WaitCount],
       100.0 * [wait_time_ms] / SUM ([wait_time_ms]) OVER() AS [Percentage],
        ROW_NUMBER() OVER(ORDER BY [wait_time_ms] DESC) AS [RowNum]
    FROM sys.dm_os_wait_stats
    WHERE [wait_type] NOT IN (
        N'BROKER_EVENTHANDLER', N'BROKER_RECEIVE_WAITFOR',
        N'BROKER_TASK_STOP', N'BROKER_TO_FLUSH',
        N'BROKER_TRANSMITTER', N'CHECKPOINT_QUEUE',
        N'CHKPT', N'CLR_AUTO_EVENT',
        N'CLR_MANUAL_EVENT', N'CLR_SEMAPHORE',
        -- Maybe uncomment these four if you have mirroring issues
        N'DBMIRROR_DBM_EVENT', N'DBMIRROR_EVENTS_QUEUE',
        N'DBMIRROR_WORKER_QUEUE', N'DBMIRRORING_CMD',
        N'DIRTY_PAGE_POLL', N'DISPATCHER_QUEUE_SEMAPHORE',
        N'EXECSYNC', N'FSAGENT',
        N'FT_IFTS_SCHEDULER_IDLE_WAIT', N'FT_IFTSHC_MUTEX',
        -- Maybe uncomment these six if you have AG issues
        N'HADR_CLUSAPI_CALL', N'HADR_FILESTREAM_IOMGR_IOCOMPLETION',
        N'HADR_LOGCAPTURE_WAIT', N'HADR_NOTIFICATION_DEQUEUE',
        N'HADR_TIMER_TASK', N'HADR_WORK_QUEUE',
        N'KSOURCE_WAKEUP', N'LAZYWRITER_SLEEP',
        N'LOGMGR_QUEUE', N'MEMORY_ALLOCATION_EXT',
        N'ONDEMAND_TASK_QUEUE',
        N'PREEMPTIVE_XE_GETTARGETSTATE',
        N'PWAIT_ALL_COMPONENTS_INITIALIZED',
        N'PWAIT_DIRECTLOGCONSUMER_GETNEXT',
        N'QDS_PERSIST_TASK_MAIN_LOOP_SLEEP', N'QDS_ASYNC_QUEUE',
        N'QDS_CLEANUP_STALE_QUERIES_TASK_MAIN_LOOP_SLEEP',
        N'QDS_SHUTDOWN_QUEUE', N'REDO_THREAD_PENDING_WORK',
        N'REQUEST_FOR_DEADLOCK_SEARCH', N'RESOURCE_QUEUE',
        N'SERVER_IDLE_CHECK', N'SLEEP_BPOOL_FLUSH',
        N'SLEEP_DBSTARTUP', N'SLEEP_DCOMSTARTUP',
        N'SLEEP_MASTERDBREADY', N'SLEEP_MASTERMDREADY',
        N'SLEEP_MASTERUPGRADED', N'SLEEP_MSDBSTARTUP',
        N'SLEEP_SYSTEMTASK', N'SLEEP_TASK',
        N'SLEEP_TEMPDBSTARTUP', N'SNI_HTTP_ACCEPT',
        N'SP_SERVER_DIAGNOSTICS_SLEEP', N'SQLTRACE_BUFFER_FLUSH',
        N'SQLTRACE_INCREMENTAL_FLUSH_SLEEP',
        N'SQLTRACE_WAIT_ENTRIES', N'WAIT_FOR_RESULTS',
        N'WAITFOR', N'WAITFOR_TASKSHUTDOWN',
        N'WAIT_XTP_RECOVERY',
        N'WAIT_XTP_HOST_WAIT', N'WAIT_XTP_OFFLINE_CKPT_NEW_LOG',
        N'WAIT_XTP_CKPT_CLOSE', N'XE_DISPATCHER_JOIN',
        N'XE_DISPATCHER_WAIT', N'XE_TIMER_EVENT')
    AND [waiting_tasks_count] > 0
    )
SELECT
    MAX ([W1].[wait_type]) AS [WaitType],
    CAST (MAX ([W1].[WaitS]) AS DECIMAL (16,2)) AS [Wait_S],
    CAST (MAX ([W1].[ResourceS]) AS DECIMAL (16,2)) AS [Resource_S],
    CAST (MAX ([W1].[SignalS]) AS DECIMAL (16,2)) AS [Signal_S],
    MAX ([W1].[WaitCount]) AS [WaitCount],
    CAST (MAX ([W1].[Percentage]) AS DECIMAL (5,2)) AS [Percentage],
    CAST ((MAX ([W1].[WaitS]) / MAX ([W1].[WaitCount])) AS DECIMAL (16,4)) AS [AvgWait_S],
    CAST ((MAX ([W1].[ResourceS]) / MAX ([W1].[WaitCount])) AS DECIMAL (16,4)) AS [AvgRes_S],
    CAST ((MAX ([W1].[SignalS]) / MAX ([W1].[WaitCount])) AS DECIMAL (16,4)) AS [AvgSig_S]
FROM [Waits] AS [W1]
INNER JOIN [Waits] AS [W2]
    ON [W2].[RowNum] <= [W1].[RowNum]
GROUP BY [W1].[RowNum]
HAVING SUM ([W2].[Percentage]) - MAX( [W1].[Percentage] ) < 95; -- percentage threshold
GO
```

**解决方案**

-   **从语句级别进行设置**
    1.  通过查询语句寻找消耗CPU的语句，SQL如下：

        ```
        SELECT TOP 50
        [Avg. MultiCore/CPU time(sec)] = qs.total_worker_time / 1000000 / qs.execution_count,
        [Total MultiCore/CPU time(sec)] = qs.total_worker_time / 1000000,
        [Avg. Elapsed Time(sec)] = qs.total_elapsed_time / 1000000 / qs.execution_count,
        [Total Elapsed Time(sec)] = qs.total_elapsed_time / 1000000,
        qs.execution_count,
        [Avg. I/O] = (total_logical_reads + total_logical_writes) / qs.execution_count,
        [Total I/O] = total_logical_reads + total_logical_writes,
        Query = SUBSTRING(qt.[text], (qs.statement_start_offset / 2) + 1,
        (
        (
        CASE qs.statement_end_offset
        WHEN -1 THEN DATALENGTH(qt.[text])
        ELSE qs.statement_end_offset
        END - qs.statement_start_offset
        ) / 2
        ) + 1
        ),
        Batch = qt.[text],
        [DB] = DB_NAME(qt.[dbid]),
        qs.last_execution_time,
        qp.query_plan
        FROM sys.dm_exec_query_stats AS qs
        CROSS APPLY sys.dm_exec_sql_text(qs.[sql_handle]) AS qt
        CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle) AS qp
        where qs.execution_count > 5        --more than 5 occurences
        ORDER BY [Total MultiCore/CPU time(sec)] DESC
        ```

    2.  对于RDS for SQL Server 2008 R2实例，可以在控制台查看慢日志统计，查找消耗CPU的语句。

        ![控制台慢日志统计](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8350/155488117444064_zh-CN.png)

    3.  找到语句之后，查看其执行计划，对于并行度较高的语句，可以在语句级别使用hint查询，限制语句并行度。示例如下：

        ```
        SELECT column1,column2 
            FROM table1 o INNER JOIN table2 d ON (o.d_id = d.d_id) 
            OPTION (maxdop 1)
        ```

-   **从实例级别进行设置**
    1.  查看当前实例的MAXDOP值，SQL如下：

        ```
        select * from sys.configurations where name like '%max%'
        ```

        ![查询maxdop](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8350/155488117444072_zh-CN.png)

    2.  在实例级别设置该参数，对所有查询均生效，SQL如下：

        ```
        sp_rds_configure 'max degree of parallelism', 1;  
        GO
        ```

        对于RDS for SQL Server 2008 R2实例，可以在RDS管理控制台的参数设置中进行手动设置，需提交参数生效。

        ![修改maxdop](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8350/155488117444085_zh-CN.png)


## 应用负载高 {#section_agv_3cn_jhb .section}

**现象**

没有出现慢查询（或者慢查询不是问题主要原因），QPS和CPU使用率曲线变化吻合。常见于应用优化过的在线事务交易系统（比如订单系统）、高读取率的热门Web网站应用等。

**特征**

实例的QPS高，查询比较简单、执行效率高、优化余地小。

**解决方案**

建议从应用架构、实例规格等方面来解决：

-   升级实例规格，增加CPU资源。
-   尽量优化查询，减少查询的执行成本（逻辑IO，执行需要访问的表数据行数），提高应用可扩展性。

## 查询语句的读写过高 {#section_alb_xcn_jhb .section}

**现象**

存在慢查询，QPS和CPU使用率曲线变化不吻合，检查消耗CPU的语句，存在I/O较大的语句。

**特征**

实例的QPS不高；查询执行效率低、执行需要扫描大量表中数据、优化余地大。

**解决方案**

-   对于大表查询，检查是否有合适的索引。检查实际执行计划，针对全表扫描操作进行优化，执行计划中也会给出缺失索引的建议。

    ![缺失索引检查](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8350/155488117444101_zh-CN.png)

-   通过CloudDBA检查性能问题。

## 避免出现CPU使用100%的一般原则 {#section_oxb_mfn_jhb .section}

-   设置CPU使用率告警，实例CPU使用率保证一定的冗余度。
-   应用设计和开发过程中，要考虑查询的优化，遵守SQL优化的一般优化原则，降低查询的逻辑 I/O，提高应用可扩展性。
-   新功能、新模块上线前，要使用生产环境数据进行压力测试。
-   经常使用CloudDBA查看实例各项性能，及时发现问题。

