# RDS for SQL Server如何修改schema为dbo {#concept_186267 .concept}

## 问题现象 {#section_qok_7em_93t .section}

RDS for SQL Server在使用过程中，经常遇到schema为非dbo的情况，导致使用`select * from <表名>`报错，提示对象名无效。

![报错信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8333/155564259344895_zh-CN.png)

## 原因 {#section_84g_l4h_liu .section}

查看该表的相关信息，命令如下：

``` {#codeblock_x8f_bza_esq}
SELECT a.name schemaName,b.name tableName,b.type_desc FROM sys.schemas a , sys.tables b
WHERE a.schema_id = b.schema_id
```

![查看表信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8333/155564259344897_zh-CN.png)

可以看到schema不是dbo，导致问题出现。

## 解决方案 {#section_to0_r7b_hhx .section}

-   **修改单个表的schema** 

    命令如下：

    ``` {#codeblock_hzr_fj7_clq}
    ALTER SCHEMA dbo TRANSFER test.kkk
    ```

-   **批量修改表的schema** 

    命令如下：

    ``` {#codeblock_my7_la5_04e}
    exec sp_msforeachtable 'alter schema dbo transfer ?'
    ```


