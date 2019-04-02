# RDS for SQL Server 回收表空间 {#concept_uwy_k4h_hhb .concept}

RDS for SQL Server在删除变长列或者减小变长列的长度后，表的大小不会自动减小。

变长列包括的字段：varchar、nvarchar、varchar\(max\)、nvarchar\(max\)、varbinary、text、ntext、image、sql\_variant、varbinary\(max\)、xml。

## 解决方法 {#section_gmp_y4h_hhb .section}

-   SQL Server 提供了一个`DBCC CLEANTABLE`命令可以回收表或索引视图中，已删除可变长度列的空间。语法如下：

    ```
    DBCC CLEANTABLE  
    (  
        { database_name | database_id | 0 }  
        , { table_name | table_id | view_name | view_id }  
        [ , batch_size ]  
    )  
    [ WITH NO_INFOMSGS ]
    ```

    **说明：** 

    -   database\_name | database\_id | 0：要清除的表所在的数据库。 如果指定0，则使用当前数据库。
    -   table\_name | table\_id | view\_name | view\_id：要清除的表或索引视图。
    -   batch\_size：每个事务处理的行数。 如果未指定，或指定为0，则该语句将在一个事务中处理整个表。
    -   WITH NO\_INFOMSGS：取消显示所有信息性消息。
    **示例**

    ```
    DBCC CLEANTABLE (testDB,'testTable', 0)  
    WITH NO_INFOMSGS;  
    GO
    ```

-   重建索引或者reorganized索引。

空间是不会自动回收的，每个记录都占了一个位置。即使删除了数据，位置也会空在那里，下次插入记录的时候，会优先选这些空的槽位。您可以考虑定时重建聚集索引。另外，即使收缩了表的空间，数据库的数据文件大小不会变小。要收缩 一个SQLServer的数据文件，必须用[DBCC SHRINKDATABASE](https://docs.microsoft.com/zh-cn/sql/t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql?view=sql-server-2017)命令收缩指定数据库的指定数据或日志文件大小，或者用[DBCC SHRINKFILE](https://docs.microsoft.com/zh-cn/sql/t-sql/database-console-commands/dbcc-shrinkfile-transact-sql?view=sql-server-2017)收缩当前数据库的指定数据或日志文件大小。MySQL表的空间是独立的一个文件，所以收缩MySQL的大表，可以收缩整体数据库的大小，但是SQL Server所有的表都是在数据库的文件里，只有收缩文件才可以缩小空间。

