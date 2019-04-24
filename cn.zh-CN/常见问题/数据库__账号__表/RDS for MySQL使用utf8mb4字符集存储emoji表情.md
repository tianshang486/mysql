# RDS for MySQL使用utf8mb4字符集存储emoji表情 {#concept_188097 .concept}

## 基本原则 {#section_q9u_vws_yop .section}

如果要实现存储emoji表情到RDS for MySQL实例，需要客户端、到RDS实例的连接、RDS实例内部三个方面统一使用或者支持utf8mb4字符集。

-   客户端：客户端需要保证输出的字符串的字符集为utf8mb4。
-   应用到RDS实例的连接：支持utf8mb4字符集。以常见的JDBC连接为例，需要使用MySQL Connector/J 5.1.13（含）以上的版本，JDBC的连接串中，建议不配置characterEncoding选项。
-   RDS实例配置：控制台设置参数character\_set\_server为utf8mb4、数据库的字符集为utf8mb4，以及表的字符集为utf8mb4。

    ![RDS实例配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8263/155609295445309_zh-CN.png)

    ![RDS实例配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8263/155609295545310_zh-CN.png)

    ![RDS实例配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8263/155609295545311_zh-CN.png)


## 通过set names命令设置会话字符集 {#section_ngj_3xh_zsj .section}

对于JDBC连接串设置了characterEncoding为utf8，或者做了上述配置仍旧无法正常插入emoji数据的情况，建议在代码中指定连接的字符集为utf8mb4，示例代码如下：

``` {#codeblock_d28_7li_022}
String query = “set names utf8mb4”;
stat.execute(query);
```

