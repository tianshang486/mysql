# Caused By: ERROR: syntax error at end of input错误处理 {#concept_186351 .concept}

## 错误信息 {#section_qia_5s6_py5 .section}

使用JDBC访问RDS for PPAS时出现如下报错：

``` {#codeblock_irq_c2k_czu}
CREATE OR REPLACE PACKAGE package_name
IS
PROCEDURE pro_name1 ();
PROCEDURE pro_name2 ();
PROCEDURE pro_name3 ();
END package_name;
[ERROR] Caused By: ERROR: syntax error at end of input
[ERROR] Position: xxx
```

## 解决方案 {#section_eot_kt8_zl8 .section}

1.  确认以上语法通过命令行交互式客户端工具psql是否可以执行成功，如果执行不成功，请检查语法问题。
2.  如果不是语法问题，请确认当前正在使用的JDBC驱动，如果使用的是PostgreSQL的JDBC也会触发此问题，这是由于使用的是Oracle语法，应该使用edb-jdbc驱动。

下载PPAS专用的JDBC驱动请通过此链接：[PPAS开发驱动程序](../../../../cn.zh-CN/RDS for PPAS 快速入门/附录/附录：PPAS 开发驱动程序.md#)。

**说明：** jdk1.5及以下请用edb-jdbc14.jar，jdk1.6及以上请使用edb-jdbc16.jar。

