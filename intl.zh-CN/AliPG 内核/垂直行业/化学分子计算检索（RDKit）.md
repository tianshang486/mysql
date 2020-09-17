# 化学分子计算检索（RDKit）

RDS PostgreSQL提供RDKit插件，支持化学分子计算、化学分子检索等功能。

实例版本为RDS PostgreSQL 12。

RDKit插件支持mol数据类型（描述分子类型）和fp数据类型（描述分子指纹），在此基础上支持比较运算、相似度计算（Tanimoto、Dice）和GiST索引。

更多RDKit插件SQL操作请参见[RDKit SQL](https://github.com/rdkit/rdkit/tree/master/Code/PgSQL/rdkit/sql)。

## 注意事项

-   mol数据类型的输入、输出函数遵循简化分子线性输入规范（SMILES）。
-   fp数据类型的输入、输出功能遵循bytea（存储二进制数据的字段类型）格式。

## 创建插件

```
postgres=# create extension rdkit ;
CREATE EXTENSION
```

## 默认参数配置

```
postgres=# show rdkit.tanimoto_threshold ;
 rdkit.tanimoto_threshold 
--------------------------
 0.5
(1 row)

postgres=# show rdkit.dice_threshold;
 rdkit.dice_threshold 
----------------------
 0.5
(1 row)
```

## 索引支持

-   mol和fp的比较运算操作支持Btree索引、Hash索引。例如：

    ```
    CREATE INDEX molidx ON pgmol (mol);
    CREATE INDEX molidx ON pgmol (fp);
    ```

-   mol的`%`、`#`、`@>`、`<@`操作和fp结构的`%`、`#`操作支持Gist索引。例如：

    ```
    CREATE INDEX molidx ON pgmol USING gist (mol);
    ```


## 函数示例

-   tanimoto\_sml函数计算tanimoto相似度。

    ```
    postgres=# \df tanimoto_sml
                               List of functions
     Schema |     Name     | Result data type | Argument data types | Type 
    --------+--------------+------------------+---------------------+------
     public | tanimoto_sml | double precision | bfp, bfp            | func
     public | tanimoto_sml | double precision | sfp, sfp            | func
    (2 rows)
    ```

-   dice\_sml函数计算dice相似度。

    ```
    postgres=# \df dice_sml
                             List of functions
     Schema |   Name   | Result data type | Argument data types | Type 
    --------+----------+------------------+---------------------+------
     public | dice_sml | double precision | bfp, bfp            | func
     public | dice_sml | double precision | sfp, sfp            | func
    (2 rows)
    ```

-   substruct函数，当函数的第二个参数是第一个参数的子结构时，函数返回结果为TRUE。

    ```
    postgres=# \df substruct
                             List of functions
     Schema |   Name    | Result data type | Argument data types | Type 
    --------+-----------+------------------+---------------------+------
     public | substruct | boolean          | mol, mol            | func
     public | substruct | boolean          | mol, qmol           | func
     public | substruct | boolean          | reaction, reaction  | func
    (3 rows)
    ```


## 基础操作说明

-   `mol % mol`、`fp % fp`

    当Tanimoto相似度计算结果小于GUC配置参数rdkit.tanimoto\_threshold时，该操作返回结果为TRUE。

-   `mol # mol`、`fp # fp`

    当Dice相似度计算结果小于GUC配置参数rdkit.dice\_threshold时，该操作返回结果为TRUE。

-   `mol @> mol`

    如果操作符`@>`左边对象包含右边对象，该操作返回结果为TRUE。

-   `mol <@ mol`

    如果操作符`<@`右边对象包含左边对象，该操作返回结果为TRUE。


