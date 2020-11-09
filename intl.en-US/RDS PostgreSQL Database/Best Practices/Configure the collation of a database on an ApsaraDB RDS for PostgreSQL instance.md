# Configure the collation of a database on an ApsaraDB RDS for PostgreSQL instance

When you initialize an ApsaraDB RDS for PostgreSQL instance, you can configure the collation of each database based on your business requirements. The collation includes the string sort order, character classification method, numeric value format, date and time format, and currency format. In addition, you may also need to configure the LC\_COLLATE and LC\_CTYPE environment variables.

|LC\_COLLATE|String sort order|
|-----------|-----------------|
|LC\_CTYPE|Character classification|
|LC\_MESSAGES|Message language|
|LC\_MONETARY|Currency format|
|LC\_NUMERIC|Numeric value format|
|LC\_TIME|Date and time format|

You can configure these environment variables to specify a collation that meets your business requirements in a locale.

## Supported character sets

For more information, see [Character Set Support](https://www.postgresql.org/docs/9.6/static/multibyte.html)``.

|Name|Description|Language|Server|Bytes/Char|Aliases|
|----|-----------|--------|------|----------|-------|
|BIG5|Big Five|Traditional Chinese|No|January 2|WIN950, Windows950|
|EUC\_CN|Extended UNIX Code-CN|Simplified Chinese|Yes|January 3|-|
|EUC\_JP|Extended UNIX Code-JP|Japanese|Yes|January 3|-|
|EUC\_JIS\_2004|Extended UNIX Code-JP, JIS X 0213|Japanese|Yes|January 3|-|
|EUC\_KR|Extended UNIX Code-KR|Korean|Yes|January 3|-|
|EUC\_TW|Extended UNIX Code-TW|Traditional Chinese, Taiwanese|Yes|January 3|-|
|GB18030|National Standard|Chinese|No|January 4|-|
|GBK|Extended National Standard|Simplified Chinese|No|January 2|WIN936, Windows936|
|ISO\_8859\_5|ISO 8859-5, ECMA 113|Latin/Cyrillic|Yes|1|-|
|ISO\_8859\_6|ISO 8859-6, ECMA 114|Latin/Arabic|Yes|1|-|
|ISO\_8859\_7|ISO 8859-7, ECMA 118|Latin/Greek|Yes|1|-|
|ISO\_8859\_8|ISO 8859-8, ECMA 121|Latin/Hebrew|Yes|1|-|
|JOHAB|JOHAB|Korean \(Hangul\)|No|January 3|-|
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
|MULE\_INTERNAL|Mule internal code|Multilingual Emacs|Yes|January 4|-|
|SJIS|Shift JIS|Japanese|No|January 2|Mskanji, ShiftJIS, WIN932, Windows932|
|SHIFT\_JIS\_2004|Shift JIS, JIS X 0213|Japanese|No|January 2|-|
|SQL\_ASCII|unspecified \(see text\)|any|Yes|1|-|
|UHC|Unified Hangul Code|Korean|No|January 2|WIN949, Windows949|
|UTF8|Unicode, 8-bit|all|Yes|January 4|Unicode|
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

## LC\_COLLATE and LC\_CTYPE settings supported by a character set

You can execute the following SQL statement to query the LC\_COLLATE and LC\_CTYPE settings that are supported by a character set from the pg\_collation system table:

```
test=> select pg_encoding_to_char(collencoding) as encoding,collname,collcollate,collctype from pg_collation ;
```

If the encoding field of a collation is empty, the collation supports all character sets.

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

## Configure the collation of a database in a locale

For more information about how to configure the character set and the LC\_COLLATE and LC\_CTYPE environment variables, see [CREATE DATABASE usage instructions](~~52949~~).

-   Configure the fields of a database in a locale

    Prerequisites

    Familiarize yourself with the collations that are supported by the character set of the database. Then, execute the following SQL statement to query the encoding format of the database:

    ```
    postgres=# select datname,pg_encoding_to_char(encoding) as encoding from pg_database;
    ```

    Information similar to the following output is returned:

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

    Procedure

    1.  When you create a table, execute the following SQL statement to specify a collation that is supported by the character set of the database:

        ```
        CREATE TABLE test1 (
         a text COLLATE "de_DE",
         b text COLLATE "es_ES",
         ...
        );
        ```

    2.  Execute the following SQL statement to modify the collation of a column:

        **Note:** When you modify the collation of a column in a table, the table is rewritten. Proceed with caution if the table is large.

        ```
        alter table a alter c1 type text COLLATE "zh_CN";
        ```

-   Configure locale settings.
    -   Execute the following SQL statement to change the sort order that is specified by the ORDER BY clause:

        ```
        test=# select * from a order by c1 collate "C";  
        ```

        Information similar to the following output is returned:

        ```
             c1
          --------
           Tom
           Alice
          (2 rows)
          test=# select * from a order by c1 collate "zh_CN";
             c1
          --------
           Alice
           Tom
          (2 rows)
        ```

    -   Execute the following SQL statement to change the result that is returned from an operator:

        Example 1:

        ```
        select * from a where c1 > 'Tom' collate "C";  
        ```

        Information similar to the following output is returned:

        ```
             c1
          --------
           Alice
          (1 row)
        ```

        Example 2:

        ```
        select * from a where c1 > 'Tom' collate "en_US";
        ```

        Information similar to the following output is returned:

        ```
           c1
          ----
          (0 rows)
        ```

-   Sort data by using locale indexes.

    You can sort data by using an index only when the collation specified in the ORDER BY clause is the same as the collation of the index. Execute the following SQL statement:

    ```
    create index idxa on a(c1 collate "zh_CN");  
    explain select * from a order by c1 collate "zh_CN";                      
    ```

    Information similar to the following output is returned:

    ```
                                   QUERY PLAN
    ------------------------------------------------------------------------
     Index Only Scan using idxa on a  (cost=0.15..31.55 rows=1360 width=64)
    (1 row)
    ```


## Configure a rule to sort results in alphabetical order

You can use one of the following four methods to configure a rule that is used to sort results in alphabetical order:

-   Use the SQL statements that are supported in your locale. This method does not require you to modify the original data. Execute the following SQL statement:

    ```
    select * from a order by c1 collate "zh_CN";  
    ```

    Information similar to the following output is returned:

    ```
         c1
      --------
       Alice
       Tom
      (2 rows)
    ```

-   Use the fields that are supported in your locale. If the database contains data, this method requires you to modify the original data. Execute the following SQL statement:

    ```
    alter table a alter c1 type text COLLATE "zh_CN";
    ```

-   Use the indexes and SQL statements that are supported in your locale. This method does not require you to modify the original data. Execute the following SQL statements:

    ```
    create index idxa on a(c1 collate "zh_CN");  
    explain select * from a order by c1 collate "zh_CN";  
    ```

    Information similar to the following output is returned:

    ```
                                     QUERY PLAN
      ------------------------------------------------------------------------
       Index Only Scan using idxa on a  (cost=0.15..31.55 rows=1360 width=64)
      (1 row)
    ```

-   Set the collation of the database to en\_US. By default, the data in this database is sorted in alphabetical order based on the specified collation. Execute the following SQL statement:

    ```
    create database test03 encoding 'UTF8' lc_collate 'zh_CN.utf8' lc_ctype 'zh_CN.utf8'  template template0;
    \c test03
    select * from (values ('Alice'),('Tom')) as a(c1) order by c1 ; 
    ```

    Information similar to the following output is returned:

    ```
         c1
      --------
       Alice
       Tom
      (2 rows)
    ```

    **Note:** A Chinese character may have more than one pronunciation. For example, the Chongqing city in China may be encoded as the Zhongqing city. Proceed with caution if you want to configure a collation that is used to sort Chinese characters based on pronunciations.


## Configure a rule to sort results in alphabetical order by using Greenplum

Greenplum does not allow you to specify collations for individual columns. Therefore, the sorting of results in alphabetical order is different in Greenplum.

You can use Greenplum to convert results among character sets. Then, you can sort the results in binary order. This allows you to obtain similar results that resemble results in alphabetical order. The following code snippet provides an example:

```
select * from (values ('Alice'), ('Tom')) t(id) order by byteain(textout(convert(id,'UTF8','EUC_CN')));
```

Information similar to the following output is returned:

```
   id
--------
 Alice
 Tom
(2 rows)
```

## References

-   [CREATE DATABASE usage instructions](~~52949~~)
-   [PostgreSQL 9.6.2 Documentation - Chapter 23. Localization](https://www.postgresql.org/docs/9.6/static/charset.html?spm=a2c4g.11186623.2.20.9cc1410c3pXuZx)

