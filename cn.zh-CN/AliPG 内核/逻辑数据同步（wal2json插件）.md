# 逻辑数据同步（wal2json插件）

RDS PostgreSQL提供wal2json插件，可以将逻辑日志文件输出为JSON格式供您查看。

-   实例为RDS PostgreSQL 11、12。
-   已设置实例参数wal\_level = logical。详情请参见[设置实例参数](/cn.zh-CN/RDS PostgreSQL 数据库/实例/设置实例参数.md)。

wal2json是逻辑解码插件，使用该插件可以访问由INSERT和UPDATE生成的元组，解析WAL中的内容。

wal2json插件会在每个事务中生成一个JSON对象。JSON对象中提供了所有新/旧元组，额外选项还可以包括事务时间戳、限定架构、数据类型、事务ID等属性。详情请参见[通过SQL获取JSON对象](#section_xdd_glx_5vf)。

## 通过SQL获取JSON对象

1.  [通过DMS登录RDS数据库](/cn.zh-CN/RDS PostgreSQL 数据库/数据库连接/通过DMS登录RDS数据库.md)。

2.  执行如下命令建表及初始化插件。

    ```
    CREATE TABLE table2_with_pk (a SERIAL, b VARCHAR(30), c TIMESTAMP NOT NULL, PRIMARY KEY(a, c));
    CREATE TABLE table2_without_pk (a SERIAL, b NUMERIC(5,2), c TEXT);
    
    SELECT 'init' FROM pg_create_logical_replication_slot('test_slot', 'wal2json');
    ```

3.  执行如下命令变更数据。

    ```
    BEGIN;
    INSERT INTO table2_with_pk (b, c) VALUES('Backup and Restore', now());
    INSERT INTO table2_with_pk (b, c) VALUES('Tuning', now());
    INSERT INTO table2_with_pk (b, c) VALUES('Replication', now());
    DELETE FROM table2_with_pk WHERE a < 3;
    INSERT INTO table2_without_pk (b, c) VALUES(2.34, 'Tapir');
    UPDATE table2_without_pk SET c = 'Anta' WHERE c = 'Tapir';
    COMMIT;
    ```

4.  执行如下命令输出JSON格式的日志信息。

    ```
    SELECT data FROM pg_logical_slot_get_changes('test_slot', NULL, NULL, 'pretty-print', '1');
    ```

    ![解析日志](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3919259951/p77370.png)

    **说明：** 如果需要停止输出并释放资源，请执行如下命令：

    ```
    SELECT 'stop' FROM pg_drop_replication_slot('test_slot');
    ```


