# 查询其他类型数据库（tds\_fdw）

您可以使用tds\_fdw插件查询其他类型数据库的数据。

实例版本如下：

-   PostgreSQL 12（内核小版本20200421及以上）
-   PostgreSQL 11（内核小版本20200402及以上）

**说明：** 您可以在**基本信息**页面的**配置信息**区域查看是否有**升级内核小版本**按钮。如果有按钮，您可以单击按钮查看当前版本；如果没有按钮，表示已经是最新版。详情请参见[升级内核小版本](/intl.zh-CN/RDS PostgreSQL 数据库/实例/升级内核小版本.md)。

![pgsql升级内核](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/4919259951/p101917.png)

tds\_fdw是PostgreSQL外部数据包装器，可以连接到使用Tabular Data Stream（TDS）协议的数据库，例如Sybase数据库和Microsoft SQL server。

详细说明请参见[postgres\_fdw](http://www.postgres.cn/docs/11/postgres-fdw.html)。

## 创建插件

连接实例后创建tds\_fdw插件，命令如下：

```
create extension tds_fdw;
```

## 使用插件

1.  创建服务器，示例如下：

    ```
    CREATE SERVER mssql_svr
      FOREIGN DATA WRAPPER tds_fdw
      OPTIONS (servername '127.0.0.1', port '1433', database 'tds_fdw_test', tds_version '7.1');
    ```

2.  创建外部表。您可以通过多种方式创建外部表：

    -   使用table\_name定义创建外部表，示例如下：

        ```
        CREATE FOREIGN TABLE mssql_table (
         id integer,
         data varchar)
         SERVER mssql_svr
         OPTIONS (table_name 'dbo.mytable', row_estimate_method 'showplan_all');
        ```

    -   使用schema\_name和table\_name定义创建外部表，示例如下：

        ```
        CREATE FOREIGN TABLE mssql_table (
         id integer,
         data varchar)
         SERVER mssql_svr
         OPTIONS (schema_name 'dbo', table_name 'mytable', row_estimate_method 'showplan_all');
        ```

    -   使用query定义创建外部表，示例如下：

        ```
        CREATE FOREIGN TABLE mssql_table (
         id integer,
         data varchar)
         SERVER mssql_svr
         OPTIONS (query 'SELECT * FROM dbo.mytable', row_estimate_method 'showplan_all');
        ```

    -   使用远程列名创建外部表，示例如下：

        ```
        CREATE FOREIGN TABLE mssql_table (
         id integer,
         col2 varchar OPTIONS (column_name 'data'))
         SERVER mssql_svr
         OPTIONS (schema_name 'dbo', table_name 'mytable', row_estimate_method 'showplan_all');
        ```

3.  创建用户映射，示例如下：

    ```
    CREATE USER MAPPING FOR postgres
      SERVER mssql_svr 
      OPTIONS (username 'sa', password '123456');
    ```

4.  导入外部模式，示例如下：

    ```
    IMPORT FOREIGN SCHEMA dbo
      EXCEPT (mssql_table)
      FROM SERVER mssql_svr
      INTO public
      OPTIONS (import_default 'true');
    ```


