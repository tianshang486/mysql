# 定制执行计划（pg\_hint\_plan）

RDS PostgreSQL提供pg\_hint\_plan插件，可以通过特殊的注释语句提示，使PostgreSQL改变其既定的执行计划。

RDS PostgreSQL版本如下：

-   PostgreSQL 10
-   PostgreSQL 9.4

PostgreSQL使用基于代价的优化器，优化路线使用统计数据而非固定的规则。对于一条SQL语句，优化器会去评估每一种可能的代价并最终选择代价最低的去执行，优化器会尽力去选择最好的执行计划，但是由于其并不了解数据中可能存在的一些内在连接关系，这些执行计划可能并不完美。使用pg\_hint\_plan插件以特殊的注释形式来提示SQL语句应该如何执行，可以优化执行计划。

## 注释提示

pg\_hint\_plan的注释以`/*+`开头，以`*/`结束。提示语句包括提示名和接下来括号包裹的参数，以空格作为分界。为了可读性，每一个提示语句都可以重新换行。

示例

HashJoin作为连接方法，并且使用序列扫描SeqScan来扫描表pgbench\_accounts。

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

返回如下结果：

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

## 提示表

虽然可以使用注释提示的方式对SQL语句进行提示，但是当SQL语句不可编辑时，这种提示方式就很不方便。对于这种情况，可以将提示放在一张特殊的表hint\_plan.hints中。这个表包含了下列字段。

**说明：** 创建pg\_hint\_plan插件的用户默认拥有提示表的权限，提示表的优先权高于注释提示。

|字段|描述|
|--|--|
|id|提示ID号，唯一且自动填充。|
|norm\_query\_string|与要提示的查询匹配的模式。查询中的常量必须替换为`?`。空格在模式中很重要。|
|application\_name|应用会话的名称，置空表示任意应用。|
|hints|提示语句，不需要注释标记。|

示例命令如下：

