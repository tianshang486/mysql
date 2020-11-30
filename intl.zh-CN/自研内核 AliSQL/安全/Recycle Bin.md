# Recycle Bin

由于DDL语句无法回滚，开发或运维人员如果误操作（例如DROP TABLE）可能会导致数据丢失。阿里云支持回收站（Recycle Bin）功能，临时将删除的表转移到回收站，还可以设置保留的时间，方便您找回数据，同时提供了工具包（DBMS\_RECYCLE）便于您快捷使用。

## Recycle Bin参数

Recycle Bin设计了如下五个参数。

|参数|说明|
|--|--|
|loose\_recycle\_bin|是否打开回收站功能，包括session级别和global级别。您可以在控制台修改参数。|
|loose\_recycle\_bin\_retention|回收站保留时间，单位：秒。默认为604800，即一周。您可以在控制台修改参数。|
|recycle\_scheduler|是否打开回收站的异步清理任务线程。暂不开放。|
|recycle\_scheduler\_interval|回收站异步清理任务线程的轮询间隔，单位：秒。默认为30。暂不开放。|
|recycle\_scheduler\_purge\_table\_print|是否打印异步清理现场工作的详细日志。暂不开放。|

## Recycle Bin介绍

-   回收/清理机制
    -   回收机制

        执行`TRUNCATE TABLE`语句时，将原始表移动到专门的recycle bin目录中，并在原位置使用相同的结构创建新表。

        执行`DROP TABLE/DATABASE`语句时，只保留相关的表对象，并移动到专门的recycle bin目录中。其它对象的删除策略如下：

        -   如果是与表无关的对象，根据操作语句决定是否保留，不做回收。
        -   如果是表的附属对象，可能会修改表数据的，做删除处理，例如Trigger和Foreign key。 但Column statistics不做清理，随表进入回收站。
    -   清理机制

        回收站会启动一个后台线程，来异步清理超过**recycle\_bin\_retention**时间的表对象。在清理回收站表的时候，如果遇到大表，会再启动一个后台线程异步删除大表。

-   权限

    RDS MySQL实例启动时，会初始化一个名为\_\_recycle\_bin\_\_的数据库，作为回收站使用的专有数据库。\_\_recycle\_bin\_\_是系统级数据库，您无法直接进行修改和删除。

    对于回收站内的表，虽然您无法直接执行`drop table`语句，但是可以使用`call dbms_recycle.purge_table('<TABLE>');`进行清理。

    **说明：** 账号在原表和回收站表都需要具有DROP权限。

-   回收站表命名规则

    Recycle Bin会从不同的数据库回收到统一的\_\_recycle\_bin\_\_数据库中，所以需要保证目标表表名唯一，所以定义了如下命名格式：

    ```
    "__" + <Storage Engine> + <SE private id>
    ```

    参数说明如下。

    |参数|说明|
    |--|--|
    |Storage Engine|存储引擎名称。|
    |SE private id|存储引擎为每一个表生成的唯一值。例如在InnoDB引擎中就是table id。|

-   独立回收

    回收的设置只会影响该实例本身，不会影响到binlog复制到的节点（备实例、只读实例和灾备实例）上。例如我们可以在主实例上设置回收，保留7天；在备实例上设置回收，保留14天。

    **说明：** 回收站保留周期不同，将导致实例的空间占用差别比较大。


## 注意事项

-   如果回收站数据库和待回收的表跨了文件系统，执行`drop table`语句将会搬迁表空间文件，耗时较长。
-   如果Tablespace为General，可能会存在多个表共享同一个表空间的情况，当回收其中一张表的时候，不会搬迁相关的表空间文件。

## 前提条件

实例版本为RDS MySQL 8.0。

## 管理Recycle Bin

AliSQL在DBMS\_RECYCLE中定义了两个管理接口。详细说明如下：

-   show\_tables

    展示回收站中所有临时保存的表。命令如下：

    ```
    call dbms_recycle.show_tables();
    ```

    示例：

    ```
    mysql> call dbms_recycle.show_tables();
    +-----------------+---------------+---------------+--------------+---------------------+---------------------+
    | SCHEMA          | TABLE         | ORIGIN_SCHEMA | ORIGIN_TABLE | RECYCLED_TIME       | PURGE_TIME          |
    +-----------------+---------------+---------------+--------------+---------------------+---------------------+
    | __recycle_bin__ | __innodb_1063 | product_db    | t1           | 2019-08-08 11:01:46 | 2019-08-15 11:01:46 |
    | __recycle_bin__ | __innodb_1064 | product_db    | t2           | 2019-08-08 11:01:46 | 2019-08-15 11:01:46 |
    | __recycle_bin__ | __innodb_1065 | product_db    | parent       | 2019-08-08 11:01:46 | 2019-08-15 11:01:46 |
    | __recycle_bin__ | __innodb_1066 | product_db    | child        | 2019-08-08 11:01:46 | 2019-08-15 11:01:46 |
    +-----------------+---------------+---------------+--------------+---------------------+---------------------+
    4 rows in set (0.00 sec)
    ```

    |参数|说明|
    |--|--|
    |SCHEMA|回收站的数据库名。|
    |TABLE|进入回收站后的表名。|
    |ORIGIN\_SCHEMA|原数据库名。|
    |ORIGIN\_TABLE|原表名。|
    |RECYCLED\_TIME|回收时间。|
    |PURGE\_TIME|预计从回收站删除的时间。|

-   purge\_table

    手动清理回收站中的表。命令如下：

    ```
    call dbms_recycle.purge_table('<TABLE>');
    ```

    **说明：**

    -   TABLE为进入回收站后的表名。
    -   账号在原表和回收站表都需要具有DROP权限。
    示例：

    ```
    call dbms_recycle.purge_table('__innodb_1063');
    ```

-   restore\_table

    恢复回收站内的表。命令如下：

    ```
    call dbms_recycle.restore_table('<RECYCLE_TABLE>','<DEST_DB>','<DEST_TABLE>');
    ```

    参数说明如下。

    |参数|说明|
    |--|--|
    |RECYCLE\_TABLE|需要恢复的回收站内的表名。**说明：** 如果仅传入此参数，会恢复到原始表。 |
    |DEST\_DB|目标数据库名。|
    |DEST\_TABLE|目标表名。|

    **说明：** 执行此命令需要有数据库\_\_recycle\_bin\_\_的ALTER\_ACL和DROP\_ACL权限，以及目标表的CREATE\_ACL和INSERT\_ACL权限。

    示例：

    ```
    mysql> call dbms_recycle.restore_table('__innodb_1063','testDB','testTable');
    ```


