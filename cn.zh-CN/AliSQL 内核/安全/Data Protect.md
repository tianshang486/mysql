# Data Protect

RDS MySQL提供数据保护功能，通过控制高危险的删除操作的权限，实现数据保护。

实例版本如下：

-   MySQL 8.0（[内核小版本](/cn.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)为20200430或以上）
-   MySQL 5.7（[内核小版本](/cn.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)为20200430或以上）
-   MySQL 5.6（[内核小版本](/cn.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)为20200430或以上）

Data Protect进行数据保护的范围如下：

-   危险的数据操作命令：
    -   `Drop Table`
    -   `Truncate Table`
    -   `Alter Table Drop Paritition`
    -   `Alter Table Truncate Partition`
    -   `Alter Table Exchange Paritition`
    -   `Drop Tablespace`
-   扩展命令：

    -   `DROP View`
    -   `ALTER View`
    -   `Drop Function`
    -   `Drop Procedure`
    -   `Drop Trigger`
    -   `Purge Binary Logs`
    **说明：** 限制扩展命令主要是为了保证应用程序代码的正常运行。


## 参数说明

Data Protect功能涉及4个参数，详细说明如下：

-   rds\_data\_protect\_level

    设定数据保护的级别，取值如下：

    -   NONE：禁用Data Protect。
    -   DDL：阻止对数据库或表的DROP和TRUNCATE操作。
    -   ALL：阻止所有DROP和TRUNCATE操作，包括视图、存储过程、函数、触发器。
    **说明：** 建议您在非维护或非发布阶段开启Data Protect Level功能，在维护或发布阶段临时关闭。

-   rds\_data\_protect\_ignore

    指定不需要进行保护的数据库列表。适用于某些特殊业务环境，例如当研发和生产数据库在同一个实例时，可以不保护研发所用的数据库。

-   rds\_data\_protect\_admin

    当保护策略指定为用户模式时，用来指定可以进行数据删除操作的用户，只有指定的用户才能进行删除操作。

-   rds\_data\_protect\_control

    设定数据保护策略，目前提供4种保护策略：

    -   USER：由指定的用户（rds\_data\_protect\_admin参数指定）或拥有SUPER\_ACL权限的用户才能进行删除操作。适用于大多数云上用户，可以自行执行删除操作。
    -   SUPER：拥有SUPER\_ACL权限的用户才能进行删除操作。可以通过SUPER\_ACL的精确控制，实现数据保护，适用于线下一般应用。
    -   MAINTAIN：拥有SUPER\_ACL权限和MAINTAIN连接权限（指云平台发起的连接）的用户才能进行删除操作。适用于在云平台进行删除操作。
    -   LOCAL：拥有SUPER\_ACL权限和MAINTAIN连接权限（指云平台发起的连接）的用户通过本地连接登录实例才能进行删除操作。适用于核心应用，此模式禁止远程连接的删除操作，必须要登录到物理机才能进行删除操作。

## 启用Data Protect

Data Protect目前处于邀请测试阶段，您如果感兴趣，可以[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)申请开通此功能。

## 测试准备

-   测试环境
    1.  在实例中创建两个数据库，一个为需要保护的数据库，另一个为不需要保护的数据库。示例如下：

        ```
        mysql> show databases like '%db';
        +----------------+
        | Database (%db) |
        +----------------+
        | ignore_db      |
        | protect_db     |
        +----------------+
        2 rows in set (0.00 sec)
        ```

    2.  在两个数据库中都创建表t\_binlog，并设置rds\_data\_protect相关参数。示例如下：

        ```
        mysql> set global rds_data_protect_level=DDL;
        Query OK, 0 rows affected (0.00 sec)
        
        mysql> set global rds_data_protect_ignore='ignore_db';
        Query OK, 0 rows affected (0.00 sec)
        mysql> set global rds_data_protect_admin='admin';
        Query OK, 0 rows affected (0.00 sec)
        mysql> set global rds_data_protect_control=USER;
        Query OK, 0 rows affected (0.00 sec)
        
        mysql> show variables like 'rds_data_protect_%';
        +--------------------------+-----------+
        | Variable_name            | Value     |
        +--------------------------+-----------+
        | rds_data_protect_admin   | admin     |
        | rds_data_protect_control | USER      |
        | rds_data_protect_ignore  | ignore_db |
        | rds_data_protect_level   | DDL       |
        +--------------------------+-----------+
        4 rows in set (0.01 sec)
        ```

