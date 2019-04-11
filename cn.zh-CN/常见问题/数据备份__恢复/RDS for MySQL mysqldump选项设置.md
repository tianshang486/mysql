# RDS for MySQL mysqldump选项设置 {#concept_lr2_ht5_jhb .concept}

## GTID特性介绍 {#section_txc_jt5_jhb .section}

MySQL 5.6引入了GTID特性，因此5.6版本的mysqldump工具增加了set-gtid-purged选项。

|选项名称|默认值|可选值|作用|
|----|---|---|--|
|set-gtid-purged|AUTO|ON|OFF|AUTO|是否输出 SET @@GLOBAL.GTID\_PURGED 子句。|

**说明：** 

-   ON：在mysqldump输出中包含SET @@GLOBAL.GTID\_PURGED语句。
-   OFF：在mysqldump输出中不包含 SET @@GLOBAL.GTID\_PURGED 语句。
-   AUTO：默认值。对于启用了GTID的实例，会输出 SET @@GLOBAL.GTID\_PURGED语句；对于没有启动或者不支持GTID的实例，不输出任何GTID相关信息。

因此对于使用MySQL 5.6及以上版本自带的mysqldump工具导出RDS for MySQL 5.5版本实例数据时，需要设置set-gtid-purged为OFF，否则会报以下错误：

```
Error: Server has GTIDs disabled.
或者
mysqldump: Couldn’t execute ‘SELECT @@GTID_MODE’: Unknown system variable ‘GTID_MODE’ <1193>
```

## 避免表级锁等待 {#section_v2l_lw5_jhb .section}

mysqldump默认会启用lock-tables选项，对要导出的表加表级锁，阻止表上的DML操作。

RDS for MySQL实例默认支持的InnoDB和TokuDB引擎均支持事务，建议使用single-transaction选项进行导出，而不要设置lock-all-tables或lock-tables选项。

|选项名称|默认值|可选值|作用|
|----|---|---|--|
|lock-all-tables|FALSE|TRUE|FALSE|在数据导出期间设置global read lock，所有库下的所有表在导出期间为只读。自动关闭lock-tables和single-transaction选项。RDS不支持该选项。|
|lock-tables|TRUE|TRUE|FALSE|导出期间在导出表上设置表级锁。默认开启。可以通过指定 skip-lock-tables选项来关闭。|
|single-transaction|FALSE|TRUE|FALSE|导出操作被放置在一个事务中执行。自动关闭lock-tables选项。|

更多表级锁的内容请参见[RDS for MySQL表级锁等待](cn.zh-CN/常见问题/参数__性能/RDS for MySQL表级锁等待.md#)。

## 设置导出字符集 {#section_lvr_2x5_jhb .section}

如果不指定，mysqldump默认使用UTF8字符集进行导出。

|选项名称|默认值|可选值|作用|
|----|---|---|--|
|default-character-set|UTF8|实例支持的字符集|mysqldump到RDS实例导出连接的字符集。|

## 其他导出时需要注意的选项 {#section_ybh_jx5_jhb .section}

|选项名称|默认值|可选值|作用|
|----|---|---|--|
|no-defaults|NA|NA|除了.mylogin.cnf，不读取任何选项文件。|
|defaults-file=file\_name|NA|NA|读取指定的选项文件。|
|add-drop-database|FALSE|TRUE|FALSE|在create database语句前增加drop database语句。|
|add-drop-table|TRUE|TRUE|FALSE|在create table语句前增加drop table语句，默认开启，使用选项skip-add-drop-table来关闭。|
|add-locks|TRUE|TRUE|FALSE|在表相关语句前后增加lock tables tab\_name write和unlock tables语句。这样在导入数据时可以加快数据导入。|
|compatible=name|NA|ansi|postgresql|oracle|mssql|增强与指定的数据库类型的兼容性。|
|compact|FALSE|TRUE|FALSE|启用skip-add-drop-table、skip-add-locks、skip-comments、skip-disable-keys、skip-set-charset 选项。|
|databases|TRUE|TRUE|FALSE|导出多个库。默认mysqldump将第一个名字识别为库，其后的名字识别为表。指定该选项后，mysqldump会将所有名称识别为库，并在每个库前增加create database和use database语句。|
|disable-keys|TRUE|TRUE|FALSE|在插入数据前后增加`/!40000 ALTER TABLE tab_name DISABLE KEYS /`和`/!40000 ALTER TABLE tab_name ENABLE KEYS /`语句来加速插入。该选项仅对 MyISAM 引擎表的非唯一索引有效。|
|events|FALSE|TRUE|FALSE|导出数据库内的计划事件（定时任务）。|
|extended-insert|TRUE|TRUE|FALSE|使用扩展的Insert语句，一条Insert语句插入多行。|
|hex-blob|FALSE|TRUE|FALSE|以16进制导出Binary、VarBinary、BLOB类型数据。如果跨版本迁移数据，建议增加该选项。|
|ignore-table=db.tab|TRUE|TRUE|FALSE|不导出某表或视图。格式：库名.表名（db.tab\)。可以多次使用该选项来忽略多张表。|
|max-allowed-packet|24MB|24MB-1GB|mysqldump和RDS实例通信缓存最大值。默认24MB。最大1GB。|
|no-create-db|FALSE|TRUE|FALSE|输出中不包含create database语句。|
|no-create-info|FALSE|TRUE|FALSE|输出中不包含create table语句。|
|no-data|FALSE|TRUE|FALSE|不导出数据。|
|opt|TRUE|TRUE|FALSE|启用add-drop-table、add-locks、create-options、disable-keys、extended-insert、lock-tables、quick、set-charset，可以通过指定skip-opt选项关闭默认opt选项。|
|dump-date|TRUE|TRUE|FALSE|如果指定了comments选项（默认开启），在输出的注释中显示导出日期时间。|
|routines|FALSE|TRUE|FALSE|导出存储过程和函数（默认不导出）。|
|result-file|TRUE|TRUE|FALSE|将输出重定向到文件。|
|set-charset|TRUE|TRUE|FALSE|在导出文件中加上set names default\_chararacter\_set。|
|triggers|TRUE|TRUE|FALSE|导出表上的Trigger。|

