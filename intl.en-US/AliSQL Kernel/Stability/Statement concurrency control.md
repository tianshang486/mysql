# Statement concurrency control

Alibaba Cloud provides the concurrency control \(CCL\) feature to ensure the stability of ApsaraDB RDS MySQL instances in case of unexpected request traffic, resource-consuming statements, and SQL access model changes. The DBMS\_CCL package can be installed to use the CCL feature.

## Prerequisites

The RDS instance version is one of the following:

-   MySQL 8.0
-   MySQL 5.7

## Precautions

-   CCL operations only affect the current instance because no binlogs are generated. For example, CCL operations performed on the primary instance are not synchronized to the secondary instance, read-only instance, or disaster recovery instance.
-   CCL includes a timeout mechanism which resolves transaction deadlocks caused by DML statements. The waiting threads also respond to the transaction timeout and kill threads to prevent deadlocks.

## Feature design

The CCL provides features based on the following dimensions:

-   SQL command

    The types of SQL statements, such as SELECT, UPDATE, INSERT, and DELETE.

-   Object

    The objects managed by SQL statements, such as tables and views.

-   keywords

    The keywords of SQL statements.


## Create a CCL table

AliSQL uses a system table named concurrency\_control to store CCL rules. The instance system automatically creates the table when the system is started. You can refer to the following statements that create the concurrency\_control table.

```
CREATE TABLE `concurrency_control` (
  `Id` bigint(20) NOT NULL AUTO_INCREMENT,
  `Type` enum('SELECT','UPDATE','INSERT','DELETE') NOT NULL DEFAULT 'SELECT',
  `Schema_name` varchar(64) COLLATE utf8_bin DEFAULT NULL,
  `Table_name` varchar(64) COLLATE utf8_bin DEFAULT NULL,
  `Concurrency_count` bigint(20) DEFAULT NULL,
  `Keywords` text COLLATE utf8_bin,
  `State` enum('N','Y') NOT NULL DEFAULT 'Y',
  `Ordered` enum('N','Y') NOT NULL DEFAULT 'N',
  PRIMARY KEY (`Id`)
) /*! 50100 TABLESPACE `mysql` */ ENGINE=InnoDB 
DEFAULT CHARSET=utf8 COLLATE=utf8_bin
STATS_PERSISTENT=0 COMMENT='Concurrency control'
```

|Parameter|Description|
|---------|-----------|
|Id|The ID of the CCL rule.|
|Type|The type of the SQL statement.|
|Schema\_name|The name of the database.|
|Table\_name|The name of the table in the database.|
|Concurrency\_count|The number of concurrent threads.|
|Keywords|The keyword. Multiple keywords are separated by semicolons \(;\).|
|State|Specifies whether to enable the CCL rule.|
|Ordered|Specifies whether to match multiple keywords in sequence.|

## Manage CCL rules

AliSQL provides four management interfaces in the DBMS\_CCL package. They are described as follows:

-   add\_ccl\_rule

    Use the following statement to create a rule.

    ```
    dbms_ccl.add_ccl_rule('<Type>','<Schema_name>','<Table_name>',<Concurrency_count>,'<Keywords>');
    ```

    Example:

    The number of concurrent threads of the SELECT statement is 10.

    ```
    mysql> call dbms_ccl.add_ccl_rule('SELECT', '', '', 10, '');
    ```

    The number of concurrent threads of the SELECT statement is 20, and the keyword of the statement is key1.

    ```
    mysql> call dbms_ccl.add_ccl_rule('SELECT', '', '', 20, 'key1');
    ```

    The number of concurrent threads of the SELECT statement in the test.t table is 20.

    ```
    mysql> call dbms_ccl.add_ccl_rule('SELECT', 'test', 't', 20, '');
    ```

    **Note:** The rule with a larger Id has higher priority.

