# Use the pg\_hint\_plan plug-in to customize query plans

ApsaraDB RDS for PostgreSQL provides the pg\_hint\_plan plug-in. You can use the plug-in to add hints to SQL statements. This allows you to change the execution plans of SQL statements on an ApsaraDB RDS for PostgreSQL instance.

Your RDS instance runs one of the following PostgreSQL versions:

-   PostgreSQL 10
-   PostgreSQL 9.4

PostgreSQL uses a cost-based optimizer that works based on data statistics instead of static rules. The optimizer evaluates the cost of every possible execution plan for an SQL statement to your database system. This helps the optimizer select a final execution plan that has the lowest cost. However, the optimizer does not consider the possible internal relationships among data. Therefore, the final execution plan may not be perfect. You can use the pg\_hint\_plan plug-in to add hints to an SQL statement. These hints specify how you want to execute the SQL statement. This is another way to optimize the execution plans of SQL statements.

## Basic usage

A hint starts with a forward slash, an asterisk, and a plus sign \(`/*+`\) and ends with an asterisk and a forward slash \(`*/`\). A hint consists of a hint name followed by parameters that are enclosed in a pair of parentheses. The parameters are separated by space characters. For readability purposes, you can separate each hint with a line break.

Example:

In this example, the HashJoin hint specifies that the SeqScan method is used to scan the pgbench\_accounts table.

```
 /*+
    HashJoin(a b)
    >SeqScan(a)
  */
 EXPLAIN SELECT *
    FROM pgbench_branches b
    JOIN pgbench_accounts a ON b.bid = a.bid
   ORDER BY a.aid;
```

The following result is returned:

```
                                      QUERY PLAN
---------------------------------------------------------------------------------------
 Sort  (cost=31465.84..31715.84 rows=100000 width=197)
   Sort Key: a.aid
   ->  Hash Join  (cost=1.02..4016.02 rows=100000 width=197)
         Hash Cond: (a.bid = b.bid)
         ->  Seq Scan on pgbench_accounts a  (cost=0.00..2640.00 rows=100000 width=97)
         ->  Hash  (cost=1.01..1.01 rows=1 width=100)
               ->  Seq Scan on pgbench_branches b  (cost=0.00..1.01 rows=1 width=100)
(7 rows)
```

## Hint table

Hints can be used to optimize the execution plans of SQL statements. However, this is convenient only when SQL statements are editable. If SQL statements are not editable, you can place hints in a table named hint\_plan.hints. The table consists of the following columns.

**Note:** By default, the user who creates the pg\_hint\_plan plug-in has the permissions on the hint table. The hints in the hint table take precedence over the hints that you add by using the pg\_hint\_plan plug-in.

|Column|Description|
|------|-----------|
|id|The ID of the hint. The ID is unique and automatically generated.|
|norm\_query\_string|The pattern that matches the SQL statement to which you want to add the hint. The constants in the SQL statement must be replaced by wildcards \(`?`\). Space characters are crucial parts of the pattern.|
|application\_name|The name of the application to which the hint is applied. If this parameter is left empty, the hint is applied to all applications.|
|hints|The comment that contains the hint. You do not need to include comment marks.|

Example:

```
INSERT INTO hint_plan.hints(norm_query_string, application_name, hints)
    VALUES (
        'EXPLAIN (COSTS false) SELECT * FROM t1 WHERE t1.id = ? ;',
        '',
        'SeqScan(t1)'
    );
INSERT 0 1
postgres=# UPDATE hint_plan.hints
postgres-#    SET hints = 'IndexScan(t1)'
postgres-#  WHERE id = 1;
UPDATE 1
postgres=# DELETE FROM hint_plan.hints
postgres-#  WHERE id = 1;
DELETE 1
```

## Hint types

Hints come in the following six types based on how they affect execution plans:

-   Hints for scan methods

    This type of hint specifies the method that is used to scan the specified table. If the specified table has an alias, the pg\_hint\_plan plug-in identifies the table based on the alias. Supported scan methods include `SeqScan`, `IndexScan`, and `NoSeqScan`.

    The hints for scan methods are valid on ordinary tables, inherited tables, unlogged tables, temporary tables, and system tables. However, the hints for scan methods are invalid on external tables, table functions, statements in which the values of constants are specified, universal expressions, views, and subqueries.

    Example:

    ```
    /*+
        SeqScan(t1)
        IndexScan(t2 t2_pkey)
     */
    SELECT * FROM table1 t1 JOIN table table2 t2 ON (t1.key = t2.key);
    ```

-   Hints for join methods

    This type of hint specifies the method that is used to join the specified tables.

    The hints for join methods are valid on ordinary tables, inherited tables, unlogged tables, temporary tables, external tables, system tables, table functions, statements in which the values of constants are specified, and universal expressions. However, the hints for join methods are invalid on views and subqueries.

-   Hints for join order

    This type of hint specifies the order in which two or more tables are joined. You can use one of the following methods to specify a hint for join order:

    -   Specify the order in which you want to join the specified tables, without restricting the direction at each join level.
    -   Specify the order in which you want to join the specified tables, as well as the direction at each join level.
    Example:

    ```
    /*+
        NestLoop(t1 t2)
        MergeJoin(t1 t2 t3)
        Leading(t1 t2 t3)
     */
    SELECT * FROM table1 t1
        JOIN table table2 t2 ON (t1.key = t2.key)
        JOIN table table3 t3 ON (t2.key = t3.key);
    ```