## RDS for MySQL 不支持的选项 {#section_gpb_v1v_jhb .section}

|选项名称|默认值|可选值|作用|
|----|---|---|--|
|all-databases|FALSE|实例支持的字符集|导出所有数据库，包括 mysql。|
|flush-logs|FALSE|TRUE|FALSE|导出前在实例中执行`flush logs;`命令。|
|flush-privileges|FALSE|TRUE|FALSE|导出mysql系统库后，输出中包含`flush privileges;`命令。|
|lock-all-tables|FALSE|TRUE|FALSE|在数据导出期间放置global read lock，所有库下的所有表在导出期间为只读。自动关闭lock-tables和single-transaction选项。|
|tab=dir\_name|NA|NA|在指定的目录下生成tbl\_name.sql文件（包含表创建语句）和 以tab作为分隔符的tbl\_name.txt文本格式的数据文件。|

**原因说明**

-   all-databases：RDS for MySQL普通用户对mysql库中部分表没有权限，因此不能导出全部库表。

    **错误信息**

    ```
    
    mysqldump: Couldn’t execute ‘show create table slow_log‘: SHOW command denied to user ‘xxx’@’xx.xx.xx.xx’ for table ‘slow_log’ (1142)
    ```

-   flush-logs： RDS for MySQL普通用户没有reload权限，因此不能执行`flush logs;`命令。

    **错误信息**

    ```
    mysqldump: Couldn’t execute ‘FLUSH TABLES’: Access denied; you need (at least one of) the RELOAD privilege(s) for this operation (1227)
    ```

-   flush-privileges：RDS for MySQL不支持mysql系统库的导出，因此没必要使用该选项。
-   lock-all-tables：RDS for MySQL普通用户没有reload权限，因此不能使用该选项。

    **错误信息**

    ```
    mysqldump: Couldn’t execute ‘FLUSH TABLES’: Access denied; you need (at least one of) the RELOAD privilege(s) for this operation (1227)
    ```

-   tab=dir\_name：该选项要求mysqldump和RDS for MySQL实例在同一物理机上，因此不支持。但该选项可以和no-data选项搭配使用来获取表的创建语句。

    ```
    # 和no-data选项搭配，获取test库下每个表的创建语句文件tab_name.sql
    mysqldump  —no-defaults -uuser_name -ppass_word -hxxx.mysql.rds.aliyuncs.com -P3306 —set-gtid-purged=off —single-transaction —tab=/tmp —no-data test
    #  —no-daa 选希望导出数据）时候的错误信息：
    mysqldump  —no-defaults -uuser_name -ppass_word -hxxx.mysql.rds.aliyuncs.com -P3306 —set-gtid-purged=off —single-transaction —tab=/tmp test
    mysqldump: Got error: 1045: Access denied for user ‘xxx’@’%’ (using password: YES) when executing ‘SELECT INTO OUTFILE’
    ```


