# SQL防火墙（sql\_firewall插件）

SQL防火墙是数据库层面的防火墙功能，可以防止恶意SQL注入。可以用来学习一些定义好的SQL规则，并将这些规则储存在数据库中作为白名单，学习完成后，可以限制用户执行这些定义规则之外的风险操作。

RDS PostgreSQL实例需为以下版本之一：

-   PostgreSQL 12
-   PostgreSQL 11
-   PostgreSQL 10

## 学习模式、预警模式与防火墙模式

![流程图](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5919259951/p162105.png)

SQL防火墙支持如下三种模式：

-   学习模式：防火墙记录用户执行的SQL，并添加到常用SQL白名单。
-   预警模式：防火墙对用户将执行的SQL进行判断，如果SQL不在白名单中，仍然会执行该SQL，但是会告警用户该SQL不在白名单中。
-   防火墙模式：防火墙对用户将执行的SQL进行判断，如果SQL不在白名单中，防火墙会拒绝执行该SQL并返回错误提示。

## SQL防火墙的使用步骤

1.  打开防火墙的学习模式，让防火墙记录用户执行的SQL，并加入白名单。这个过程建议持续一段较长的时间，尽量让防火墙学习到所有可能执行的SQL。
2.  切换防火墙为预警模式，这个过程防火墙会对用户的一些不在白名单的SQL进行告警，用户结合自己的业务判断是否为风险SQL，如果这些SQL确实是用户需要的业务语句，则记录这些SQL，之后打开学习模式进行二次学习。
3.  经过前两步，用户常用SQL已经被记录完毕，打开防火墙模式，此时不在白名单的SQL均会被拒绝执行。

## 操作说明

-   创建插件

    ```
    create extension sql_firewall;
    ```

-   删除插件

    ```
    drop extension sql_firewall;
    ```

-   切换模式

    在控制台找到**sql\_firewall.firewall**参数，修改参数值并重启实例。详情请参见[设置实例参数](/cn.zh-CN/RDS PostgreSQL 数据库/实例/设置实例参数.md)。

    **sql\_firewall.firewall**取值如下：

    -   disable：关闭SQL防火墙
    -   learning：学习模式
    -   permissive：预警模式
    -   enforcing：防火墙模式
-   功能函数
    -   sql\_firewall\_reset\(\)

        清空白名单。该函数只有在防火墙关闭模式下，rds\_superuser权限的用户可执行该函数。

    -   sql\_firewall\_stat\_reset\(\)

        清空统计信息。该函数只有在防火墙关闭模式下，rds\_superuser权限的用户可执行该函数。

-   视图函数
    -   sql\_firewall.sql\_firewall\_statements

        展示目前数据库中所有的白名单及其被调用的次数。

        ```
        postgres=# select * from sql_firewall.sql_firewall_statements;
             userid |  queryid   |              query              | calls
            --------+------------+---------------------------------+-------
                 10 | 3294787656 | select * from k1 where uid = ?; |     4
            (1 row)
        ```

    -   sql\_firewall.sql\_firewall\_stat

        展示预警模式下的警告数量（sql\_warning）和防火墙模式下的错误数量（sql\_error）。

        ```
        postgres=# select * from sql_firewall.sql_firewall_stat;
             sql_warning | sql_error
            -------------+-----------
                       2 |         1
            (1 row)
        ```


## 示例

```
--预警模式

    postgres=# select * from sql_firewall.sql_firewall_statements;
    WARNING:  Prohibited SQL statement
     userid |  queryid   |              query              | calls
    --------+------------+---------------------------------+-------
         10 | 3294787656 | select * from k1 where uid = 1; |     1
    (1 row)

    postgres=# select * from k1 where uid = 1;
     uid |    uname
    -----+-------------
       1 | Park Gyu-ri
    (1 row)

    postgres=# select * from k1 where uid = 3;
     uid |   uname
    -----+-----------
       3 | Goo Ha-ra
    (1 row)

    postgres=# select * from k1 where uid = 3 or 1 = 1;
    WARNING:  Prohibited SQL statement
     uid |     uname
    -----+----------------
       1 | Park Gyu-ri
       2 | Nicole Jung
       3 | Goo Ha-ra
       4 | Han Seung-yeon
       5 | Kang Ji-young
    (5 rows)

--防火墙模式

    postgres=# select * from k1 where uid = 3;
     uid |   uname
    -----+-----------
       3 | Goo Ha-ra
    (1 row)

    postgres=# select * from k1 where uid = 3 or 1 = 1;
    ERROR:  Prohibited SQL statement
    postgres=#
```

