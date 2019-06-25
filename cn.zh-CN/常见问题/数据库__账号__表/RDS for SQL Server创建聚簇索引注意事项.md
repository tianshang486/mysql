# RDS for SQL Server创建聚簇索引注意事项 {#concept_266536 .concept}

## 一个表只能创建一个聚簇索引 {#section_tn7_zpy_2oy .section}

如果已创建聚簇索引，再次创建会失败，报错如下。

![重复创建报错](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8390/156144806047471_zh-CN.png)

## 使用sp\_helpindex查看索引 {#section_4ze_jyu_g6p .section}

命令如下：

``` {#codeblock_7ca_7zg_awg}
ues  <数据库名>
go
sp_helpindex '<表名>'
```

## 使用drop index删除聚簇索引 {#section_hmh_ifl_txf .section}

命令如下：

``` {#codeblock_7dj_bbe_hjc}
DROP INDEX <索引名> ON <数据库名>.<表名>
```

## 重新计算统计信息 {#section_0wu_ntv_0wk .section}

统计信息指的是创建索引时的STATISTICS\_NORECOMPUTE选项。一般来说都需要重新计算，详情请参见[CREATE INDEX](https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2008-r2/ms188783(v=sql.105))。

**说明：** STATISTICS\_NORECOMPUTE的默认值是OFF，即需要重新计算（因为该选项本身就是否定的意思）。

