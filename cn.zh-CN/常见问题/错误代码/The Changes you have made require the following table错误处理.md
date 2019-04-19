# The Changes you have made require the following table错误处理 {#concept_186288 .concept}

## 错误信息 {#section_xvi_ksj_w86 .section}

RDS for SQL Server实例中修改表结构，保存时报错。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8337/155564477644901_zh-CN.jpg)

## 原因及解决方案 {#section_pz9_kfs_myc .section}

RDS for SQL Server开启了**Prevent saving changes that require the table re-creation**选项，在**Tools** \> **Designers** \> **Table and Database Designers** \> **Table options**里关闭该选项即可。

![关闭选项](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8337/155564477644904_zh-CN.jpg)

