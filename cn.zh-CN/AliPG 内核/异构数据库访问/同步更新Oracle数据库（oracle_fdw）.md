# 同步更新Oracle数据库（oracle\_fdw）

RDS PostgreSQL提供oracle\_fdw插件，可以连接到Oracle数据库，通过操作PostgreSQL表同步更新Oracle数据库中的表。

-   实例为RDS PostgreSQL 12（内核版本20200421及以上）。

    **说明：** 您可以执行`show rds_supported_extensions;`查看是否支持oracle\_fdw，不支持的话请升级内核版本。

-   Oracle Client版本为11.2及以上。
-   Oracle Server版本要求取决于Oracle Client版本。详情请参见[Oracle官方文档](https://oraclefact.wordpress.com/2018/04/05/client-server-interoperability-support-matrix-for-different-oracle-versions-doc-id-207303-1/)。

oracle\_fdw是PostgreSQL外部表插件，可以读取Oracle数据库的数据，也非常方便地实现PostgreSQL与Oracle数据同步。

更多详细信息请参见[oracle\_fdw](https://github.com/laurenz/oracle_fdw)。

## 注意事项

-   如果需要执行UPDATE和DELETE操作，需要在创建外部表时为主键列设置key参数，详情请参见[创建外部表](#step_amc_tf2_tpp)。
-   外部表定义的列数据类型必须是oracle\_fdw可以识别并可以转换的，oracle\_fdw插件对于数据类型的转换规则请参见[Data types](https://github.com/laurenz/oracle_fdw#data-types)。
-   WHERE子句和ORDER BY子句支持计算下推，即oracle\_fdw会将子句发送给Oracle进行计算。
-   JOIN操作支持计算下推，但是有以下注意事项：
    -   两个表必须被定义在相同的映射中。
    -   三个及以上的JOIN操作不支持下推。
    -   JOIN操作必须包含在SELECT操作中。
    -   没有JOIN条件的CROSS JOIN操作不支持下推。
    -   如果JOIN子句被下推，ORDER BY子句将不会被下推。
-   oracle\_fdw支持postgis插件，安装postgis插件后支持空间数据类型，包括：
    -   POINT
    -   LINE
    -   POLYGON
    -   MULTIPOINT
    -   MULTILINE
    -   MULTIPOLYGON

## 操作步骤

1.  新建oracle\_fdw插件。命令如下：

    ```
    CREATE EXTENSION oracle_fdw;
    ```

2.  创建Oracle数据库映射。有如下两种命令：

    -   ```
CREATE SERVER <SERVER名称>
FOREIGN DATA WRAPPER oracle_fdw
OPTIONS (dbserver '//<连接地址>:<连接端口>/<数据库名>');
```

        示例

        ```
        CREATE SERVER <SERVER名称>
        FOREIGN DATA WRAPPER oracle_fdw
        OPTIONS (dbserver '//127.0.0.1:5432/oradbname');
        ```

    -   ```
CREATE SERVER oradb
FOREIGN DATA WRAPPER oracle_fdw
OPTIONS (host '<连接地址>', port '<连接端口>', dbname '<数据库名>');
```

        示例

        ```
        CREATE SERVER oradb
        FOREIGN DATA WRAPPER oracle_fdw
        OPTIONS (host '127.0.0.1', port '5432', dbname 'oradbname');
        ```

3.  创建用户映射。命令如下：

    ```
    CREATE USER MAPPING
    FOR <PostgreSQL用户名> SERVER <映射名>
    OPTIONS (user '<Oracle数据库用户名>', password '<Oracle数据库用户密码>');
    ```

    **说明：** 如果不在PostgreSQL数据库中存储Oracle用户凭证，可以设置user为空字符串，然后提供必须的外部授权。

    示例

    ```
    CREATE USER MAPPING
    FOR pguser SERVER oradb
    OPTIONS (user 'orauser', password 'orapwd');
    ```

4.  创建Oracle的外部表。示例如下：

    ```
    CREATE FOREIGN TABLE oratab (
              id        integer OPTIONS (key 'true')  NOT NULL,
              text      character varying(30),
              floating  double precision  NOT NULL
           ) SERVER oradb OPTIONS (table 'ORATAB',
                                   schema 'ORAUSER',
                                   max_long '32767',
                                   readonly 'false',
                                   sample_percent, '100',
                                   prefetch, '200');
    ```

    **说明：** 外部表的结构需要和Oracle中的映射表结构保持一致。

    OPTIONS内的参数说明如下。

    |参数|说明|
    |--|--|
    |key|是否设置对应的列为主键，取值为true或false，默认值为false。如果要执行UPDATE和DELETE操作，必须将所有主键列设置为true。|
    |table|表名，一般是大写，必填参数。可以使用Oracle的SQL来定义table变量的值，例如：`OPTIONS (table '(SELECT col FROM tab WHERE val = ''string'')')`，此时不要使用schema参数。|
    |schema|一般是Oracle用户名，保持大写，用来访问不属于当前连接用户的表。|
    |max\_long|限制Oracle表中LONG、LONG RAW、XMLTYPE类型列的最大长度，取值范围是1~1073741823，默认值是32767。|
    |readonly|限制Oracle表为只读，不允许INSERT、UPDATE、DELETE操作。|
    |sample\_percent|设置随机选择Oracle表数据的比例，用于PostgreSQL表统计信息，取值范围是0.000001~100，默认值是100。|
    |prefetch|外表扫描时，PostgreSQL和Oracle数据表之间一次性传输的行数，取值范围是0~1024，默认值是200，0代表取消prefetch功能。|


完成以上步骤即可通过操作外表来实现对Oracle表的操作。支持DELETE、INSERT、UPDATE、SELECT等基本操作，支持导入外部表定义的操作，命令如下：

```
IMPORT FOREIGN SCHEMA <ora_schema_name>
FROM SERVER <server_name>
INTO <schema_name>
OPTIONS (case 'lower');
```

**说明：** case取值如下：

-   keep：表示保留Oracle上的对象名，通常是大写。
-   lower：表示转换所有的对象名为小写。
-   smart：表示只将对象名中都是大写字母的替换为小写。

## 卸载插件

卸载插件命令如下：

```
DROP EXTENSION oracle_fdw;
```

