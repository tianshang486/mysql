# Data Protect

RDS MySQL提供数据保护功能，通过控制高危险的删除操作的权限，实现数据保护。

实例版本如下：

-   MySQL 8.0（[内核小版本](/intl.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)为20200430或以上）
-   MySQL 5.7（[内核小版本](/intl.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)为20200430或以上）
-   MySQL 5.6（[内核小版本](/intl.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)为20200430或以上）

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

Data Protect目前处于邀请测试阶段，您如果感兴趣，可以[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)申请开通此功能。

