# RDS for MySQL Online DDL 使用 {#concept_sww_pl2_jhb .concept}

本文介绍如何使用MySQL 5.6的新特性Online DDL。

RDS for MySQL 5.6支持Online DDL特性。

Online DDL（在线DDL）功能允许在表上执行DDL的操作（例如创建索引）的同时不阻塞并发的DML操作和查询（select）操作。

**说明：** 从低版本（例如 RDS for MySQL 5.5）升级到 RDS for MySQL 5.6，第一次执行 DDL 时有可能会因为表数据的文件格式仍旧是 5.5 版本而不支持 Online DDL 特性。这种情况可以通过执行以下命令来转换：

``` {#codeblock_4vs_bfm_jax}
alter table <表名> engine=innodb;
```

## Online DDL的限制 {#section_bc1_fm2_jhb .section}

|操作|是否支持Inplace方式|是否需要Copy Table|是否允许并发DML|是否允许并发查询|备注|
|--|-------------|--------------|---------|--------|--|
|创建普通索引|支持|不需要|允许|允许|-|
|创建全文索引|支持|不需要|不允许|允许|第一个全文索引需要通过Copy Table的方式创建；其后的全文索引可以通过Inplace方式创建。|
|删除索引|支持|不需要|允许|允许|仅修改表元数据metadata。|
|优化表|支持|需要|允许|允许|如果表上创建有全文索引，则不支持algorithm=inplace选项。|
|设置列默认值|支持|不需要|允许|允许|仅修改表云数据metadata。|
|修改自增列值|支持|不需要|允许|允许|仅修改表元数据metadata。|
|添加外键约束|支持|不需要|允许|允许|`set foreign_key_checks=0;`来关闭 foreign\_key\_checks，避免拷贝表。|
|删除外键约束|支持|不需要|允许|允许|foreign\_key\_checks选项开启或者关闭都可以。|
|重命名列|支持|不需要|允许|允许|如果仅仅修改字段名称，而不要修改字段类型，是支持并发DML操作的。|
|添加列|支持|需要|允许|允许| 在添加auto\_increment自增列时，是不允许并发 DML 操作的。

 尽管支持Algorithm=INPLACE ，但因为数据实质上需要重新组织，因此操作的开销高昂。

 |
|删除列|支持|需要|允许|允许|尽管支持Algorithm=INPLACE ，但因为数据实质上需要重新组织，因此操作的开销高昂。|
|修改各列顺序|支持|需要|允许|允许|尽管支持Algorithm=INPLACE ，但因为数据实质上需要重新组织，因此操作的开销高昂。|
|修改Row\_Format属性|支持|需要|允许|允许|尽管支持Algorithm=INPLACE ，但因为数据实质上需要重新组织，因此操作的开销高昂。|
|修改Key\_Block\_Size属性|支持|需要|允许|允许|尽管支持Algorithm=INPLACE ，但因为数据实质上需要重新组织，因此操作的开销高昂。|
|设置列为空值Null|支持|需要|允许|允许|尽管支持Algorithm=INPLACE ，但因为数据实质上需要重新组织，因此操作的开销高昂。|
|设置列不为空值NOT Null|支持|需要|允许|允许| 该操作需要将SQL\_MODE 参数设置为STRICT\_ALL\_TABLES或STRICT\_TRANS\_TABLES才能成功。如果列值中包含空值（NULL），则该DDL 操作会失败。

 尽管支持Algorithm=INPLACE ，但因为数据实质上需要重新组织，因此操作的开销高昂。

 |
|修改列的数据类型|不支持|需要|不允许|允许|-|
|添加主键|支持|需要|允许|允许| 尽管支持Algorithm=INPLACE ，但因为数据实质上需要重新组织，因此操作的开销高昂。

 如果涉及的列需要转换为NOT NULL，则不支持Algorithm=INPLACE。

 |
|删除主键并添加新主键|支持|需要|允许|允许| 仅当在同一个Alter Table语句中（删除主键的DDL语句）添加新主键才支持Algorithm=INPLACE。

 因为数据实质上需要重新组织，因此操作的开销高昂。

 |
|删除主键|不支持|需要|不允许|允许|-|
|Convert character set|不支持|需要|不允许|允许|如果新的字符集编码不同，需要重建表。|
|Specify character set|不支持|需要|不允许|允许|如果新的字符集编码不同，需要重建表。|
|带force选项重建表|支持|需要|允许|允许|如果表上有全文索引，则不支持Algorithm=Inplace选项。|
| 重建表

 alter table ... engine=innodb

 |支持|需要|允许|允许|如果表上有全文索引，则不支持Algorithm=Inplace选项。|
| 设置表的 persistent statistics

 |支持|不需要|允许|允许|仅修改表的元数据metadata。|

