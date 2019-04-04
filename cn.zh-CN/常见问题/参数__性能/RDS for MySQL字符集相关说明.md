# RDS for MySQL字符集相关说明 {#concept_xdc_trr_ggb .concept}

## 字符序命名规则 {#section_ns5_vrr_ggb .section}

以字符序对应的字符集名称开头，以 \_ci（大小写不敏感）、\_cs（大小写敏感）、\_bin（按编码值比较，大小写敏感）结尾。

例如：当会话的collation\_connction设置为字符序utf8\_general\_ci时，字符a和字符A是等价的；而当其设置为utf8\_bin 时，字符a和字符A是不等价的。

请参考以下示例：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8273/155434895935365_zh-CN.png)

## 字符集相关 MySQL 命令 {#section_j51_yrr_ggb .section}

```
show global variables like '%char%';    #查看RDS实例字符集相关参数设置
show global variables like 'coll%';     #查看当前会话字符序相关参数设置
show character set;                     #查看实例支持的字符集
show collation;                         #查看实例支持的字符序
show create table table_name \G         #查看表字符集设置
show create database database_name \G   #查看数据库字符集设置
show create procedure procedure_name \G #查看存储过程字符集设置
show procedure status \G                #查看存储过程字符集设置
alter database db_name default charset utf8;  #修改数据库的字符集
create database db_name character set utf8;   #创建数据库时指定字符集
alter table tab_name default charset utf8 collate utf8_general_ci;   #修改表字符集和字符序
```

示例如图：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8273/155434895935366_zh-CN.png)

## 控制台修改字符集参数\(character\_set\_server\)的方法 {#section_vfb_yrr_ggb .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/155434895936543_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**参数设置**。
5.  在可修改参数页签下查找到**character\_set\_server**，单击右侧![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8266/155434895943351_zh-CN.jpg)进行修改并单击**确定**。

    ![修改character_set_server参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8266/155434895943352_zh-CN.png)

6.  在右上角单击**提交参数**，在弹出的对话框中单击**确定**，等待实例重启。

    **说明：** 该参数修改后，仅对开启高权限账号的实例后来创建的数据库有效，对当前数据库无效。

7.  
## 使用SQL语句修改数据库字符集的方法 {#section_y4b_yrr_ggb .section}

语法如下：

```
修改库：ALTER DATABASE <库名> CHARACTER SET  <字符集名称> COLLATE  <排序规则名称>;
修改表:ALTER TABLE <表名> CONVERT TO CHARACTER SET <字符集名称>  COLLATE  <排序规则名称>;
修改一列:ALTER TABLE <表名> MODIFY <列名>  <字段类型> CHARACTER SET  <字符集名称>  COLLATE <排序规则名称>;
```

示例: 三条sql 分别将库dbsdq、表tt2 、表tt2中的c2列修改为utf8mb4 字符集，命令如下：

```
alter database dbsdq character set utf8mb4 collate utf8mb4_unicode_ci;
use dbsdq;
alter table tt2 convert to character set utf8mb4 collate utf8mb4_unicode_ci;
alter table tt2 modify c2  varchar(10) character set utf8mb4 collate utf8mb4_unicode_ci;
```

**说明：** 

-   修改列时,当前列中的所有行都会立即转化为新的字符集。
-   alter table 会对表加元数据锁\(metadata lock\), 详情请参见[RDS MySQL 表上 Metadata lock 的产生和处理](https://help.aliyun.com/knowledge_detail/41723.html)。

## 如何正确设置数据库字符集编码 {#section_mzs_xsr_ggb .section}

请参见[RDS for MySQL如何保证数据库字符编码正确](cn.zh-CN/常见问题/参数__性能/RDS for MySQL如何保证数据库字符编码正确.md#)。