-   del\_ccl\_rule

    Use the following statement to delete a rule.

    ```
    dbms_ccl.del_ccl_rule(<Id>);
    ```

    Example:

    Delete the CCL rule whose ID is 15.

    ```
    mysql> call dbms_ccl.del_ccl_rule(15);
    ```

    **Note:** If the CCL rule that you want to delete does not exist, the system displays an error. You can execute the `SHOW WARNINGS;` statement to view the error message.

    ```
    mysql> call dbms_ccl.del_ccl_rule(100);
      Query OK, 0 rows affected, 2 warnings (0.00 sec)
    
    mysql> show warnings;
    +---------+------+----------------------------------------------------+
    | Level   | Code | Message                                            |
    +---------+------+----------------------------------------------------+
    | Warning | 7514 | Concurrency control rule 100 is not found in table |
    | Warning | 7514 | Concurrency control rule 100 is not found in cache |
    +---------+------+----------------------------------------------------+
    ```

-   show\_ccl\_rule

    Use the following statement to view the enabled rules in the memory.

    ```
    dbms_ccl.show_ccl_rule();
    ```

    Example:

    ```
    ​mysql> call dbms_ccl.show_ccl_rule();
    +------+--------+--------+-------+-------+-------+-------------------+---------+---------+----------+----------+
    | ID   | TYPE   | SCHEMA | TABLE | STATE | ORDER | CONCURRENCY_COUNT | MATCHED | RUNNING | WAITTING | KEYWORDS |
    +------+--------+--------+-------+-------+-------+-------------------+---------+---------+----------+----------+
    |   17 | SELECT | test   | t     | Y     | N     |                30 |       0 |       0 |        0 |          |
    |   16 | SELECT |        |       | Y     | N     |                20 |       0 |       0 |        0 | key1     |
    |   18 | SELECT |        |       | Y     | N     |                10 |       0 |       0 |        0 |          |
    +------+--------+--------+-------+-------+-------+-------------------+---------+---------+----------+----------+​
    ```

    The following table describes the MATCHED, RUNNING, and WAITTING parameters.

    |Parameter|Description|
    |---------|-----------|
    |MATCHED|The number of times the rule is matched.|
    |RUNNING|The number of concurrent threads under the rule.|
    |WAITTING|The number of threads to be run under the rule.|

-   flush\_ccl\_rule

    If you modify the rules in the concurrency\_control table, you must execute the following statement to validate the rules again.

    ```
    dbms_ccl.flush_ccl_rule();
    ```

    Example:

    ```
    ​mysql> update mysql.concurrency_control set CONCURRENCY_COUNT = 15 where Id = 18;
    Query OK, 1 row affected (0.00 sec)
    Rows matched: 1  Changed: 1  Warnings: 0
    
    mysql> call dbms_ccl.flush_ccl_rule();
    Query OK, 0 rows affected (0.00 sec)​
    ```


## Feature test

-   Test rules

    Execute the following statements to create the rules for three dimensions.

    ```
    call dbms_ccl.add_ccl_rule('SELECT', 'test', 'sbtest1', 3, '');  // The SELECT statement manages the sbtest1 table and the number of concurrent threads is 3.
    call dbms_ccl.add_ccl_rule('SELECT', '', '', 2, 'sbtest2');       // The keyword of the SELECT statement is sbtest2 and the number of concurrent threads is 2.
     call dbms_ccl.add_ccl_rule('SELECT', '', '', 2, '');            // The number of concurrent threads of the SELECT statement is 2.
    ```

-   Test scenarios

    Use sysbench to test in the following scenarios:

    -   64 threads
    -   4 tables
    -   select.lua
-   Test results

    Execute the following statement to view the number of concurrent threads under the rules.

    ```
    ​mysql> call dbms_ccl.show_ccl_rule();
    +------+--------+--------+---------+-------+-------+-------------------+---------+---------+----------+----------+
    | ID   | TYPE   | SCHEMA | TABLE   | STATE | ORDER | CONCURRENCY_COUNT | MATCHED | RUNNING | WAITTING | KEYWORDS |
    +------+--------+--------+---------+-------+-------+-------------------+---------+---------+----------+----------+
    |   20 | SELECT | test   | sbtest1 | Y     | N     |                 3 |     389 |       3 |        9 |          |
    |   21 | SELECT |        |         | Y     | N     |                 2 |     375 |       2 |       14 | sbtest2  |
    |   22 | SELECT |        |         | Y     | N     |                 2 |     519 |       2 |       34 |          |
    +------+--------+--------+---------+-------+-------+-------------------+---------+---------+----------+----------+
    3 rows in set (0.00 sec)​
    ```

    The numbers displayed in the **RUNNING** column are the same as the numbers specified when you create the rules.


