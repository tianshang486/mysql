# RDS for SQL Server查看内存占用情况 {#concept_r5r_lnh_hhb .concept}

## 操作步骤 {#section_f2v_pnh_hhb .section}

1.  使用客户端连接实例，请参见[连接实例](../../../../../cn.zh-CN/RDS for SQL Server 快速入门/连接实例.md#)。
2.  在SQL窗口中执行以下命令。

    ```
    select count(*)*8/1024 as 'cache size(MB)',
    case database_id
    when 32767 then 'ResourceDb'
    else DB_NAME(database_id)
    end as 'datebase'
    from sys.dm_os_buffer_descriptors
    group by DB_NAME(database_id),database_id
    order by 'cache size(MB)' desc
    ```


