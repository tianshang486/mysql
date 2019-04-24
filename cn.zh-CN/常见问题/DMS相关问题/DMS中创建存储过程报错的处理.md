# DMS中创建存储过程报错的处理 {#concept_188008 .concept}

## 错误信息 {#section_tgy_nya_y7i .section}

DMS中使用SQL语句创建存储过程时报如下错误。

![dms创建存储过程报错](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8413/155608501145280_zh-CN.png)

## 错误原因 {#section_hpw_u6s_bjc .section}

dms中默认是以一个分号（;）作为一条语句结束的标志，但存储过程需要执行一段SQL，这些SQL是不可分割的。

## 解决方案 {#section_3nq_v4f_p3b .section}

使用DELIMITER临时设置新的结束符。以双斜杠（//）为例，修改SQL代码如下：

``` {#codeblock_twy_ux4_v7d}
DELIMITER //
CREATE  PROCEDURE  p_test()
BEGIN 
  select CURRENT_DATE  as curDate ;
END//

DELIMITER ;
```

**说明：** `DELIMITER ;`表示还原为以分号（;）作为结束标识符的默认设置。