```
INSERT INTO hint_plan.hints(norm_query_string, application_name, hints)
    VALUES (
        'EXPLAIN (COSTS false) SELECT * FROM t1 WHERE t1.id = ?;',
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

## 提示类型

根据提示短语影响执行计划的方式，可以被分为如下六类：

-   扫描方法提示

    扫描方法提示对目标表强制执行特定的扫描方法。pg\_hint\_plan通过表格的别名（如果存在的话）来识别目标表。扫描方法是`SeqScan`、`IndexScan`、`NoSeqScan`等。

    扫描提示对普通表、继承表、无日志表、临时表和系统表有效，对外部表、表函数、常量值语句、通用表达式、视图和子查询无效。

    示例命令如下：

    ```
    /*+
        SeqScan(t1)
        IndexScan(t2 t2_pkey)
     */
    SELECT * FROM table1 t1 JOIN table table2 t2 ON (t1.key = t2.key);
    ```

-   连接方法提示

    连接方法提示强制指定相关表格聚合在一起的方法。

    连接方法提示对普通表 、继承表、无日志表、临时表、外部表、系统表、表函数、常量值命令和通用表达式有效，对视图和子查询无效。

-   连接顺序提示

    连接顺序提示指定两个或多个表的连接顺序。这里有两种强制指定方法：

    -   强制执行特定的连接顺序，但不限制每个连接级别的方向。
    -   强制连接方向。
    示例命令如下：

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

-   行号纠正提示

    行号纠正提示会纠正由于计划器限制而导致的行号错误。

    示例命令如下：

    ```
    /*+ Rows(a b #10) */ SELECT... ;     //设置连接结果的行号为10。
    /*+ Rows(a b +10) */ SELECT... ;     //行号增加10。
    /*+ Rows(a b -10) */ SELECT... ;     //行号减去10。
    /*+ Rows(a b *10) */ SELECT... ;     //将行号扩大至原来的10倍。
    ```

-   并行执行提示

    并行提示会指定并行的执行计划。

    并行执行提示对普通表、继承表、无日志表和系统表有效，对外部表、常量从句、通用表达式、视图和子查询无效。视图的内部表可以通过其真实名称或别名指定目标对象。

    下面两个示例说明在每个表上执行查询的方式不同：

    -   方式一

        ```
        explain /*+ Parallel(c1 3 hard) Parallel(c2 5 hard) */
               SELECT c2.a FROM c1 JOIN c2 ON (c1.a = c2.a);
        ```

        返回如下结果：

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

    -   方式二

        ```
        EXPLAIN /*+ Parallel(tl 5 hard) */ SELECT sum(a) FROM tl;
        ```

        返回如下结果：

        ```
                                            QUERY PLAN                                  
        -----------------------------------------------------------------------------------
         Finalize Aggregate  (cost=693.02..693.03 rows=1 width=8)
           ->  Gather  (cost=693.00..693.01 rows=5 width=8)
                 Workers Planned: 5
                 ->  Partial Aggregate  (cost=693.00..693.01 rows=1 width=8)
                       ->  Parallel Seq Scan on tl  (cost=0.00..643.00 rows=20000 width=4)
        ```

-   设置临时GUC参数

    在计划的时候临时改变GUC参数。执行计划中的GUC参数会有预期的效果，除非提示语句与其他计划冲突。同样的GUC参数设置以最后一次为准。

    示例命令如下：

    ```
    /*+ Set(random_page_cost 2.0) */
    SELECT * FROM table1 t1 WHERE key = 'value';
    ```


所有提示支持的格式如下表。

|类别|格式|说明|
|--|--|--|
|扫描方法提示|SeqScan\(table\)|强制序列扫描。|
|TidScan\(table\)|强制TID扫描。|
|IndexScan\(table\[ index...\]\)|强制索引扫描，可以指定某个索引。|
|IndexOnlyScan\(table\[ index...\]\)|强制仅使用索引扫描，可以指定某个索引。|
|BitmapScan\(table\[ index...\]\)|强制使用Bitmap扫描。|
|NoSeqScan\(table\)|强制不使用序列扫描。|
|NoTidScan\(table\)|强制不使用TID扫描。|
|NoIndexScan\(table\)|强制不使用索引扫描。|
|NoIndexOnlyScan\(table\)|强制不使用索引扫描，仅扫描表。|
|NoBitmapScan\(table\)|强制不使用Bitmap扫描。|
|连接方法提示|NestLoop\(table table\[ table...\]\)|强制使用嵌套循环连接。|
|HashJoin\(table table\[ table...\]\)|强制使用散列连接。|
|MergeJoin\(table table\[ table...\]\)|强势使用合并连接。|
|NoNestLoop\(table table\[ table...\]\)|强制不使用嵌套循环连接。|
|NoHashJoin\(table table\[ table...\]\)|强制不使用散列连接。|
|NoMergeJoin\(table table\[ table...\]\)|强制不使用合并连接。|
|连接顺序提示|Leading\(table table\[ table...\]\)|强制连接的顺序。|
|Leading\(<join pair\>\)|强制连接的顺序和方向。|
|行号纠正提示|Rows\(table table\[ table...\] correction\)|纠正由指定表组成的联接结果的行号。可用的校正方法为绝对值`#<n>`、加法`+ <n>`、减法`-<n>`和乘法`* <n>`。`<n>`是strtod函数可以读取的数字。|
|并行执行提示|Parallel\(table <\# of workers\> \[soft\|hard\]\)|强制或禁止并行执行指定表。 `<worker#>`是所需的并行工作程序数量，0表示禁止并行执行。第三个参数如果是soft（默认），表示仅更改max\_parallel\_workers\_per\_gather并将其他所有内容留给计划器选择； 如果是hard，表示所有相关参数都会被强制指定。 |
|设置临时GUC参数|Set\(GUC-param value\)|规划器运行时，将GUC参数设置为该值。|

更多pg\_hint\_plan的介绍请参见[PostgreSQL官方文档](https://postgrespro.com/docs/enterprise/10/pg-hint-plan.html)。

