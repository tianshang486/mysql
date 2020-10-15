# 设置PostgreSQL排序规则（Collation）

初始化数据库集群时，可以设置数据库的字符串排序、字符归类方法、数值格式、日期格式、时间格式、货币格式等。另外，为了支持国际化，数据库通常会涉及到LC\_COLLATE和LC\_CTYPE的概念。

|LC\_COLLATE|String sort order|
|-----------|-----------------|
|LC\_CTYPE|字符分类|
|LC\_MESSAGES|消息的语言|
|LC\_MONETARY|货币使用的格式|
|LC\_NUMERIC|数字使用的格式|
|LC\_TIME|时间日期使用的格式|

您可以利用这些特性，按本土化需求，输出对应的顺序或者格式。本文将通过示例介绍如何设置数据库的本土化信息以及如何设置输出结果按中文的拼音顺序进行排序。

## PostgreSQL 支持的字符集类型

您可以通过[PostgreSQL 的官方文档](https://www.postgresql.org/docs/9.6/static/multibyte.html)``

|Name|Description|Language|Server|Bytes/Char|Aliases|
|----|-----------|--------|------|----------|-------|
|BIG5|Big Five|Traditional Chinese|No|1月2日|WIN950, Windows950|
|EUC\_CN|Extended UNIX Code-CN|Simplified Chinese|Yes|1月3日|-|
|EUC\_JP|Extended UNIX Code-JP|Japanese|Yes|1月3日|-|
|EUC\_JIS\_2004|Extended UNIX Code-JP, JIS X 0213|Japanese|Yes|1月3日|-|
|EUC\_KR|Extended UNIX Code-KR|Korean|Yes|1月3日|-|
|EUC\_TW|Extended UNIX Code-TW|Traditional Chinese, Taiwanese|Yes|1月3日|-|
|GB18030|National Standard|Chinese|No|1月4日|-|
|GBK|Extended National Standard|Simplified Chinese|No|1月2日|WIN936, Windows936|
|ISO\_8859\_5|ISO 8859-5, ECMA 113|Latin/Cyrillic|Yes|1|-|
|ISO\_8859\_6|ISO 8859-6, ECMA 114|Latin/Arabic|Yes|1|-|
|ISO\_8859\_7|ISO 8859-7, ECMA 118|Latin/Greek|Yes|1|-|
|ISO\_8859\_8|ISO 8859-8, ECMA 121|Latin/Hebrew|Yes|1|-|
|JOHAB|JOHAB|Korean \(Hangul\)|No|1月3日|-|
|KOI8R|KOI8-R|Cyrillic \(Russian\)|Yes|1|KOI8|
|KOI8U|KOI8-U|Cyrillic \(Ukrainian\)|Yes|1|-|
|LATIN1|ISO 8859-1, ECMA 94|Western European|Yes|1|ISO88591|
|LATIN2|ISO 8859-2, ECMA 94|Central European|Yes|1|ISO88592|
|LATIN3|ISO 8859-3, ECMA 94|South European|Yes|1|ISO88593|
|LATIN4|ISO 8859-4, ECMA 94|North European|Yes|1|ISO88594|
|LATIN5|ISO 8859-9, ECMA 128|Turkish|Yes|1|ISO88599|
|LATIN6|ISO 8859-10, ECMA 144|Nordic|Yes|1|ISO885910|
|LATIN7|ISO 8859-13|Baltic|Yes|1|ISO885913|
|LATIN8|ISO 8859-14|Celtic|Yes|1|ISO885914|
|LATIN9|ISO 8859-15|LATIN1 with Euro and accents|Yes|1|ISO885915|
|LATIN10|ISO 8859-16, ASRO SR 14111|Romanian|Yes|1|ISO885916|
|MULE\_INTERNAL|Mule internal code|Multilingual Emacs|Yes|1月4日|-|
|SJIS|Shift JIS|Japanese|No|1月2日|Mskanji, ShiftJIS, WIN932, Windows932|
|SHIFT\_JIS\_2004|Shift JIS, JIS X 0213|Japanese|No|1月2日|-|
|SQL\_ASCII|unspecified \(see text\)|any|Yes|1|-|
|UHC|Unified Hangul Code|Korean|No|1月2日|WIN949, Windows949|
|UTF8|Unicode, 8-bit|all|Yes|1月4日|Unicode|
|WIN866|Windows CP866|Cyrillic|Yes|1|ALT|
|WIN874|Windows CP874|Thai|Yes|1|-|
|WIN1250|Windows CP1250|Central European|Yes|1|-|
|WIN1251|Windows CP1251|Cyrillic|Yes|1|WIN|
|WIN1252|Windows CP1252|Western European|Yes|1|-|
|WIN1253|Windows CP1253|Greek|Yes|1|-|
|WIN1254|Windows CP1254|Turkish|Yes|1|-|
|WIN1255|Windows CP1255|Hebrew|Yes|1|-|
|WIN1256|Windows CP1256|Arabic|Yes|1|-|
|WIN1257|Windows CP1257|Baltic|Yes|1|-|
|WIN1258|Windows CP1258|Vietnamese|Yes|1|ABC, TCVN, TCVN5712, VSCII|

## 查询字符集支持的LC\_COLLATE和LC\_CTYPE信息

您可以使用如下SQL查询系统表pg\_collation，来获取字符集支持的LC\_COLLATE和LC\_CTYPE信息。

```
test=> select pg_encoding_to_char(collencoding) as encoding,collname,collcollate,collctype from pg_collation ;
```

返回结果如下所示，encoding为空时，表示这个collation支持所有的字符集。

```
  encoding  |       collname        |      collcollate      |       collctype
------------+-----------------------+-----------------------+-----------------------
            | default               |                       |
            | C                     | C                     | C
            | POSIX                 | POSIX                 | POSIX
 UTF8       | aa_DJ                 | aa_DJ.utf8            | aa_DJ.utf8
 LATIN1     | aa_DJ                 | aa_DJ                 | aa_DJ
 LATIN1     | aa_DJ.iso88591        | aa_DJ.iso88591        | aa_DJ.iso88591
 UTF8       | aa_DJ.utf8            | aa_DJ.utf8            | aa_DJ.utf8
 UTF8       | aa_ER                 | aa_ER                 | aa_ER
 UTF8       | aa_ER.utf8            | aa_ER.utf8            | aa_ER.utf8
.......
 EUC_CN     | zh_CN                 | zh_CN                 | zh_CN
 UTF8       | zh_CN                 | zh_CN.utf8            | zh_CN.utf8
 EUC_CN     | zh_CN.gb2312          | zh_CN.gb2312          | zh_CN.gb2312
 UTF8       | zh_CN.utf8            | zh_CN.utf8            | zh_CN.utf8
 UTF8       | zh_HK                 | zh_HK.utf8            | zh_HK.utf8
 UTF8       | zh_HK.utf8            | zh_HK.utf8            | zh_HK.utf8
 EUC_CN     | zh_SG                 | zh_SG                 | zh_SG
 UTF8       | zh_SG                 | zh_SG.utf8            | zh_SG.utf8
 EUC_CN     | zh_SG.gb2312          | zh_SG.gb2312          | zh_SG.gb2312
 UTF8       | zh_SG.utf8            | zh_SG.utf8            | zh_SG.utf8
 EUC_TW     | zh_TW                 | zh_TW.euctw           | zh_TW.euctw
 UTF8       | zh_TW                 | zh_TW.utf8            | zh_TW.utf8
 EUC_TW     | zh_TW.euctw           | zh_TW.euctw           | zh_TW.euctw
 UTF8       | zh_TW.utf8            | zh_TW.utf8            | zh_TW.utf8
 UTF8       | zu_ZA                 | zu_ZA.utf8            | zu_ZA.utf8
 LATIN1     | zu_ZA                 | zu_ZA                 | zu_ZA
 LATIN1     | zu_ZA.iso88591        | zu_ZA.iso88591        | zu_ZA.iso88591
 UTF8       | zu_ZA.utf8            | zu_ZA.utf8            | zu_ZA.utf8
(869 rows)
```

## 设置数据库的本土化（collate）信息

关于如何设置字符集、LC\_COLLATE及LC\_CTYPE的信息，请参见文档[CREATE DATABASE 命令的具体使用方法](~~52949~~)

-   设置字段的本土化

    前提条件

    执行如下SQL命令，查询当前数据库的字符集（encoding）类型，并了解清楚与您当前数据库字符集兼容的collate。

    ```
    postgres=# select datname,pg_encoding_to_char(encoding) as encoding from pg_database;
    ```

    返回结果如下所示：

    ```
          datname       | encoding
    --------------------+-----------
     template1          | UTF8
     template0          | UTF8
     db                 | SQL_ASCII
     db1                | EUC_CN
     contrib_regression | UTF8
     test01             | UTF8
     test02             | UTF8
     postgres           | UTF8
    (8 rows)
    ```

    操作步骤

    1.  在创建表时，执行如下命令，指定兼容当前字符集的collate。

        ```
        CREATE TABLE test1 (
         a text COLLATE "de_DE",
         b text COLLATE "es_ES",
         ...
        );
        ```

    2.  执行如下命令，修改列collate。

        **说明：** 修改列collate时，会导致rewrite table，大表请谨慎操作。

        ```
        alter table a alter c1 type text COLLATE "zh_CN";
        ```

-   在SQL使用本土化
    -   使用本土化，改变order by输出排序。命令如下：

        ```
        test=# select * from a order by c1 collate "C";  
        ```

        输出结果如下：

        ```
             c1
          --------
           刘少奇
           刘德华
          (2 rows)
          test=# select * from a order by c1 collate "zh_CN";
             c1
          --------
           刘德华
           刘少奇
          (2 rows)
        ```

    -   使用本土化，改变操作符的结果。示例如下：

        命令：

        ```
        select * from a where c1 > '刘少奇' collate "C";  
        ```

        输出结果如下：

        ```
             c1
          --------
           刘德华
          (1 row)
        ```

        命令：

        ```
        select * from a where c1 > '刘少奇' collate "zh_CN";
        ```

        输出结果如下：

        ```
           c1
          ----
          (0 rows)
        ```

-   使用本土化索引进行排序

    排序语句中的collate与索引的collate保持一致，才能使用这个索引进行排序。命令如下：

    ```
    create index idxa on a(c1 collate "zh_CN");  
    explain select * from a order by c1 collate "zh_CN";                      
    ```

    输出结果如下：

    ```
                                   QUERY PLAN
    ------------------------------------------------------------------------
     Index Only Scan using idxa on a  (cost=0.15..31.55 rows=1360 width=64)
    (1 row)
    ```


## 设置输出结果按拼音排序

您可以通过如下四种方法来设置按拼音排序：

-   使用本土化 SQL。该方法不修改原有数据。命令如下：

    ```
    select * from a order by c1 collate "zh_CN";  
    ```

    输出结果如下：

    ```
         c1
      --------
       刘德华
       刘少奇
      (2 rows)
    ```

-   使用本土化字段。若已有数据，使用该方法时需要调整原有数据。命令如下：

    ```
    alter table a alter c1 type text COLLATE "zh_CN";
    ```

-   使用本土化索引以及本土化 SQL。该方法不修改原有数据。命令如下：

    ```
    create index idxa on a(c1 collate "zh_CN");  
    explain select * from a order by c1 collate "zh_CN";  
    ```

    输出结果如下：

    ```
                                     QUERY PLAN
      ------------------------------------------------------------------------
       Index Only Scan using idxa on a  (cost=0.15..31.55 rows=1360 width=64)
      (1 row)
    ```

-   将数据库的collate设置为zh\_CN，数据会将默认使用这个collate按拼音排序。命令如下：

    ```
    create database test03 encoding 'UTF8' lc_collate 'zh_CN.utf8' lc_ctype 'zh_CN.utf8'  template template0;
    \c test03
    select * from (values ('刘德华'),('刘少奇')) as a(c1) order by c1 ; 
    ```

    输出结果如下：

    ```
         c1
      --------
       刘德华
       刘少奇
      (2 rows)
    ```

    **说明：** 在设置按拼音排序时，要注意多音字。例如重庆（chongqing），在编码时，重可能会按照zhong编码，影响输出。


## 在Greenplum中设置输出结果按拼音排序

Greenplum不支持单列设置collate，按拼音排序有些许不同。

在Greenplum中，可以使用字符集转换，按对应二进制排序，得到拼音排序的效果，如下面的命令所示：

```
select * from (values ('刘德华'), ('刘少奇')) t(id) order by byteain(textout(convert(id,'UTF8','EUC_CN')));
```

输出结果如下：

```
   id
--------
 刘德华
 刘少奇
(2 rows)
```

## 参考文档

-   [CREATE DATABASE命令的具体使用方法](~~52949~~)
-   [PostgreSQL 9.6.2 Documentation — Chapter 23. Localization](https://www.postgresql.org/docs/9.6/static/charset.html?spm=a2c4g.11186623.2.20.9cc1410c3pXuZx)

