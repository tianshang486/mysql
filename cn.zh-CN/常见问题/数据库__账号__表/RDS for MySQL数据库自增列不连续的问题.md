# RDS for MySQL数据库自增列不连续的问题 {#concept_265533 .concept}

## 问题现象 {#section_vra_jmb_bos .section}

使用RDS for MySQL数据库时， 发现自增列不连续。

## 问题原因 {#section_0y1_iud_1en .section}

由于数据库的列存在约束条件，插入数据失败，导致的了自增列不连续。

关于自增列的原理详情请参考MySQL的官方文档：[点此查看](https://dev.mysql.com/doc/refman/5.6/en/create-table.html)

