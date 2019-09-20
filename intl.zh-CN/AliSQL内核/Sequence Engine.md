# Sequence Engine {#concept_1697905 .concept}

AliSQL提供了Sequence Engine，简化获取序列值的复杂度。

## Sequence Engine介绍 {#section_0rb_5ph_jjo .section}

在持久化数据库系统中，无论是单节点中的业务主键，还是分布式系统中的全局唯一值，亦或是多系统中的幂等控制，单调递增的唯一值是常见的需求。不同的数据库系统有不同的实现方法，例如MySQL提供的AUTO\_INCREMENT，Oracle、SQL Server提供的SEQUENCE。

在MySQL数据库中，如果业务希望封装唯一值，例如增加日期、用户等信息，使用AUTO\_INCREMENT的方法会带来很大不便，在实际的系统设计中，也存在不同的折中方法：

-   序列值由Application或者Proxy来生成，不过弊端很明显，状态带到应用端会增加扩容和缩容的复杂度。
-   序列值由数据库通过模拟的表来生成，但需要中间件来封装和简化获取唯一值的逻辑。

AliSQL提供了Sequence Engine，通过引擎的设计方法，尽可能地兼容其他数据库的使用方法，简化获取序列值复杂度。

Sequence Engine实现了MySQL存储引擎的设计接口，但底层的数据仍然使用现有的存储引擎，例如InnoDB或者MyISAM来保存持久化数据，兼容现有的第三方工具（例如Xtrabackup），所以Sequence Engine仅仅是一个逻辑引擎。

Sequence Engine通过Sequence Handler接口访问Sequence对象，实现NEXTVAL的滚动、缓存的管理等，最后透传给底层的基表数据引擎，实现最终的数据访问。

## 使用限制 {#section_b93_ytw_omo .section}

-   Sequence不支持子查询和join查询。
-   可以使用`SHOW CREATE TABLE`或者`SHOW CREATE SEQUENCE`来访问Sequence结构，但不能使用`SHOW CREATE SEQUENCE`访问普通表。
-   不支持建表的时候指定Sequence引擎，Sequence表只能通过[创建Sequence](#section_vtj_6nh_09h)的语法来创建。

## 创建Sequence {#section_vtj_6nh_09h .section}

创建Sequence语句如下：

``` {#codeblock_e5j_fiz_ist}
CREATE SEQUENCE [IF NOT EXISTS] schema.sequence_name
   [START WITH <constant>]
   [MINVALUE <constant>]
   [MAXVALUE <constant>]
   [INCREMENT BY <constant>]
   [CACHE <constant> | NOCACHE]
   [CYCLE | NOCYCLE]
  ;
```

参数说明如下。

|参数|说明|
|--|--|
|START|Sequence的起始值。|
|MINVALUE|Sequence的最小值。|
|MAXVALUE|Sequence的最大值。 **说明：** 如果有参数NOCYCLE，到达最大值后会报如下错误：

``` {#codeblock_0f9_v6p_8mi}
ERROR HY000: Sequence 'db.seq' has been run out.
```

 |
|INCREMENT BY|Sequence的步长。|
|CACHE/NOCACHE|缓存的大小，为了性能考虑，可以设置较大的缓存，但如果遇到实例重启，缓存内的值会丢失。|
|CYCLE/NOCYCLE|表示Sequence如果用完了后，是否允许从MINVALUE重新开始。取值： -   CYCLE：允许；
-   NOCYCLE：不允许。

 |

示例：

``` {#codeblock_q2a_4ug_7t1}
create sequence s
       start with 1
       minvalue 1
       maxvalue 9999999
       increment by 1
       cache 20
       cycle;
```

为了兼容MySQL Dump的备份方式，您也可以使用另外一种创建Sequence的方法，即创建Sequence表并插入一行初始记录。示例如下：

``` {#codeblock_wl4_esk_3jc}
CREATE SEQUENCE schema.sequence_name (
  `currval` bigint(21) NOT NULL COMMENT 'current value',
  `nextval` bigint(21) NOT NULL COMMENT 'next value',
  `minvalue` bigint(21) NOT NULL COMMENT 'min value',
  `maxvalue` bigint(21) NOT NULL COMMENT 'max value',
  `start` bigint(21) NOT NULL COMMENT 'start value',
  `increment` bigint(21) NOT NULL COMMENT 'increment value',
  `cache` bigint(21) NOT NULL COMMENT 'cache size',
  `cycle` bigint(21) NOT NULL COMMENT 'cycle state',
  `round` bigint(21) NOT NULL COMMENT 'already how many round'
) ENGINE=InnoDB DEFAULT CHARSET=latin1

INSERT INTO schema.sequence_name VALUES(0,0,1,9223372036854775807,1,1,10000,1,0);
COMMIT;
```

## Sequence表介绍 {#section_fkw_itb_nld .section}

由于Sequence是通过真正的引擎表来保存的，所以通过查询创建语句看到仍然是默认的引擎表。示例如下：

``` {#codeblock_1s5_rqj_06v}
SHOW CREATE [TABLE|SEQUENCE] schema.sequence_name;

CREATE SEQUENCE schema.sequence_name (
  `currval` bigint(21) NOT NULL COMMENT 'current value',
  `nextval` bigint(21) NOT NULL COMMENT 'next value',
  `minvalue` bigint(21) NOT NULL COMMENT 'min value',
  `maxvalue` bigint(21) NOT NULL COMMENT 'max value',
  `start` bigint(21) NOT NULL COMMENT 'start value',
  `increment` bigint(21) NOT NULL COMMENT 'increment value',
  `cache` bigint(21) NOT NULL COMMENT 'cache size',
  `cycle` bigint(21) NOT NULL COMMENT 'cycle state',
  `round` bigint(21) NOT NULL COMMENT 'already how many round'
) ENGINE=InnoDB DEFAULT CHARSET=latin1
```

## 查询语法 {#section_m82_3mj_vbh .section}

Sequence支持的查询语法如下：

``` {#codeblock_jvt_5hq_zrb}
 SELECT [nextval | currval | *] FROM seq;
 SELECT nextval(seq),currval(seq);
 SELECT seq.currval, seq.nextval from dual;
```

