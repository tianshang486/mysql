# Use the sql\_firewall plug-in

The sql\_firewall plug-in is a database-level firewall that prevents against SQL injection. It learns defined SQL rules and stores the rules in your ApsaraDB RDS for PostgreSQL instance as a whitelist. User operations that do not comply with the rules are forbidden.

Your RDS instance runs one of the following RDS editions:

-   PostgreSQL 12
-   PostgreSQL 11
-   PostgreSQL 10

## Learning, permissive, and enforcing modes

![流程图](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5402873061/p162105.png)

The sql\_firewall plug-in supports the following modes:

-   Learning: The plug-in records common SQL statements that are executed and adds them to a whitelist.
-   Permissive: The plug-in checks SQL statements that will be executed. If the SQL statements are not in the whitelist, the plug-in executes the SQL statements but generates alerts.
-   Enforcing: The plug-in checks SQL statements that will be executed. If the SQL statements are not in the whitelist, the plug-in does not execute the SQL statements and returns errors.

## Procedure

1.  Enable the learning mode of the sql\_firewall plug-in. Wait for a specific period of time to ensure that the plug-in learns more SQL statements.
2.  Switch the sql\_firewall plug-in to the permissive mode. In this mode, the plug-in generates alerts for SQL statements that are not in the whitelist. You can check whether these SQL statements are high-risky statements based on your business requirements. If these statements are not high-risky statements, switch to the learning mode and add these SQL statements to the whitelist.
3.  Switch the sql\_firewall plug-in to the enforcing mode. In this mode, the plug-in does not execute SQL statements that are not in the whitelist.

## Operations

-   Create the plug-in

    ```
    create extension sql_firewall;
    ```

-   Delete the plug-in

    ```
    drop extension sql_firewall;
    ```

-   Switch the mode

    In the ApsaraDB for RDS console, find the **sql\_firewall.firewall** parameter. Modify the parameter value and restart your RDS instance. For more information, see [Reconfigure parameters for an RDS PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Instance/Reconfigure parameters for an RDS PostgreSQL instance.md).

    Valid values for the **sql\_firewall.firewall** parameter:

    -   disable: disables the sql\_firewall plug-in.
    -   learning: enables the learning mode.
    -   permissive: enables the permissive mode.
    -   enforcing: enables the enforcing mode.
-   Functionality functions
    -   sql\_firewall\_reset\(\)

        This function clears the whitelist. You can call this function only if you are authorized with the rds\_superuser role and the enforcing mode is disabled.

    -   sql\_firewall\_stat\_reset\(\)

        This function deletes statistics. You can call this function only if you are authorized with the rds\_superuser role and the enforcing mode is disabled.

-   View functions
    -   sql\_firewall.sql\_firewall\_statements

        This function returns all SQL statements in the whitelist of your RDS instance. This function also returns the number of times that each SQL statement is executed.

        ```
        postgres=# select * from sql_firewall.sql_firewall_statements;
             userid |  queryid   |              query              | calls
            --------+------------+---------------------------------+-------
                 10 | 3294787656 | select * from k1 where uid = ? ; |     4
            (1 row)
        ```

    -   sql\_firewall.sql\_firewall\_stat

        This function returns the number of alerts that are generated in permissive mode and the number of errors that are generated in enforcing mode. The first number is measured by sql\_warning, and the second number is measured by sql\_error.

        ```
        postgres=# select * from sql_firewall.sql_firewall_stat;
             sql_warning | sql_error
            -------------+-----------
                       2 |         1
            (1 row)
        ```


## Examples

```
-- Permissive mode

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

-- Enforcing mode

    postgres=# select * from k1 where uid = 3;
     uid |   uname
    -----+-----------
       3 | Goo Ha-ra
    (1 row)

    postgres=# select * from k1 where uid = 3 or 1 = 1;
    ERROR:  Prohibited SQL statement
    postgres=#
```

