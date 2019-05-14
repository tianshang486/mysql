# RDS for MySQL查看表的主键字段的方法 {#concept_265113 .concept}

## 查看系统表 {#section_v7y_lpk_w7v .section}

``` {#codeblock_zeb_bcq_bo3}
SELECT
  t.TABLE_NAME,
  t.CONSTRAINT_TYPE,
  c.COLUMN_NAME,
  c.ORDINAL_POSITION
FROM
  INFORMATION_SCHEMA.TABLE_CONSTRAINTS AS t,
  INFORMATION_SCHEMA.KEY_COLUMN_USAGE AS c
WHERE
  t.TABLE_NAME = c.TABLE_NAME
  AND t.CONSTRAINT_TYPE = 'PRIMARY KEY'
  AND t.TABLE_NAME='<表名>'
  AND t.TABLE_SCHEMA='<数据库名>';
```

## 查看建表语句 {#section_gjq_gmx_0nd .section}

``` {#codeblock_5qr_llv_xu3}
show create table <表名>;
```

## 查看表结构 {#section_aj3_4fu_szq .section}

``` {#codeblock_909_uc5_3rf}
desc <表名>；
```

