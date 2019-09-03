# 常用 SQL 命令（MySQL） {#concept_jqv_vpv_ydb .concept}

本章内容列举了部分常用 SQL 命令，此处仅做展示，如需了解更详细的 SQL 命令信息，包括命令参数和限制条件等，请参见 [MySQL 参考指南（官方）](http://dev.mysql.com/doc/refman/5.7/en/)。

## 数据库相关 {#section_uy3_2qv_ydb .section}

|命令|示例|
|--|--|
|创建数据库并指定字符集| ```
create database db01 DEFAULT CHARACTER SET gbk COLLATE gbk_chinese_ci;
```

 |
|删除数据库| ```
drop database db01;
```

 |

## 账号相关 { .section}

**说明：** 一个具有高权限账号的实例，不能通过高权限账号修改其他账号的密码。如果需要修改，只能删除账号后重新创建。

|命令|示例|
|--|--|
|创建账号| ```
CREATE USER 'username'@'host' IDENTIFIED BY 'password';
```

 |
|删除账号| ```
DROP USER 'username'@'host';
```

 |
|赋权| ```
GRANT SELECT ON db01.* TO 'username'@'host';
```

 |
|查询数据库中的账号|```
SELECT user,host,password FROM mysql.user_view;
```

或 ```
show grants for xxx
```

|
|权限回收| -   收回全部权限

    ```
REVOKE ALL PRIVILEGES,GRANT OPTION FROM 'username'@'host';
    ```

-   收回指定权限

    ```
REVOKE UPDATE ON *.* FROM 'username'@'host';
    ```


 |

