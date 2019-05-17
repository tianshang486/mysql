# RDS for PostgreSQL跨库查询 {#concept_266438 .concept}

RDS for PostgreSQL可以通过dblink插件来实现跨库查询。

## 创建dblink插件 {#section_305_su1_184 .section}

登录源库，创建dblink插件，命令如下：

``` {#codeblock_ins_124_no9}
create extension dblink;
```

## 创建到目的库的连接 {#section_fw4_1pi_j48 .section}

创建到目的库的连接，命令如下：

``` {#codeblock_s5o_hr3_h1n}
select dblink_connect(‘<连接名称>’,’host=<目的实例域名> port=<目的实例端口> dbname=<目的库名称> user=<目的库账号> password=<目的库密码>’);
```

**示例**

``` {#codeblock_p8n_5uw_s0l}
select dblink_connect(‘test1_test2’,’host=rdsxxx.pg.rds.aliyuncs.com port=3433 dbname=test2 user=pgtest2 password=123456’);
```

**说明：** 如果使用dblink访问相同实例的不同数据库，则其中的host=localhost，可以通过`show port;`来获得本地的端口。

## 跨库查询 {#section_dtg_c49_h6j .section}

跨库查询示例如下：

``` {#codeblock_ofa_1m8_l4f}
select * from dblink(‘test1_test2’,’select * from area_j02’) as area_j02(id int, name varchar(20));
```

