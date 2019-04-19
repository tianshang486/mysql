# There are 2 other sessions using the database错误处理 {#concept_186338 .concept}

## 错误信息 {#section_9yw_99x_re9 .section}

RDS for PostgreSQL删除数据库时报错如下：

``` {#codeblock_y03_q3w_omq}
ERROR: database "mctest" is being accessed by other users  详细：There are 2 other sessions using the database. 
```

## 原因 {#section_f82_a92_9ok .section}

当前有其他连接在使用该库。

## 解决方案 {#section_dhq_4xe_gqo .section}

断开mctest上所有的连接，命令如下：

``` {#codeblock_zt7_kgi_7lp}
select pg_terminate_backend(pid) from  (select pid from pg_stat_activity where datname = '<数据库名>'  ) a;
```

然后再删除数据库即可。

