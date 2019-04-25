# RDS for MySQL auto\_increment自增字段相关参数 {#concept_41740_zh .concept}

RDS for MySQL经常会使用到auto\_increment自增长字段，下面是相关参数的说明。

|参数名称|默认值|取值范围|作用|
|----|---|----|--|
|auto\_increment\_increment|1|1~65535|控制增量的幅度。|
|auto\_increment\_offset|1|1~65535|增量开始的位置（开始的偏移量）。|

**说明：** 

-   两个参数均可以在全局和会话级别设置。
-   如果auto\_increment\_offset的值大于auto\_increment\_increment，则auto\_increment\_offset被忽略。

示例：

``` {#codeblock_uj0_ba3_mft}
Create table au (id int auto_increment primary key);
```

## 插入奇数 {#section_5cs_yrb_drq .section}

查看当前会话auto\_increment相关参数设置：

``` {#codeblock_um0_1nt_xpv}
show variables like 'auto_i%';
```

插入4行数据：

``` {#codeblock_owj_tus_c77}
insert into au values (null),(null),(null),(null);
```

检查表内数据：

``` {#codeblock_mx2_87k_pzq}
select * from au;
```

![插入奇数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8254/155618064245466_zh-CN.png)

## 插入偶数 {#section_jdr_xql_jpd .section}

![插入偶数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8254/155618064245467_zh-CN.png)

## 插入以300001开始的奇数 {#section_6pt_s2m_2n4 .section}

设置表auto increment初始值为300001：

``` {#codeblock_hvq_50u_z4d}
alter table au auto_increment=300001;
```

![300001开始](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8254/155618064245468_zh-CN.png)

## 插入以300002开始的偶数 {#section_mnu_yw2_7v2 .section}

设置表auto increment字段初始值为300002：

``` {#codeblock_ynk_j6t_2zh}
alter table au auto_increment=300002;
```

![300002开始](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8254/155618064245470_zh-CN.png)

## 插入初始值为3，增量为5的记录 {#section_t00_ddb_a7e .section}

![应用](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8254/155618064345471_zh-CN.png)

