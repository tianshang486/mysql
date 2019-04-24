# MySQL在DMS新增视图时算法的含义 {#concept_188044 .concept}

DMS中新建视图，或在现有视图上，会看到算法一栏，如下图。

![DMS视图算法](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8412/155608753945289_zh-CN.png)

这三项的含义如下：

-   **UNDEFINED**：MySQL将自行选择所要使用的算法。它倾向于MERGE而不是TEMPTABLE，这是因为MERGE通常更有效，而且如果使用了TEMPTABLE，视图是不可更新的。
-   **MERGE**：会将引用视图的语句的文本与视图定义合并起来，使得视图定义的某一部分取代语句的对应部分。
-   **TEMPTABLE**：视图的结果将被置于临时表中，然后使用它执行语句。