-   是否支持Inplace方式：对应DDL语句的Algorithm选项，通过Inplace方式执行DDL。相比Copy Table的方式，可以减少空间和I/O消耗。
-   是否需要Copy Table：对应DDL语句的Algorithm选项，通过Copy Table的方式执行DDL。DDL执行期间会占用更大的磁盘空间和消耗更多的I/O。
-   是否允许并发DML：对应DDL语句的Lock选项，DDL执行期间是否支持并发DML操作。
-   是否允许并发查询：DDL语句执行期间是否支持并发查询操作（通常都是支持的）。
-   MySQL官方文档请参考：[Online DDL 概览](https://dev.mysql.com/doc/refman/5.6/en/innodb-online-ddl-operations.html)。
-   DDL操作执行时需要修改表的元数据（metadata），有可能会遇到等待表元数据锁的情况（waiting for table metadata lock），该情况的处理方式请参考[解决MDL锁导致无法操作数据库的问题](../../../../intl.zh-CN/最佳实践/MySQL/故障处理/解决MDL锁导致无法操作数据库的问题.md#)。
-   Inplace和Copy Table是相反的2种处理方式；但即使DDL支持Inplace选项，某些操作在整个执行过程中也会部分涉及到Copy Table，例如上表中的添加列操作。

## Online DDL选项建议 {#section_r2h_5r2_jhb .section}

-   Algorithm=Inplace ：为了避免Copy Table导致的实例性能问题（空间、I/O问题），建议在DDL中包含该选项。如果DDL操作不支持Algorithm=Inplace方式，DDL操作会立刻返回错误。

    ``` {#codeblock_2ba_oxd_t4u}
    alter table area_bak algorithm=inplace, modify father text;
    
    ERROR 1846 (0A000): ALGORITHM=INPLACE is not supported. Reason: Cannot change column type INPLACE. Try ALGORITHM=COPY.
    ```

-   Lock=None ：为了在DDL操作过程中不影响业务DML 操作，建议在DDL中包含该选项。如果DDL操作不支持Lock=None （允许并行DML操作）选项，DDL操作会立刻返回错误。

    ``` {#codeblock_5zv_hx3_d3v}
    alter table area ALGORITHM=copy, lock=none,CONVERT TO CHARACTER SET utf8mb4;
    
    ERROR 1846 (0A000): LOCK=NONE is not supported. Reason: COPY algorithm requires a lock. Try LOCK=SHARED.
    ```


默认情况下RDS for MySQL会尽量使用algorithm=inplace以及lock=none来进行DDL操作，因此默认可以不指定这两个选项。但如果担心DDL操作对系统负载有影响或阻塞对目标表的DML操作，建议使用algorithm=inplace或lock=none选项来操作，这样如果系统对某一个选项不支持，会立刻返回错误，避免影响业务。

示例

``` {#codeblock_y14_6w8_jib}
alter table area algorithm=inplace, lock=none, add index idx_fa (father);
```

**说明：** 所有的DDL操作均建议在业务低峰期进行，避免对业务产生影响。

对不支持Online DDL的操作（例如RDS for MySQL 5.5），可以考虑通过Percona的Schema Online Change工具来操作，请参考[RDS for MySQL 如何使用 Percona Toolkit](https://help.aliyun.com/knowledge_detail/13098164.html?spm=a2c4g.11186623.2.22.cb0a2867KJiYg9)。

Alter Table语法请参考[ALTER TABLE Syntax](http://dev.mysql.com/doc/refman/5.6/en/alter-table.html?spm=a2c4g.11186623.2.23.cb0a2867KJiYg9)。

## 异常处理 {#section_gzj_qs2_jhb .section}

在对某些大表的Online DDL过程中，有时会碰到下面的错误：

``` {#codeblock_bxr_cd9_ec0}
alter table rd_order_rec add index idx_cr_time_detail (cr_time,detail);

ERROR 1799(HY000): Creating index 'idx_cr_time_detail' required more than 'innodb_online_alter_log_max_size' bytes of modification log. Please try again.
```

原因

在进行Online DDL（不阻塞并发DML） 的过程中，每个被修改的表或者创建的索引都会使用一个临时日志来保存 DDL过程中并发DML操作的记录。该临时日志文件的大小可以根据需要从参数innodb\_sort\_buffer\_size指定的大小扩展到参数nnodb\_online\_alter\_log\_max\_size指定的大小。

如果有临时日志文件大小超过上限，则该DDL语句返回失败并且所有没有提交的并发DML操作会被回滚。因此增加 innodb\_online\_alter\_log\_max\_size参数的大小可以允许DDL过程中更多的并发DML操作，但是较大的值也会使在DDL操作末尾阶段的锁定表应用日志中的数据的过程持续更长的时间。

解决方法

针对MySQL 5.6/5.7，可以在控制台修改innodb\_online\_alter\_log\_max\_size参数值，详细步骤请参见[设置实例参数](intl.zh-CN/RDS for MySQL 用户指南/实例管理/设置实例参数.md#)。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8301/156894988060853_zh-CN.png)

