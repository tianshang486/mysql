# PostgreSQL/PPAS磁盘空间占用剧增后下降情况解析 {#concept_upv_wfn_hhb .concept}

## 情况一 {#section_inm_jhn_hhb .section}

**原因**

大量更新导致日志剧增，来不及归档和删除，占用了磁盘空间。

**解决方案**

提高实例的磁盘空间容量或降低更新频率。

## 情况二 {#section_xbn_jhn_hhb .section}

**原因**

查询操作含有大数据量的排序、连接等操作，处理过程中产生临时表并溢出到磁盘，短时间内造成大量空间占用。

**解决方案**

-   对于PostgreSQL用户，通过RDS初始帐号执行如下命令：

    ```
    alter role all set temp_file_limit = <临时表空间上限>;
    ```

-   对于PPAS用户，通过RDS初始帐号执行如下命令：

    ```
    select rds_set_conf_for_all_roles('temp_file_limit', '<临时表空间上限>');
    ```


**说明：** 以上命令用于指定每个查询可以使用的临时表空间上限（单位为KB），执行成功后，单个查询生成的临时表空间达到上限就会报错。这样就能及时发现有问题的SQL语句，并避免磁盘空间被占满。

**示例**

```
alter role all set temp_file_limit = 512000;
```

```
select rds_set_conf_for_all_roles('temp_file_limit', '512000');
```

