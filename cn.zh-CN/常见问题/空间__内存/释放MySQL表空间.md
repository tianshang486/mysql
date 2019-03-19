# 释放MySQL表空间 {#concept_atj_hld_n2b .concept}

MySQL可以通过`optimize table`命令释放表空间，重组表数据和索引的物理页，减少所占空间和优化读写性能。

如果使用`delete`命令删除数据库，表空间不会直接回收，您可以用`optimize table`释放表空间。

## 注意事项 {#section_klc_q4c_dhb .section}

-   操作将会锁表，建议在业务低峰期操作。
-   仅Innodb和MyISAM引擎支持`optimize table`命令。

## 通过命令行操作 {#section_agq_y4c_dhb .section}

1.  [使用通用客户端连接MySQL数据库](../../../../../intl.zh-CN/RDS for MySQL 快速入门/连接MySQL实例.md#)，本文以MySQL-Front为例进行演示。
2.  在右侧选择SQL编辑器页签。
3.  在命令行中执行如下命令释放表空间：

    ```
    optimize table <数据库名1>.<表名1>,<数据库名2>.<表名2>
    ```

    ![mysql-front](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8253/155296082240992_zh-CN.png)


