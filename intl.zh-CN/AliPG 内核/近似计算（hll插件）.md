# 近似计算（hll插件）

hll插件支持的数据类型HyperLogLog可以帮助您快速预估PV、UV等业务指标。

实例版本如下：

-   PostgreSQL 12（内核小版本20200421及以上）
-   PostgreSQL 11（内核小版本20200402及以上）

**说明：** 您可以在基本信息页面的**配置信息**区域查看是否有**升级内核小版本**按钮。如果有按钮，您可以单击按钮查看当前版本；如果没有按钮，表示已经是最新版。详情请参见[升级内核小版本](/intl.zh-CN/RDS PostgreSQL 数据库/实例/升级内核小版本.md)。

![pgsql升级内核](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/4919259951/p101917.png)

hll插件支持一种可变长、类似集合的数据类型HyperLogLog（hll），常用于在指定精度下返回近似的distinct值，例如1280字节的hll数据类型可以高精度地估计出近百亿的distinct值。hll适合互联网广告分析或其他有类似预估分析计算需求的行业，可以快速预估PV、UV等业务指标。

更多hll插件使用方法请参见[postgresql-hll](https://github.com/citusdata/postgresql-hll)。

详细算法说明请参见论文[HyperLogLog: the analysis of a near-optimalcardinality estimation algorithm](http://algo.inria.fr/flajolet/Publications/FlFuGaMe07.pdf)。

## 创建hll插件

连接实例后创建hll插件，命令如下：

```
CREATE EXTENSION hll;
```

## 基础操作

-   创建一个含有hll字段的表，命令如下：

    ```
    create table agg (id int primary key,userids hll);
    ```

-   将int数据类型转换为hll\_hashval，命令如下：

    ```
    select 1::hll_hashval;
    ```


## 基本操作符

-   hll类型支持如下操作符：

    -   =
    -   !=
    -   <\>
    -   \|\|
    -   \#
    示例如下：

    ```
    select hll_add_agg(1::hll_hashval) = hll_add_agg(2::hll_hashval);
    select hll_add_agg(1::hll_hashval) || hll_add_agg(2::hll_hashval);
    select #hll_add_agg(1::hll_hashval);
    ```

-   hll\_hashval类型支持如下操作符：

    -   =
    -   !=
    -   <\>
    示例如下：

    ```
    select 1::hll_hashval = 2::hll_hashval;
    select 1::hll_hashval <> 2::hll_hashval;
    ```


## 基本函数

-   支持hll\_hash\_boolean、hll\_hash\_smallint和hll\_hash\_bigint等hash函数，示例如下：

    ```
    select hll_hash_boolean(true);
    select hll_hash_integer(1);
    ```

-   支持hll\_add\_agg函数，可以将int转换为hll格式，示例如下：

    ```
    select hll_add_agg(1::hll_hashval);
    ```

-   支持hll\_union函数，可以将hll并集，示例如下：

    ```
    select hll_union(hll_add_agg(1::hll_hashval),hll_add_agg(2::hll_hashval));
    ```

-   支持hll\_set\_defaults函数，可以设置精度，示例如下：

    ```
    select hll_set_defaults(15,5,-1,1);
    ```

-   支持hll\_print函数，用于打印debug信息，示例如下：

    ```
    select hll_print(hll_add_agg(1::hll_hashval));
    ```


## 示例

```
create table access_date (acc_date date unique, userids hll);
insert into access_date select current_date, hll_add_agg(hll_hash_integer(user_id)) from generate_series(1,10000) t(user_id);
insert into access_date select current_date-1, hll_add_agg(hll_hash_integer(user_id)) from generate_series(5000,20000) t(user_id);
insert into access_date select current_date-2, hll_add_agg(hll_hash_integer(user_id)) from generate_series(9000,40000) t(user_id);
postgres=# select #userids from access_date where acc_date=current_date;
     ?column?
------------------
 9725.85273370708
(1 row)
postgres=# select #userids from access_date where acc_date=current_date-1;
     ?column?
------------------
 14968.6596883279
(1 row)
postgres=# select #userids from access_date where acc_date=current_date-2;
     ?column?
------------------
 29361.5209149911
(1 row)
```

