# RDS for MySQL为无主键表添加主键 {#concept_1495870 .concept}

本文介绍RDS for MySQL的表在没有主键时如何添加主键。

## 查看无主键表 {#section_0jf_2ft_qik .section}

执行如下命令查看是否有无主键表：

``` {#codeblock_0jo_r34_d7r}
select table_schema,table_name from information_schema.tables
where (table_schema,table_name) not in(
    select distinct table_schema,table_name from information_schema.columns where COLUMN_KEY='PRI'
)
and table_schema not in (
    'sys','mysql','information_schema','performance_schema'
);
```

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1188469/156473669254218_zh-CN.png)

## 解决方法 {#section_qos_ojt_3sj .section}

-   添加隐式主键
    1.  使用如下命令查看参数**implicit\_primary\_key**的值是否为**ON**。

        ``` {#codeblock_4mx_y57_zx1}
        show global variables  like 'implicit_primary_key';
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1188469/156473669254222_zh-CN.png)

        **说明：** 如果查询没有该参数或值为**OFF**，请您提交工单进行修改。

    2.  执行如下命令修改无主键表：

        ``` {#codeblock_6gz_ym4_iau}
        alter table <表名> engine=innodb;
        ```

        **说明：** 

        -   执行过程中会禁止数据写入表，但是仍然可以读取。
        -   当**implicit\_primary\_key**为**ON**时，修改表的引擎会自动添加隐式主键。
-   直接添加主键

    执行如下命令为无主键表添加主键：

    ``` {#codeblock_gi2_o2n_7mb}
    ALTER TABLE <表名> ADD PRIMARY KEY (<需要设为主键的列名>);
    ```


