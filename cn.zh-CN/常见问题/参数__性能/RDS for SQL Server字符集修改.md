# RDS for SQL Server字符集修改 {#concept_ztm_4jt_jhb .concept}

## RDS for SQL Server控制台支持的字符集 {#section_vzr_2c5_jhb .section}

-   Chinese\_PRC\_CI\_AS
-   Chinese\_PRC\_CS\_AS
-   SQL\_Latin1\_General\_CP1\_CI\_AS
-   SQL\_Latin1\_General\_CP1\_CS\_AS
-   Chinese\_PRC\_BIN

**说明：** 后缀说明：

-   \_CI：不分区大小写。
-   \_CS：区分大小写。
-   \_BIN：按二进制排序，区分大小写。

## **修改表的字符集** {#section_ppy_cd5_jhb .section}

RDS for SQL Server不支持修改数据库级别字符集，只支持修改表中列的字符集。SQL如下：

```
alter table <表名> alter column <列名> <列数据类型> collate <字符集>
```

**示例**

```
alter table test2 alter column name varchar(10) collate Chinese_PRC_CI_AS
```

## 字符集导致的查询错误 {#section_cjs_4d5_jhb .section}

![字符集不匹配](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8335/155496162144239_zh-CN.png)

**原因**

由于列的字符集不同，导致查询失败。

**解决方案**

可以修改表的字符集保持一致，或者查询时指定字符集，SQL如下：

```
select * from test1 a ,test2 b where a.name=b.name collate Chinese_PRC_CI_AS
```

