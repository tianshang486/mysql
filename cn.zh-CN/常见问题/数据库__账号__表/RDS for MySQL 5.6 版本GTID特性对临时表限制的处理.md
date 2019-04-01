# RDS for MySQL 5.6 版本GTID特性对临时表限制的处理 {#concept_uvl_pwz_ghb .concept}

由于RDS for MySQL 5.6版本引入了GTID特性，因此要求应用不能够在事务中创建和删除临时表。

## 错误信息 {#section_wsj_wwz_ghb .section}

```
When @@GLOBAL.ENFORCE_GTID_CONSISTENCY = 1, the statements CREATE TEMPORARY TABLE and DROP TEMPORARY TABLE ca n be executed in a non-transactional context only, and require that AUTOCOMMIT = 1.
```

## 解决方法 {#section_rrd_zwz_ghb .section}

-   将`create temporary table`语句更改为`create table`，使用普通表替代临时表，规避这个问题。
-   修改代码，将临时表的创建和删除操作放在事务外，并且保证会话的参数`autocommit=1`。

如果问题还未能解决，请联系[售后技术支持](https://selfservice.console.aliyun.com/ticket/createIndex.htm)。