-   测试账号

    为验证4种保护模式，需要创建4个账号，分别具有不同权限。如下所示：

    -   test@'%'：普通账号，为表的所有者。
    -   admin@'%'：高权限账号，允许进行删表操作的账号。
    -   root@'%'：SUPER\_ACL权限账号，但不具备MAINTAIN连接权限。
    -   aliyun\_root@'%'：SUPER\_ACL权限账号，且具备MAINTAIN连接权限。

## USER模式测试

1.  用test账号在受保护的数据库下进行Truncate操作会被拒绝。示例如下：

    ```
    mysql> select user(), database();
    +--------------------+------------+
    | user()             | database() |
    +--------------------+------------+
    | test@xx.xx.xxx.xxx | protect_db |
    +--------------------+------------+
    1 row in set (0.00 sec)
    
    mysql> show tables;
    +----------------------+
    | Tables_in_protect_db |
    +----------------------+
    | t_binlog             |
    +----------------------+
    1 row in set (0.00 sec)
    
    mysql> truncate table t_binlog;
    ERROR 7533 (HY000): Operation rejected by RDS data protection policy
    ```

2.  用test账号在不受保护的数据库下进行Truncate操作，可以正常执行。示例如下：

    ```
    mysql> select user(), database();
    +--------------------+------------+
    | user()             | database() |
    +--------------------+------------+
    | test@xx.xx.xxx.xxx | ignore_db  |
    +--------------------+------------+
    1 row in set (0.00 sec)
    
    mysql> truncate table t_binlog;
    Query OK, 0 rows affected (0.01 sec)
    ```

3.  用admin账号在受保护的数据库下进行Truncate操作，可以正常执行（`global rds_data_protect_admin='admin'`）。示例如下：

    ```
    mysql> select user(), database();
    +---------------------+------------+
    | user()              | database() |
    +---------------------+------------+
    | admin@xx.xx.xxx.xxx | protect_db |
    +---------------------+------------+
    1 row in set (0.00 sec)
    
    mysql> truncate table t_binlog;
    Query OK, 0 rows affected (0.01 sec)
    ```


## SUPER模式测试

1.  将模式切换为SUPER。示例如下：

    ```
    mysql> set global rds_data_protect_control=SUPER;
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> show variables like 'rds_data_protect_%';
    +--------------------------+-----------+
    | Variable_name            | Value     |
    +--------------------------+-----------+
    | rds_data_protect_admin   | admin     |
    | rds_data_protect_control | SUPER     |
    | rds_data_protect_ignore  | ignore_db |
    | rds_data_protect_level   | DDL       |
    +--------------------------+-----------+
    4 rows in set (0.00 sec)
    ```

2.  用admin账号在受保护的数据库下进行Truncate操作会被拒绝。示例如下：

    ```
    mysql> select user(), database();
    +---------------------+------------+
    | user()              | database() |
    +---------------------+------------+
    | admin@xx.xx.xxx.xxx | protect_db |
    +---------------------+------------+
    1 row in set (0.00 sec)
    
    mysql> truncate table t_binlog;
    ERROR 7533 (HY000): Operation rejected by RDS data protection policy
    ```

3.  用root账号在受保护的数据库下进行Truncate操作，可以正常执行。示例如下：

    ```
    mysql> select user(), database();
    +----------------+------------+
    | user()         | database() |
    +----------------+------------+
    | root@localhost | protect_db |
    +----------------+------------+
    1 row in set (0.00 sec)
    
    mysql> truncate table t_binlog;
    Query OK, 0 rows affected (0.01 sec)
    ```


