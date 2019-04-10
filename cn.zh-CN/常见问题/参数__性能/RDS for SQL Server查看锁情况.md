# RDS for SQL Server查看锁情况 {#concept_dr5_3sl_jhb .concept}

## 查看锁 {#section_yfh_4sl_jhb .section}

通过sys.dm\_tran\_locks系统视图查看锁的情况，查询哪些数据库有锁，SQL如下：

```
select str(request_session_id, 4, 0) as spid,
convert(varchar(20), db_name(resource_database_id)) as DB_Name,
case when resource_database_id = db_id() and resource_type = 'OBJECT'
then convert(char(20), object_name(resource_Associated_Entity_id))
else convert(char(20), resource_Associated_Entity_id)
end as object,
convert(varchar(12), resource_type) as resrc_type,
convert(varchar(12), request_type) as req_type,
convert(char(3), request_mode) as mode,
convert(varchar(8), request_status) as status
from sys.dm_tran_locks
order by request_session_id desc;
```

![系统视图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8329/155486776643744_zh-CN.png)

**说明：** **MODE**列是锁的模式，介绍如下：

-   共享（S）用于不更改或不更新数据的操作（只读操作），如SELECT语句。
-   更新（U）用于可更新的资源中。防止当多个会话在读取、锁定以及随后可能进行的资源更新时发生常见形式的死锁。
-   排它（X）用于数据修改操作，例如INSERT、UPDATE或DELETE，确保不会同时同一资源进行多重更新。
-   意向锁用于建立锁的层次结构。意向锁的类型为：意向共享（IS）、意向排它（IX）以及与意向排它共享（SIX）。
-   架构锁在执行依赖于表架构的操作时使用。架构锁的类型为：架构修改（Sch-M）和架构稳定性（Sch-S）。
-   大容量更新（BU）向表中大容量复制数据并指定了TABLOCK提示时使用。

也可以查询哪些表有锁，SQL如下：

```
select request_session_id sessionid,
resource_type type,
convert(varchar(20), db_name(resource_database_id)) as db_name,
OBJECT_NAME(resource_associated_entity_id, resource_database_id) objectname,
request_mode rmode,
request_status rstatus
from sys.dm_tran_locks
where resource_type in ('OBJECT')
```

![表锁](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8329/155486776643753_zh-CN.png)

**说明：** 

-   **sessionid**：锁表的进程。
-   **objectname**：被锁的表名。