-   Hints for row number correction

    This type of hint corrects row number errors that are caused by the optimizer.

    Examples:

    ```
    /*+ Rows(a b #10) */ SELECT... ;     //Sets the row number to 10.
    /*+ Rows(a b +10) */ SELECT... ;     //Increases the row number by 10.
    /*+ Rows(a b -10) */ SELECT... ;     //Decreases the row number by 10.
    /*+ Rows(a b *10) */ SELECT... ;     //Increases the row number by 10 times.
    ```

-   Hints for parallel execution

    This type of hint specifies the plan that is used to execute SQL statements in parallel.

    The hints for parallel execution are valid on ordinary tables, inherited tables, unlogged tables, and system tables. However, the hints for parallel execution are invalid on external tables, clauses in which the values of constants are specified, universal expressions, views, and subqueries. You can specify the internal tables of a view based on their real names or aliases.

    The following examples show how an SQL statement is executed in a different way on each table:

    -   Example 1:

        ```
        explain /*+ Parallel(c1 3 hard) Parallel(c2 5 hard) */
               SELECT c2.a FROM c1 JOIN c2 ON (c1.a = c2.a);
        ```

        The following result is returned:

        ```
                                          QUERY PLAN                                   
        -------------------------------------------------------------------------------
         Hash Join  (cost=2.86..11406.38 rows=101 width=4)
           Hash Cond: (c1.a = c2.a)
           ->  Gather  (cost=0.00..7652.13 rows=1000101 width=4)
                 Workers Planned: 3
                 ->  Parallel Seq Scan on c1  (cost=0.00..7652.13 rows=322613 width=4)
           ->  Hash  (cost=1.59..1.59 rows=101 width=4)
                 ->  Gather  (cost=0.00..1.59 rows=101 width=4)
                       Workers Planned: 5
                       ->  Parallel Seq Scan on c2  (cost=0.00..1.59 rows=59 width=4)
        ```

    -   Example 2:

        ```
        EXPLAIN /*+ Parallel(tl 5 hard) */ SELECT sum(a) FROM tl;
        ```

        The following result is returned:

        ```
                                            QUERY PLAN                                  
        -----------------------------------------------------------------------------------
         Finalize Aggregate  (cost=693.02..693.03 rows=1 width=8)
           ->  Gather  (cost=693.00..693.01 rows=5 width=8)
                 Workers Planned: 5
                 ->  Partial Aggregate  (cost=693.00..693.01 rows=1 width=8)
                       ->  Parallel Seq Scan on tl  (cost=0.00..643.00 rows=20000 width=4)
        ```

-   Hints for GUC parameter setting

    This type of hint temporarily changes the value of a GUC parameter. The values of GUC parameters in the execution plan help you achieve the expected effect. However, this does not apply if the specified hint conflicts with the execution plans of other SQL statements. If you set a GUC parameter more than once, the latest value takes effect.

    Example:

    ```
    /*+ Set(random_page_cost 2.0) */
    SELECT * FROM table1 t1 WHERE key = 'value';
    ```


The following table describes all of the supported hints.

|Type|Hint|Description|
|----|----|-----------|
|Hints for scan methods|SeqScan\(table\)|Specifies a sequence scan.|
|TidScan\(table\)|Specifies a TID scan.|
|IndexScan\(table\[ index...\]\)|Specifies an index scan. You can specify an index.|
|IndexOnlyScan\(table\[ index...\]\)|Specifies an index-only scan. You can specify an index.|
|BitmapScan\(table\[ index...\]\)|Specifies a bitmap scan.|
|NoSeqScan\(table\)|Prohibits a sequence scan.|
|NoTidScan\(table\)|Prohibits a TID scan.|
|NoIndexScan\(table\)|Prohibits an index scan.|
|NoIndexOnlyScan\(table\)|Prohibits an index scan. Only tables are scanned.|
|NoBitmapScan\(table\)|Prohibits a bitmap scan.|
|Hints for join methods|NestLoop\(table table\[ table...\]\)|Specifies a nested loop join.|
|HashJoin\(table table\[ table...\]\)|Specifies a hash join.|
|MergeJoin\(table table\[ table...\]\)|Specifies a merge join.|
|NoNestLoop\(table table\[ table...\]\)|Prohibits a nested loop join.|
|NoHashJoin\(table table\[ table...\]\)|Prohibits a hash join.|
|NoMergeJoin\(table table\[ table...\]\)|Prohibits a merge join.|
|Hints for join order|Leading\(table table\[ table...\]\)|Specifies the join order.|
|Leading\(<join pair\>\)|Specifies the join order and direction.|
|Hints for row number correction|Rows\(table table\[ table...\] correction\)|Corrects the row number of the join result that is obtained from the specified tables. The following operators are supported: `#<n>`, `+ <n>`, `-<n>`, and `* <n>`. The `<n>` operator is supported by the strtod function.|
|Hints for parallel execution|Parallel\(table <\# of workers\> \[soft\|hard\]\)|Specifies or prohibits the parallel execution of the specified tables. The `<worker#>` parameter specifies the number of working programs that are required. The value 0 specifies to prohibit parallel execution.If the third parameter is set to soft, only the value of the max\_parallel\_workers\_per\_gather parameter is changed and the other parameters are specified by the optimizer. If the third parameter is set to hard, the values of all related parameters are changed. The third parameter is set to soft by default. |
|Hints for GUC parameter setting|Set\(GUC-param value\)|Specifies the value of a GUC parameter when the optimizer runs.|

For more information, visit the [official PostgreSQL website](https://postgrespro.com/docs/enterprise/10/pg-hint-plan.html).