## MAINTAIN模式测试

1.  将模式切换为MAINTAIN。示例如下：

    ```
    mysql> set global rds_data_protect_control=maintain;
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> show variables like 'rds_data_protect_%';
    +--------------------------+-----------+
    | Variable_name            | Value     |
    +--------------------------+-----------+
    | rds_data_protect_admin   | admin     |
    | rds_data_protect_control | MAINTAIN  |
    | rds_data_protect_ignore  | ignore_db |
    | rds_data_protect_level   | DDL       |
    +--------------------------+-----------+
    4 rows in set (0.01 sec)
    ```

    **说明：** 切换到MAINTAIN模式后，root账号就不能再修改保护策略。

    ```
    mysql> set global rds_data_protect_control=maintain;
    ERROR 7533 (HY000): Operation rejected by RDS data protection policy
    ```

2.  用root账号在受保护的数据库下进行Truncate操作会被拒绝。示例如下：

    ```
    mysql> select user(), database();
    +----------------+------------+
    | user()         | database() |
    +----------------+------------+
    | root@localhost | protect_db |
    +----------------+------------+
    1 row in set (0.00 sec)
    
    mysql> truncate table t_binlog;
    ERROR 7533 (HY000): Operation rejected by RDS data protection policy
    ```

3.  用aliyun\_root账号在受保护的数据库下进行Truncate操作，可以正常执行。示例如下：

    ```
    mysql> select user(), database();
    +-----------------------+------------+
    | user()                | database() |
    +-----------------------+------------+
    | aliyun_root@localhost | protect_db |
    +-----------------------+------------+
    1 row in set (0.01 sec)
    
    mysql> truncate table t_binlog;
    Query OK, 0 rows affected (0.01 sec)
    ```


## LOCAL模式测试

1.  将模式切换为LOCAL。示例如下：

    ```
    mysql> select user(), database();
    +-----------------------+------------+
    | user()                | database() |
    +-----------------------+------------+
    | aliyun_root@localhost | protect_db |
    +-----------------------+------------+
    1 row in set (0.00 sec)
    
    mysql> set global rds_data_protect_control=local;
    Query OK, 0 rows affected (0.00 sec)
    
    mysql> show variables like 'rds_data_protect_%';
    +--------------------------+-----------+
    | Variable_name            | Value     |
    +--------------------------+-----------+
    | rds_data_protect_admin   | admin     |
    | rds_data_protect_control | LOCAL     |
    | rds_data_protect_ignore  | ignore_db |
    | rds_data_protect_level   | DDL       |
    +--------------------------+-----------+
    4 rows in set (0.01 sec)
    ```

    **说明：** 切换到LOCAL模式后，远程连接的aliyun\_root账号就不能再修改保护策略。

    ```
    mysql> set global rds_data_protect_control=user;
    ERROR 7533 (HY000): Operation rejected by RDS data protection policy
    ```

2.  用远程连接的aliyun\_root账号在受保护的数据库下进行Truncate操作会被拒绝。示例如下：

    ```
    mysql> select user(), database();
    +----------------------------+------------+
    | user()                     | database() |
    +----------------------------+------------+
    | aliyun_root@xx.xxx.xxx.xxx | protect_db |
    +----------------------------+------------+
    1 row in set (0.00 sec)
    
    mysql> truncate table t_binlog;
    ERROR 7533 (HY000): Operation rejected by RDS data protection policy
    ```

3.  用本地登录的aliyun\_root账号在受保护的数据库下进行Truncate操作，可以正常执行。示例如下：

    ```
    mysql> select user(), database();
    +-----------------------+------------+
    | user()                | database() |
    +-----------------------+------------+
    | aliyun_root@localhost | protect_db |
    +-----------------------+------------+
    1 row in set (0.00 sec)
    
    mysql> truncate table t_binlog;
    Query OK, 0 rows affected (0.00 sec)
    ```


