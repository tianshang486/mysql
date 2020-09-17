# 分片代理（PL/Proxy）

PL/Proxy插件包含CLUSTER模式和CONNECT模式，可以帮助您用不同方式访问数据库。

实例版本如下：

-   PostgreSQL 12（内核小版本20200421及以上）
-   PostgreSQL 11（内核小版本20200402及以上）

**说明：** 您可以在**基本信息**页面的**配置信息**区域查看是否有**升级内核小版本**按钮。如果有按钮，您可以单击按钮查看当前版本；如果没有按钮，表示已经是最新版。详情请参见[升级内核小版本](/cn.zh-CN/RDS PostgreSQL 数据库/实例/升级内核小版本.md)。

![pgsql升级内核](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/4919259951/p101917.png)

PL/Proxy插件包含如下两种模式：

-   CLUSTER模式

    支持数据库水平拆分和SQL复制。

-   CONNECT模式

    支持将SQL请求路由到指定的数据库。


更多PL/Proxy插件使用方法请参见[PL/Proxy](https://plproxy.github.io/tutorial.html)。

## 注意事项

-   相同VPC内的PostgreSQL实例可以直接跨库操作。
-   不同VPC内的PostgreSQL实例可以通过本VPC内的ECS实例进行端口跳转，实现跨库操作。
-   代理节点后端的数据节点数必须是2的N次方。

## 测试环境

选择一个数据库实例作为代理节点，另外两个数据库实例作为数据节点。详细信息如下。

|IP|节点类型|数据库名|用户名|
|--|----|----|---|
|100.xx.xx.136|代理节点|postgres|postgres|
|100.xx.xx.72|数据节点|pl\_db0|postgres|
|11.xx.xx.9|数据节点|pl\_db1|postgres|

## 创建PL/Proxy插件

创建PL/Proxy插件命令如下：

```
create extension plproxy
```

## 创建PL/Proxy集群

**说明：** CONNECT模式不需要进行本操作。

1.  创建PL/Proxy集群，指定连接的子节点的数据库名、IP地址和端口，示例如下：

    ```
    postgres=# CREATE SERVER cluster_srv1 FOREIGN DATA WRAPPER plproxy
    postgres-# OPTIONS (
    postgres(#         connection_lifetime '1800',
    postgres(#         disable_binary '1',
    postgres(#         p0 'dbname=pl_db0 host=100.xxx.xxx.72 port=5678',
    postgres(#         p1 'dbname=pl_db1 host=11.xxx.xxx.9 port=5678'
    postgres(#         );
    CREATE SERVER
    ```

2.  为postgres用户赋予权限，示例如下：

    ```
    postgres=# grant usage on FOREIGN server cluster_srv1 to postgres;
    GRANT 
    ```

3.  创建用户映射，示例如下：

    ```
    postgres=> create user mapping for postgres server cluster_srv1 options (user 'postgres');
    CREATE USER MAPPING
    ```


## 创建测试表

在每个数据节点创建测试表（代理节点不需要创建），示例如下：

```
create table users(userid int, name text);
```

## CLUSTER模式测试

数据水平拆分测试步骤如下：

1.  在每个数据节点创建插入函数，示例如下：

    ```
    pl_db0=> CREATE OR REPLACE FUNCTION insert_user(i_id int, i_name text)
    pl_db0-> RETURNS integer AS $$
    pl_db0$>        INSERT INTO users (userid, name) VALUES ($1,$2);
    pl_db0$>        SELECT 1;
    pl_db0$> $$ LANGUAGE SQL;
    CREATE FUNCTION
    
    pl_db1=> CREATE OR REPLACE FUNCTION insert_user(i_id int, i_name text)
    pl_db1-> RETURNS integer AS $$
    pl_db1$>        INSERT INTO users (userid, name) VALUES ($1,$2);
    pl_db1$>        SELECT 1;
    pl_db1$> $$ LANGUAGE SQL;
    CREATE FUNCTION
    ```

2.  在代理节点创建同名的插入函数，示例如下：

    ```
    postgres=> CREATE OR REPLACE FUNCTION insert_user(i_id int, i_name text)
    postgres-> RETURNS integer AS $$
    postgres$>     CLUSTER 'cluster_srv1';
    postgres$>     RUN ON ANY;
    postgres$> $$ LANGUAGE plproxy;
    CREATE FUNCTION
    ```

3.  在代理节点创建读取函数，示例如下：

    ```
    postgres=> CREATE OR REPLACE FUNCTION get_user_name()
    postgres-> RETURNS TABLE(userid int, name text) AS $$
    postgres$>     CLUSTER 'cluster_srv1';
    postgres$>     RUN ON ALL ;
    postgres$> SELECT userid,name FROM users;
    postgres$> $$ LANGUAGE plproxy;
    CREATE FUNCTION
    ```

4.  在代理节点插入10条测试记录，示例如下：

    ```
    SELECT insert_user(1001, 'Sven');
    SELECT insert_user(1002, 'Marko');
    SELECT insert_user(1003, 'Steve');
    SELECT insert_user(1004, 'lottu');
    SELECT insert_user(1005, 'rax');
    SELECT insert_user(1006, 'ak');
    SELECT insert_user(1007, 'jack');
    SELECT insert_user(1008, 'molica');
    SELECT insert_user(1009, 'pg');
    SELECT insert_user(1010, 'oracle');
    ```

5.  由于插入函数执行的是RUN ON ANY，即插入数据时随机选取数据节点，查看每个数据节点的数据如下：

    ```
    pl_db0=> select * from users;
     userid |  name
    --------+--------
       1001 | Sven
       1003 | Steve
       1004 | lottu
       1005 | rax
       1006 | ak
       1007 | jack
       1008 | molica
       1009 | pg
    (8 rows)
    
    pl_db1=> select * from users;
     userid |  name
    --------+--------
       1002 | Marko
       1010 | oracle
    (2 rows)
    ```

    **说明：** 通过查询可以发现10条数据分布在不同数据节点，由于10条数据太少，导致分布不均匀。

6.  在代理节点执行读取函数，由于执行的是RUN ON ALL，即代理节点返回所有数据节点查询结果，示例如下：

    ```
    postgres=> SELECT USERID,NAME FROM GET_USER_NAME();
     userid |  name
    --------+--------
       1001 | Sven
       1003 | Steve
       1004 | lottu
       1005 | rax
       1006 | ak
       1007 | jack
       1008 | molica
       1009 | pg
       1002 | Marko
       1010 | oracle
    (10 rows)
    ```


SQL复制测试步骤如下：

1.  在各个节点创建清理函数用于清理表users数据，示例如下：

    ```
    pl_db0=> CREATE OR REPLACE FUNCTION trunc_user()
    pl_db0-> RETURNS integer AS $$
    pl_db0$>        truncate table users;
    pl_db0$>        SELECT 1;
    pl_db0$> $$ LANGUAGE SQL;
    CREATE FUNCTION
    
    pl_db1=> CREATE OR REPLACE FUNCTION trunc_user()
    pl_db1-> RETURNS integer AS $$
    pl_db1$>        truncate table users;
    pl_db1$>        SELECT 1;
    pl_db1$> $$ LANGUAGE SQL;
    CREATE FUNCTION
    
    postgres=> CREATE OR REPLACE FUNCTION trunc_user()
    postgres-> RETURNS SETOF integer AS $$
    postgres$>     CLUSTER 'cluster_srv1';
    postgres$>     RUN ON ALL;
    postgres$> $$ LANGUAGE plproxy;
    CREATE FUNCTION
    ```

2.  在代理节点执行清理函数，示例如下：

    ```
    postgres=> SELECT TRUNC_USER();
     trunc_user
    ------------
              1
              1
    (2 rows)
    ```

3.  在代理节点创建插入函数，示例如下：

    ```
    postgres=> CREATE OR REPLACE FUNCTION insert_user_2(i_id int, i_name text)
    postgres-> RETURNS SETOF integer AS $$
    postgres$>     CLUSTER 'cluster_srv1';
    postgres$>     RUN ON ALL;
    postgres$> TARGET insert_user;
    postgres$> $$ LANGUAGE plproxy;
    CREATE FUNCTION
    ```

4.  在代理节点插入4条测试记录，示例如下：

    ```
    SELECT insert_user_2(1004, 'lottu');
    SELECT insert_user_2(1005, 'rax');
    SELECT insert_user_2(1006, 'ak');
    SELECT insert_user_2(1007, 'jack');
    ```

5.  查看每个数据节点的数据，示例如下：

    ```
    pl_db0=> select * from users;
     userid | name
    --------+-------
       1004 | lottu
       1005 | rax
       1006 | ak
       1007 | jack
    (4 rows)
    
    pl_db1=> select * from users;
     userid | name
    --------+-------
       1004 | lottu
       1005 | rax
       1006 | ak
       1007 | jack
    (4 rows)
    ```

    **说明：** 每个数据节点的数据都一样，说明数据复制成功。

6.  在代理节点查询时，只需要执行RUN ON ANY，即在任意一个数据节点读取数据即可，示例如下：

    ```
    postgres=> CREATE OR REPLACE FUNCTION get_user_name_2()
    postgres-> RETURNS TABLE(userid int, name text) AS $$
    postgres$>     CLUSTER 'cluster_srv1';
    postgres$>     RUN ON ANY ;
    postgres$> SELECT userid,name FROM users;
    postgres$> $$ LANGUAGE plproxy;
    CREATE FUNCTION
    
    postgres=> SELECT USERID,NAME FROM GET_USER_NAME_2();
     userid | name
    --------+-------
       1004 | lottu
       1005 | rax
       1006 | ak
       1007 | jack
    (4 rows)
    ```


## CONNECT模式测试

使用CONNECT模式时，代理节点可以直接跨实例访问，示例如下：

```
postgres=> CREATE OR REPLACE FUNCTION get_user_name_3()
postgres-> RETURNS TABLE(userid int, name text) AS $$
postgres$>     CONNECT 'dbname=pl_db0 host=100.81.137.72 port=56789';
postgres$> SELECT userid,name FROM users;
postgres$> $$ LANGUAGE plproxy;
CREATE FUNCTION

postgres=> SELECT USERID,NAME FROM GET_USER_NAME_3();
 userid | name
--------+-------
   1004 | lottu
   1005 | rax
   1006 | ak
   1007 | jack
(4 rows)
```

