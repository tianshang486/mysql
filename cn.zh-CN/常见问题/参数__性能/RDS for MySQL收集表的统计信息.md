# RDS for MySQL收集表的统计信息 {#concept_qqy_1xf_jhb .concept}

## 什么是统计信息 {#section_uvz_lxf_jhb .section}

RDS for MySQL查询优化器依据表的统计信息计算不同执行计划的代价，因此表上统计信息的准确对查询优化器选取正确的执行计划至关重要。

## 什么情况下需要收集统计信息 {#section_hk1_rxf_jhb .section}

当表上有大量的数据修改时，例如从数据源加载大量数据（ETL）或者大量历史数据归档，建议手动收集下表上的统计信息，以保证查询优化器可以选取最优的执行计划。

## 如何收集统计信息 {#section_igj_sxf_jhb .section}

您可以[连接MySQL实例](../../../../../cn.zh-CN/RDS for MySQL 快速入门/连接MySQL实例.md#)后执行以下命令：

```
analyze table <表名>;
```

**说明：** 执行命令期间将对全表加只读锁，建议在业务低峰期执行。

![收集统计信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8310/155479323143570_zh-CN.png)

