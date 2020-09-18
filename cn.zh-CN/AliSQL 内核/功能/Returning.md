# Returning

AliSQL提供returning功能，支持DML语句返回Resultset，同时提供了工具包（DBMS\_TRANS）便于您快捷使用。

MySQL的语句执行结果报文通常分为三类：Resultset、OK和ERR。针对DML语句返回的是OK或ERR报文，其中包括影响记录、扫描记录等属性。但在很多业务场景下，执行INSERT、UPDATE、DELETE这样的DML语句后，都会跟随SELECT查询当前记录内容，以进行接下来的业务处理，为了减少一次客户端和服务器的交互，returning功能支持使用DML语句后返回Resultset。

## 前提条件

实例版本为RDS MySQL 8.0。

## 语法

```
DBMS_TRANS.returning(<Field_list>,<Statement>);
```

参数说明如下。

|参数|说明|
|--|--|
|Field\_list|期望的返回字段，多个字段以英文逗号（,）进行分隔，支持表中原生的字段或星号（\*），不支持进行计算或者聚合等操作。|
|Statement|执行的DML语句，支持INSERT、UPDATE、DELETE。|

## 注意事项

`dbms_trans.returning()`不是事务性语句，会根据DML语句来继承事务上下文，结束事务需要显式的提交或者回滚。

## INSERT Returning

针对INSERT语句，returning返回插入到表中的记录内容。

示例：

```
CREATE TABLE `t` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `col1` int(11) NOT NULL DEFAULT '1',
  `col2` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB;

mysql> call dbms_trans.returning("*", "insert into t(id) values(NULL),(NULL)");
+----+------+---------------------+
| id | col1 | col2                |
+----+------+---------------------+
|  1 |    1 | 2019-09-03 10:39:05 |
|  2 |    1 | 2019-09-03 10:39:05 |
+----+------+---------------------+
2 rows in set (0.01 sec)
```

**说明：**

-   如果没有填入Field\_list，returning将返回OK或ERR报文。

    ```
    mysql> call dbms_trans.returning("", "insert into t(id) values(NULL),(NULL)");
    Query OK, 2 rows affected (0.01 sec)
    Records: 2  Duplicates: 0  Warnings: 0
    
    mysql> select * from t;
    +----+------+---------------------+
    | id | col1 | col2                |
    +----+------+---------------------+
    |  1 |    1 | 2019-09-03 10:40:55 |
    |  2 |    1 | 2019-09-03 10:40:55 |
    |  3 |    1 | 2019-09-03 10:41:06 |
    |  4 |    1 | 2019-09-03 10:41:06 |
    +----+------+---------------------+
    4 rows in set (0.00 sec)
    ```

-   INSERT Returning只支持`insert values`形式的语法，类似`create as`、`insert select`形式的则不支持。

    ```
    mysql> call dbms_trans.returning("", "insert into t select * from t");
    ERROR 7527 (HY000): Statement didn't support RETURNING clause
    ```


## UPDATE Returning

针对UPDATE语句，returning返回更新后的记录。

示例：

```
mysql> call dbms_trans.returning("id, col1, col2", "update t set col1 = 2 where id >2");
+----+------+---------------------+
| id | col1 | col2                |
+----+------+---------------------+
|  3 |    2 | 2019-09-03 10:41:06 |
|  4 |    2 | 2019-09-03 10:41:06 |
+----+------+---------------------+
2 rows in set (0.01 sec)
```

**说明：** UPDATE Returning不支持多表UPDATE语句。

## DELETE Returning

针对DELETE语句，returning返回被删除的记录。

示例：

```
mysql> call dbms_trans.returning("id, col1, col2", "delete from t where id < 3");
+----+------+---------------------+
| id | col1 | col2                |
+----+------+---------------------+
|  1 |    1 | 2019-09-03 10:40:55 |
|  2 |    1 | 2019-09-03 10:40:55 |
+----+------+---------------------+
2 rows in set (0.00 sec)
```

