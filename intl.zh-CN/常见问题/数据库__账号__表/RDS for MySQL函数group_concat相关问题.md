# RDS for MySQL函数group\_concat相关问题 {#concept_265010 .concept}

## group\_concat返回结果的长度 {#section_teo_v9e_onu .section}

函数group\_concat返回结果的长度受参数**group\_concat\_max\_len**控制，默认值为1024，即默认返回1024字节长度结果。

|参数名称|默认值|取值范围|说明|
|----|---|----|--|
|group\_concat\_max\_len|1024|4-1844674407370954752|group\_concat函数返回结果的最大长度，单位：Byte。|

**说明：** 您可以设置参数**group\_concat\_max\_len**在全局生效或会话级别生效：

-   全局生效：在控制台的参数设置页面修改。
-   会话级别生效：

    ``` {#codeblock_xpz_9ud_mwx}
    set group_concat_max_len=90; -- 设置当前会话 group_concat_max_len 为 90 字节
    
    show variables like 'group_concat_max_len'; -- 查看当前会话的 group_concat_max_len 值
    
    
    select group_concat(distinct concat_ws(' ', t1.col0, t1.col2, t1.col3, t1.col4) separator "---")
    from grp_con_test t1, grp_con_test t2 \G  -- 查询结果
    
    select length(group_concat(distinct concat_ws(' ', t1.col0, t1.col2, t1.col3, t1.col4) separator "---"))
    from grp_con_test t1, grp_con_test t2 \G  -- 查询结果的长度
    ```

    ![当前会话生效](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8259/155781163447227_zh-CN.png)


## group\_concat\(distinct\) 去除重复数据失效的处理 {#section_dkp_gzh_xpw .section}

**失效原因**

当设置group\_concat\_max\_len为较大值时，使用`group_concat(distinct)`去除结果中的重复数据，会出现失效的情况，例如：

``` {#codeblock_jkq_qkx_aeb}
select group_concat(distinct concat_ws(' ', t1.col0, t1.col2, t1.col3, t1.col4) separator "---")
from grp_con_test t1, grp_con_test t2 \G -- 查询结果
```

![数据重复](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8259/155781163447229_zh-CN.png)

可以看到，结果中出现了多个重复值。出现这个问题的原因当group\_concat返回结果集比较大，会出现内存临时表无法承载全部结果集数据，进而会使用磁盘临时表；而group\_concat在使用磁盘临时表时会触发[BUG](https://bugs.mysql.com/bug.php?spm=a2c4g.11186623.2.21.52d5173e1MUH17&id=68145)导致无法去除重复数据。

**解决方法**

调整tmp\_table\_size参数设置，增大内存临时表的最大尺寸，命令如下：

``` {#codeblock_iaq_pbe_q0p}
set tmp_table_size=1*1024*1024 -- 设置当前会话 tmp_table_size 为 1 MB
show variables like 'tmp_table_size' -- 查看当前会话 tmp_table_size 的设置
select group_concat(distinct concat_ws(' ', t1.col0, t1.col2, t1.col3, t1.col4) separator "---")
from grp_con_test t1, grp_con_test t2 \G
```

**说明：** 也可以在控制台的参数设置页面修改参数**tmp\_table\_size**。

## group\_concat和concat结合使用返回异常 {#section_1nn_lr7_0u3 .section}

**异常原因**

group\_concat和concat结合使用某些情况下会出现返回BLOB字段类型的情况，例如：

``` {#codeblock_uep_7v3_w37}
select concat('{' ,group_concat(concat('\"payMoney' ,t.signature ,'\":' ,ifnull(t.money,0))) ,'}') payType
from my_money t
where cash_id='989898989898998898'
group by cash_id;
```

![返回BLOB字段](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8259/155781163447230_zh-CN.png)

这是由于函数concat按字节返回结果，如果concat的输入有多种类型，其结果是不可预期的。

**解决方法**

通过cast函数进行约束，为concat返回结果为字符串类型，将上面例子修改为：

``` {#codeblock_hez_hj3_zx5}
select concat('{' ,cast(group_concat(concat('\"payMoney' ,t.signature ,'\":' ,ifnull(t.money,0))) as char) ,'}') payType
from my_money y t
where cash_id='989898989898998898'
group by cash_id;
```

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8259/155781163447232_zh-CN.png)

