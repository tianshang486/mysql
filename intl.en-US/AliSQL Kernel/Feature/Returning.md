# Returning

This topic describes the Returning feature of AliSQL. This feature enables data manipulation language \(DML\) statements to return result sets and provides the DBMS\_TRANS package for you to track the execution of DML statements.

The execution results of MySQL statements are divided into three types: result sets, OK packets, and ERR packets. An OK or ERR packet contains attributes such as the number of affected and the number of scanned records. However, the execution of a DML statement \(INSERT, UPDATE, or DELETE\) is often followed by the execution of the SELECT statement to query current records. In such cases, the Returning feature enables the server to respond to the client only once by combining the execution results of the two statements into a result set.

## Prerequisites

Your RDS instance is running MySQL 8.0.

## Syntax

```
DBMS_TRANS.returning(<Field_list>,<Statement>);
```

The following table describes the parameters that you need to configure.

|Parameter|Description|
|---------|-----------|
|Field\_list|The fields to return. If you enter more than one field, separate them with commas \(,\). Native fields and wildcards \(\*\) in the specified table are supported. However, operations such as calculation and aggregation are not supported.|
|Statement|The DML statement to execute. Only the INSERT, UPDATE, and DELETE statements are supported.|

## Precautions

`dbms_trans.returning()` is not a transactional statement. It inherits the context of the specified transaction based on the DML statement that you want to execute. To terminate the transaction, you must explicitly commit it or roll it back.

## INSERT Returning

The server returns the records that were inserted into the specified table by using the INSERT statement.

Example:

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

**Note:**

-   If you do not specify the Field\_list parameter, the server returns an OK or ERR packet.

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

-   The Returning feature only supports statements that are similar to `INSERT VALUES`. It does not support statements such as `CREATE AS` and `INSERT SELECT`.

    ```
    mysql> call dbms_trans.returning("", "insert into t select * from t");
    ERROR 7527 (HY000): Statement didn't support RETURNING clause
    ```


## UPDATE Returning

The server returns the records that were updated in the specified table by the using UPDATE statement.

Example:

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

**Note:** The Returning feature does not allow the UPDATE statement to be executed on more than one table.

## DELETE Returning

The server returns the records that were deleted from the specified table by using the DELETE statement.

Example:

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

