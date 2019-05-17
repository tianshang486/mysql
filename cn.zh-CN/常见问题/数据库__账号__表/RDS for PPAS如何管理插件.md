# RDS for PPAS如何管理插件 {#concept_266466 .concept}

RDS for PPAS没有对外开放超级用户，为了解决插件问题，RDS在模板库template1上创建了一个插件管理函数rds\_manage\_extension。

您可以在创建数据库时使用模板库，示例如下：

``` {#codeblock_xpb_q5l_6hz}
create database mydb template template1;
```

这样您的数据库中就存在插件管理函数。

用RDS高权限用户登录自己的数据库，使用这个插件可以创建和删除外部插件，示例如下：

``` {#codeblock_8yf_xmv_d8j}
select rds_manage_extension('create','dblink');  --创建插件
select rds_manage_extension('drop','dblink');  --删除插件
```

目前支持管理的插件如下：

|支持的插件|支持的插件|
|-----|-----|
|pg\_stat\_statements|pg\_prewarm|
|oss\_fdw|pg\_trgm|
|btree\_gin|postgres\_fdw|
|btree\_gist|sslinfo|
|chkpass|tablefunc|
|citext|tsearch2|
|cube|unaccent|
|dblink|postgis|
|dict\_int|postgis\_topology|
|earthdistance|fuzzystrmatch|
|hstore|postgis\_tiger\_geocoder|
|intagg|plperl|
|intarray|pltcl|
|isn|plv8|
|ltree|uuid-ossp|
|pgcrypto|plpgsql|
|pgrowlocks| |

