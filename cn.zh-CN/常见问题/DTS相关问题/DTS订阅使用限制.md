# DTS订阅使用限制 {#concept_187592 .concept}

DTS提供的数据订阅功能意在帮助用户实时获取RDS增量数据，实现数据分析、消息转发及本地灾备等功能。目前DTS支持的RDS for MySQL订阅功能存在一定的限制，具体限制如下：

-   MySQL 5.6的binlog\_row\_image格式必须为FULL。
-   MySQL存储引擎只支持Innodb。
-   MySQL字符集只支持latin1、latin2、gbk、utf8、utf8mb4和binary。

