# The maximum column size is 767 bytes错误处理 {#concept_185603 .concept}

## 错误信息 {#section_g08_ggz_00a .section}

RDS for MySQL在大字段上创建索引时，有时会遇到以下错误：

``` {#codeblock_2bd_svf_l1n}
ERROR 1709 (HY000): Index column size too large. The maximum column size is 767 bytes.
```

## 错误原因 {#section_alw_8nu_ar2 .section}

由于MySQL的Innodb引擎表索引字段长度的限制为767字节，因此对于多字节字符集的大字段或者多字段组合，创建索引时会出现此错误。

以utf8mb4字符集字符串类型字段为例，utf8mb4是4字节字符集，则默认支持的索引字段最大长度是191字符（767字节/4字节每字符≈191字符），因此在varchar\(255\)或char\(255\)类型字段上创建索引会失败。详情请参见[MySQL官网文档](https://dev.mysql.com/doc/refman/5.6/en/charset-unicode-utf8mb4.html)。

## 解决方案 {#section_pie_s6p_5il .section}

1.  在控制台的参数设置里修改参数**innodb\_large\_prefix**为ON或者1，然后单击**提交参数**。

    ![innodb_large_prefix](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8279/155548092544664_zh-CN.png)

    **说明：** 将**innodb\_large\_prefix**修改为ON或者1后，对于Dynamic和Compressed格式的InnoDB引擎表，其最大的索引字段长度支持到3072字节。

2.  创建表的时候指定表的row format格式为Dynamic或者Compressed，示例如下：

    ``` {#codeblock_ktp_j86_w14}
    create table idx_length_test_02
    (
      id int auto_increment primary key,
      name varchar(255)
    ) 
    ROW_FORMAT=DYNAMIC default charset utf8mb4;
    ```

    **说明：** 对已经创建的表，修改表的row\_format格式命令如下：

    ``` {#codeblock_yxg_gt9_s7m}
    alter table <表名> row_format=dynamic;
    alter table <表名> row_format=compressed;
    ```


