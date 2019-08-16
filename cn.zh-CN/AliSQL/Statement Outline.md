# Statement Outline {#concept_1664234 .concept}

生产环境中，SQL语句的执行计划经常会发生改变，导致数据库不稳定。阿里云利用Optimizer Hint和Index Hint让MySQL稳定执行计划，该方法称为Statement Outline，并提供了工具包（DBMS\_OUTLN）便于您快捷使用。

## 前提条件 {#section_k46_kac_fe6 .section}

实例版本为RDS for MySQL 8.0。

## 功能设计 {#section_tp6_iks_j2z .section}

Statement Outline支持官方MySQL 8.0的所有hint类型，分为如下两类：

-   Optimizer Hint

    根据作用域和hint对象，分为Global level hint、Table/Index level hint、Join order hint等。详情请参见[MySQL官网](https://dev.mysql.com/doc/refman/8.0/en/optimizer-hints.html)。

-   Index Hint

    根据Index Hint的类型和范围进行分类。详情请参见[MySQL官网](https://dev.mysql.com/doc/refman/8.0/en/index-hints.html)


## Statement Outline表介绍 {#section_vht_dvt_dzq .section}

AliSQL内置了一个系统表（outline）保存hint，系统启动时会自动创建该表，无需您手动创建。这里提供表的创建语句供您参考：

``` {#codeblock_r1h_qn2_qjn}
​CREATE TABLE `mysql`.`outline` (
  `Id` bigint(20) NOT NULL AUTO_INCREMENT,
  `Schema_name` varchar(64) COLLATE utf8_bin DEFAULT NULL,
  `Digest` varchar(64) COLLATE utf8_bin NOT NULL,
  `Digest_text` longtext COLLATE utf8_bin,
  `Type` enum('IGNORE INDEX','USE INDEX','FORCE INDEX','OPTIMIZER') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `Scope` enum('','FOR JOIN','FOR ORDER BY','FOR GROUP BY') CHARACTER SET utf8 COLLATE utf8_general_ci DEFAULT '',
  `State` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'Y',
  `Position` bigint(20) NOT NULL,
  `Hint` text COLLATE utf8_bin NOT NULL,
  PRIMARY KEY (`Id`)
) /*!50100 TABLESPACE `mysql` */ ENGINE=InnoDB
DEFAULT CHARSET=utf8 COLLATE=utf8_bin STATS_PERSISTENT=0 COMMENT='Statement outline'​
```

参数说明如下。

|参数|说明|
|--|--|
|Id|Outline ID。|
|Schema\_name|数据库名。|
|Digest|**Digest\_text**进行hash计算得到的64字节的hash字符串。|
|Digest\_text|SQL语句的特征。|
|Type| -   Optimizer Hint中，hint类型的取值为OPTIMIZER。
-   Index Hint中，hint类型的取值为USE INDEX、FORCE INDEX或IGNORE INDEX。

 |
|Scope|仅Index Hint需要提供，分为如下三类： -   FOR GROUP BY
-   FOR ORDER BY
-   FOR JOIN

 空串表示所有类型的Index Hint。

 |
|State|本规则是否启用。|
|Position| -   Optimizer Hint中，Position表示Query Block， 因为所有的Optimizer Hint必须作用到 Query Block上，所以，Position从1开始，hint作用在语句的第几个关键字上，Position就是几。
-   Index Hint中，Position表示表的位置， 也是从1开始，hint作用在第几个表上，Position就是几。

 |
|Hint| -   Optimizer Hint中，Hint表示完整的hint字符串，例如`/*+ MAX_EXECUTION_TIME(1000) */`。
-   Index Hint中，Hint表示索引名字的列表， 例如`ind_1,ind_2`。

 |

## 管理Statement Outline {#section_mz6_5vp_2qs .section}

为了便捷地管理Statement Outline，AliSQL在DBMS\_OUTLN中定义了六个本地存储规则。详细说明如下：

-   add\_optimizer\_outline

    增加Optimizer Hint。命令如下：

    ``` {#codeblock_7or_56j_xr9}
    dbms_outln.add_optimizer_outline('<Schema_name>','<Digest>','<query_block>','<hint>','<query>');
    ```

    **说明：** Digest和Query（原始SQL语句）可以任选其一。如果填写Query，DBMS\_OUTLN会计算Digest和Digest\_text。

    示例：

    ``` {#codeblock_z6e_jhh_8oj}
    CALL DBMS_OUTLN.add_optimizer_outline("outline_db", '', 1, '/*+ MAX_EXECUTION_TIME(1000) */',
                                          "select * from t1 where id = 1");
    ```

-   add\_index\_outline

    增加Index Hint。命令如下：

    ``` {#codeblock_0vc_clx_wok}
    dbms_outln.add_index_outline('<Schema_name>','<Digest>',<Position>,'<Type>','<Hint>','<Scope>','<Query>');
    ```

    **说明：** Digest和Query（原始SQL语句）可以任选其一。如果填写Query，DBMS\_OUTLN会计算Digest和Digest\_text。

    示例：

    ``` {#codeblock_7yq_rs4_iqe}
    call dbms_outln.add_index_outline('outline_db', '', 1, 'USE INDEX', 'ind_1', '',
                                    "select * from t1 where t1.col1 =1 and t1.col2 ='xpchild'");
    ```

-   preview\_outline

    查看匹配Statement Outline的情况，可用于手动验证。命令如下：

    ``` {#codeblock_ejy_c0l_zfa}
    dbms_outln.preview_outline('<Schema_name>','<Query>');
    ```

    示例：

    ``` {#codeblock_381_5ez_ehu}
    ​mysql> call dbms_outln.preview_outline('outline_db', "select * from t1 where t1.col1 =1 and t1.col2 ='xpchild'");
    +------------+------------------------------------------------------------------+------------+------------+-------+---------------------+
    | SCHEMA     | DIGEST                                                           | BLOCK_TYPE | BLOCK_NAME | BLOCK | HINT                |
    +------------+------------------------------------------------------------------+------------+------------+-------+---------------------+
    | outline_db | b4369611be7ab2d27c85897632576a04bc08f50b928a1d735b62d0a140628c4c | TABLE      | t1         |     1 | USE INDEX (`ind_1`) |
    +------------+------------------------------------------------------------------+------------+------------+-------+---------------------+
    1 row in set (0.00 sec)​
    ```

-   show\_outline

    展示Statement Outline在内存中命中的情况。命令如下：

    ``` {#codeblock_l0d_fkp_336}
    dbms_outln.show_outline();
    ```

    示例：

    ``` {#codeblock_xo0_mj7_83x}
    ​mysql> call dbms_outln.show_outline();
    +------+------------+------------------------------------------------------------------+-----------+-------+------+-------------------------------------------------------+------+----------+-------------------------------------------------------------------------------------+
    | ID   | SCHEMA     | DIGEST                                                           | TYPE      | SCOPE | POS  | HINT                                                  | HIT  | OVERFLOW | DIGEST_TEXT                                                                         |
    +------+------------+------------------------------------------------------------------+-----------+-------+------+-------------------------------------------------------+------+----------+-------------------------------------------------------------------------------------+
    |   33 | outline_db | 36bebc61fce7e32b93926aec3fdd790dad5d895107e2d8d3848d1c60b74bcde6 | OPTIMIZER |       |    1 | /*+ SET_VAR(foreign_key_checks=OFF) */                |    1 |        0 | SELECT * FROM `t1` WHERE `id` = ?                                                   |
    |   32 | outline_db | 36bebc61fce7e32b93926aec3fdd790dad5d895107e2d8d3848d1c60b74bcde6 | OPTIMIZER |       |    1 | /*+ MAX_EXECUTION_TIME(1000) */                       |    2 |        0 | SELECT * FROM `t1` WHERE `id` = ?                                                   |
    |   34 | outline_db | d4dcef634a4a664518e5fb8a21c6ce9b79fccb44b773e86431eb67840975b649 | OPTIMIZER |       |    1 | /*+ BNL(t1,t2) */                                     |    1 |        0 | SELECT `t1` . `id` , `t2` . `id` FROM `t1` , `t2`                                   |
    |   35 | outline_db | 5a726a609b6fbfb76bb8f9d2a24af913a2b9d07f015f2ee1f6f2d12dfad72e6f | OPTIMIZER |       |    2 |  /*+ QB_NAME(subq1) */                                |    2 |        0 | SELECT * FROM `t1` WHERE `t1` . `col1` IN ( SELECT `col1` FROM `t2` )               |
    |   36 | outline_db | 5a726a609b6fbfb76bb8f9d2a24af913a2b9d07f015f2ee1f6f2d12dfad72e6f | OPTIMIZER |       |    1 | /*+ SEMIJOIN(@subq1 MATERIALIZATION, DUPSWEEDOUT) */  |    2 |        0 | SELECT * FROM `t1` WHERE `t1` . `col1` IN ( SELECT `col1` FROM `t2` )               |
    |   30 | outline_db | b4369611be7ab2d27c85897632576a04bc08f50b928a1d735b62d0a140628c4c | USE INDEX |       |    1 | ind_1                                                 |    3 |        0 | SELECT * FROM `t1` WHERE `t1` . `col1` = ? AND `t1` . `col2` = ?                    |
    |   31 | outline_db | 33c71541754093f78a1f2108795cfb45f8b15ec5d6bff76884f4461fb7f33419 | USE INDEX |       |    2 | ind_2                                                 |    1 |        0 | SELECT * FROM `t1` , `t2` WHERE `t1` . `col1` = `t2` . `col1` AND `t2` . `col2` = ? |
    +------+------------+------------------------------------------------------------------+-----------+-------+------+-------------------------------------------------------+------+----------+-------------------------------------------------------------------------------------+
    7 rows in set (0.00 sec)​
    ```

    关于HIT和OVERFLOW的说明如下。

    |参数|说明|
    |--|--|
    |HIT|此Statement Outline命中的次数。|
    |OVERFLOW|此Statement Outline没有找到Query block或相应的表的次数。|

-   del\_outline

    删除内存和表中的某一条Statement Outline。命令如下：

    ``` {#codeblock_hof_2qz_o7s}
    dbms_outln.del_outline(<Id>);
    ```

    示例：

    ``` {#codeblock_nz0_syk_xbe}
    ​mysql> call dbms_outln.del_outline(32);
    ```

    **说明：** 如果删除的规则不存在，系统会报相应的警告，您可以使用`show warnings;`查看警告内容。

    ``` {#codeblock_acw_53r_09o}
    ​mysql> call dbms_outln.del_outline(1000);
    Query OK, 0 rows affected, 2 warnings (0.00 sec)
    
    mysql> show warnings;
    +---------+------+----------------------------------------------+
    | Level   | Code | Message                                      |
    +---------+------+----------------------------------------------+
    | Warning | 7521 | Statement outline 1000 is not found in table |
    | Warning | 7521 | Statement outline 1000 is not found in cache |
    +---------+------+----------------------------------------------+
    2 rows in set (0.00 sec)​
    ```

-   flush\_outline

    如果您直接操作了表outline修改Statement Outline，您需要让Statement Outline重新生效。命令如下：

    ``` {#codeblock_8je_7mu_3md}
    dbms_outln.flush_outline(); 
    ```

    示例：

    ``` {#codeblock_v8d_i1n_y1s}
    mysql> update mysql.outline set Position = 1 where Id = 18;
    Query OK, 1 row affected (0.00 sec)
    Rows matched: 1  Changed: 1  Warnings: 0
    
    ​mysql> call dbms_outln.flush_outline(); 
    Query OK, 0 rows affected (0.01 sec)​
    ```


## 功能测试 {#section_x4e_9l4_3sl .section}

验证Statement Outline是否有效果，有如下两种方法：

-   通过preview\_outline进行预览。

    ``` {#codeblock_r27_jn5_s6c}
    mysql> call dbms_outln.preview_outline('outline_db', "select * from t1 where t1.col1 =1 and t1.col2 ='xpchild'");
    +------------+------------------------------------------------------------------+------------+------------+-------+---------------------+
    | SCHEMA     | DIGEST                                                           | BLOCK_TYPE | BLOCK_NAME | BLOCK | HINT                |
    +------------+------------------------------------------------------------------+------------+------------+-------+---------------------+
    | outline_db | b4369611be7ab2d27c85897632576a04bc08f50b928a1d735b62d0a140628c4c | TABLE      | t1         |     1 | USE INDEX (`ind_1`) |
    +------------+------------------------------------------------------------------+------------+------------+-------+---------------------+
    1 row in set (0.01 sec)
    ```

-   直接使用explain查看。

    ``` {#codeblock_aj8_v2i_f2k}
    mysql> explain select * from t1 where t1.col1 =1 and t1.col2 ='xpchild';
    +----+-------------+-------+------------+------+---------------+-------+---------+-------+------+----------+-------------+
    | id | select_type | table | partitions | type | possible_keys | key   | key_len | ref   | rows | filtered | Extra       |
    +----+-------------+-------+------------+------+---------------+-------+---------+-------+------+----------+-------------+
    |  1 | SIMPLE      | t1    | NULL       | ref  | ind_1         | ind_1 | 5       | const |    1 |   100.00 | Using where |
    +----+-------------+-------+------------+------+---------------+-------+---------+-------+------+----------+-------------+
    1 row in set, 1 warning (0.00 sec)
    
    mysql> show warnings;
    +-------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | Level | Code | Message                                                                                                                                                                                                                                                 |
    +-------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | Note  | 1003 | /* select#1 */ select `outline_db`.`t1`.`id` AS `id`,`outline_db`.`t1`.`col1` AS `col1`,`outline_db`.`t1`.`col2` AS `col2` from `outline_db`.`t1` USE INDEX (`ind_1`) where ((`outline_db`.`t1`.`col1` = 1) and (`outline_db`.`t1`.`col2` = 'xpchild')) |
    +-------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    1 row in set (0.00 sec)
    ```


