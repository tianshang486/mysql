# Use the pg\_concurrency\_control plug-in

ApsaraDB RDS for PostgreSQL provides a pg\_concurrency\_control plug-in to control concurrency of SQL statements.

Your RDS instance runs PostgreSQL 10.

## Parameters

**Note:** The following parameters cannot be modified in the ApsaraDB RDS console. You can [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to modify them.

|Parameter|Default value|Description|
|---------|-------------|-----------|
|pg\_concurrency\_control.query\_concurrency|0|Sets the maximum number of concurrent jobs in SELECT SQL statements. Valid values: 0 to 1024. Default value: 0. The default value indicates that concurrency control is disabled for SELECT SQL statements.|
|pg\_concurrency\_control.bigquery\_concurrency|0|Sets the maximum number of concurrent jobs in slow queries. Valid values: 0 to 1024. Default value: 0. The default value indicates that concurrency control is disabled for slow queries.You can specify a statement as a slow query by using `hint "/*+bigsql*/"`. Example:

```
/*+bigsql*/select * from test;
```

The `select * from test;` statement is a slow query. |
|pg\_concurrency\_control.transaction\_concurrency|0|Sets the maximum number of concurrent jobs for transaction blocks. Valid values: 0 to 1024. Default value: 0. The default value indicates that concurrency control is disabled for transaction blocks.|
|pg\_concurrency\_control.autocommit\_concurrency|0|Sets the maximum number of concurrent jobs in DML SQL statements. Valid values: 0 to 1024. Default value: 0. The default value indicates that concurrency control is disabled for DML SQL statements.|
|pg\_concurrency\_control.control\_timeout|1s|Sets the maximum time to wait for a SELECT SQL statement, DML SQL statement, and transaction block. The minimum value is 30 ms, and the maximum value is 3s.|
|pg\_concurrency\_control.bigsql\_control\_timeout|1s|Sets the maximum time to wait for a slow query. The minimum value is 30 ms, and the maximum value is 3s.|
|pg\_concurrency\_control.timeout\_action|TCC\_break|Sets the action upon a timeout for a SELECT SQL statement, DML SQL statement, and transaction block. Valid values:-   TCC\_break: skips the statement in waiting and execute the statement that follows.
-   TCC\_rollback: reports an error and rolls back the transaction.
-   TCC\_wait: resets the timestamp after a timeout and continues to wait. |
|pg\_concurrency\_control.bigsql\_timeout\_action|TCC\_wait|Sets the action upon a timeout for slow queries. Valid values:-   TCC\_break: skips the statement in waiting and execute the statement that follows.
-   TCC\_rollback: reports an error and rolls back the transaction.
-   TCC\_wait: resets the timestamp after a timeout and continues to wait. |

## Procedure

1.  Run the following command to create the plug-in:

    ```
    create extension pg_concurrency_control;
    ```

2.  Set the number of concurrent jobs to a value that is greater than 0 to enable concurrency control in the plug-in.

    For example, set the pg\_concurrency\_control.query\_concurrency parameter to 10 to enable concurrency control for SELECT SQL statements. The methods to enable concurrency control for other types of statements are similar.

    **Note:** The parameters cannot be modified in the ApsaraDB RDS console. You can [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to modify them.


## Example

Perform the following operations to enable concurrency control for custom SQL statements:

1.  Run the following command to view information of the statement queue:

    ```
    select * from pg_concurrency_control_status();
    ```

    The system displays information similar to the following output:

    ```
     autocommit_count | bigquery_count | query_count | transaction_count 
    ------------------+----------------+-------------+-------------------
                    0 |              0 |           0 |                 0 
    (1 row)
    ```

2.  Set the pg\_concurrency\_control.query\_concurrency parameter to a value that is greater than 0, for example, 10.

3.  Execute a slow query.

    ```
    /*+ bigsql */ select pg_sleep(10);
    ```

4.  Run the following command to view information of the statement queue again:

    ```
    select * from pg_concurrency_control_status();
    ```

    The system displays information similar to the following output:

    ```
     autocommit_count | bigquery_count | query_count | transaction_count 
    ------------------+----------------+-------------+-------------------
                    0 |              1 |           0 |                 0 
    (1 row)
    ```

    **Note:** After the slow query is complete, the queue information is automatically cleared.


