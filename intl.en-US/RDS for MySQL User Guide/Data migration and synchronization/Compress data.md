# Compress data {#concept_hhr_wzv_ydb .concept}

RDS for MySQL 5.6 allows you to compress data by using the TokuDB storage engine. Tests show that, after data tables are migrated from the InnoDB to TokuDB storage engines, the data volume can be reduced by 80% to 90%. That is, 2 TB of data can be compressed to 400 GB or even lower. Additionally, the TokuDB storage engine supports transactions and online DDL operations to maintain better compatibility with the applications that run on a MyISAM or InnoDB storage engine.

## Limits {#section_gfv_jbw_ydb .section}

-   The TokuDB storage engine does not support foreign keys.
-   The TokuDB storage engine is not applicable when a large volume of data is frequently read.

## Procedure {#section_r4k_lbw_ydb .section}

1.  Run the following command to check the MySQL version of your RDS instance:

    ``` {#codeblock_70j_dos_sq0}
    SELECT version();
    ```

    **Note:** Currently, only MySQL 5.6 supports the TokuDB storage engine. If you use the MySQL 5.1 or 5.5 database engine, then you must upgrade it to MySQL 5.6 before data compression.

2.  Set the loose\_tokudb\_buffer\_pool\_ratio parameter, which indicates the proportion of cache shared between TokuDB and InnoDB as occupied by TokuDB in all the shared cache.

    ``` {#codeblock_jp1_jsh_85a}
    select sum(data_length) into @all_size from information_schema.tables where engine='innodb';
    select sum(data_length) into @change_size from information_schema.tables where engine='innodb' and concat(table_schema, '.', table_name) in ('XX.XXXX', 'XX.XXXX', 'XX.XXXX');    
    select round(@change_size/@all_size*100);
    ```

    In the preceding code, XX.XXXX indicates the names of the database and table that you want to migrate to the TokuDB storage engine.

3.  Restart your RDS instance.

    For more information, see [Restart an RDS instance](intl.en-US/RDS for MySQL User Guide/Instance management/Restart an RDS instance.md#).

4.  Modify the storage engine.

    ``` {#codeblock_vme_ze9_2yw}
    ALTER TABLE XX.XXXX ENGINE=TokuDB
    ```

    In the preceding code, XX.XXXX indicates the name of the database and table that you want to migrate to the TokuDB storage engine.


