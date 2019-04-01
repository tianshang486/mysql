# RDS for MySQL表分区的限制 {#concept_rzy_2tz_ghb .concept}

RDS for MySQL对表分区有以下限制：

-   只能对数据表的整型列进行分区，或者数据列可以通过分区函数转化成整型列。
-   最大分区数目不能超过1024。
-   如果含有唯一索引或者主键，则分区列必须包含在所有的唯一索引或者主键在内。
-   不支持外键。
-   不支持全文索引（FULL TEXT）。

如果问题还未能解决，请联系[售后技术支持](https://selfservice.console.aliyun.com/ticket/createIndex.htm)。

