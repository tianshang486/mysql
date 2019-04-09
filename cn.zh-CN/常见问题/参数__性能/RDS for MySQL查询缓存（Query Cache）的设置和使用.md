# RDS for MySQL查询缓存（Query Cache）的设置和使用 {#concept_cxs_yff_1gb .concept}

## 功能和适用范围 {#section_q3l_vlb_wdb .section}

**功能**：

-   降低CPU使用率。
-   降低IOPS使用率（某些情况下）。
-   减少查询响应时间，提高系统的吞吐量。

**适用范围**：

-   表数据修改不频繁、数据较静态。
-   查询（Select）重复度高。
-   查询结果集小于 1 MB。

**说明：** 查询缓存并不一定带来性能上的提升，在某些情况下（比如查询数量大，但重复的查询很少）开启查询缓存会带来性能的下降。

## 原理 {#section_zch_lgf_1gb .section}

RDS for MySQL对来自客户端的查询（Select）进行Hash计算得到该查询的Hash值，通过该Hash值到查询缓存中匹配该查询的结果。

如果匹配（命中），则将查询的结果集直接返回给客户端，不必再解析、执行查询。

如果没有匹配（命中），则将Hash值和结果集保存在查询缓存中，以便以后使用。

查询涉及的任何一个表中数据发生变化，RDS for MySQL将查询缓存中所有与该表相关的查询结果集全部释放（删除）。

## 限制 {#section_r2x_ngf_1gb .section}

-   查询必须严格一致（大小写、空格、使用的数据库、协议版本、字符集等必须一致）才可以命中，否则视为不同查询。
-   不缓存查询中的子查询结果集，仅缓存查询最终结果集。
-   不缓存存储函数（Stored Function）、存储过程（Stored Procedure）、触发器（Trigger）、事件（Event）中的查询。
-   不缓存含有每次执行结果变化的函数的查询，比如now\(\)、curdate\(\)、last\_insert\_id\(\)、rand\(\)等。
-   不缓存对mysql、information\_schema、performance\_schema系统数据库表的查询。
-   不缓存使用临时表的查询。
-   不缓存产生告警（Warnings）的查询。
-   不缓存Select … lock in share mode、Select … for update、 Select \* from … where autoincrement\_col is NULL类型的查询。
-   不缓存使用用户定义变量的查询。
-   不缓存使用Hint - SQL\_NO\_CACHE的查询。

## 设置 {#section_zvy_tgf_1gb .section}

-   **参数设置**

    控制台参数设置如下。

    -   query\_cache\_limit（单位：byte）：查询缓存中可存放的单条查询最大结果集，默认为 1 MB；超过该大小的结果集不被缓存。

    -   query\_cache\_size（单位：byte）：查询缓存的大小，默认为 3 MB。

    -   query\_cache\_type：是否开启查询缓存功能。

        取值为 0 ：关闭查询功能。

        取值为 1 ：开启查询缓存功能，但不缓存Select SQL\_NO\_CACHE开头的查询。

        取值为 2 ：开启查询缓存功能，但仅缓存Select SQL\_CACHE开头的查询。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8311/155478966033697_zh-CN.png)

    **说明：** 

    -   修改query\_cache\_type需要重启实例（修改后实例会自动重启）。
    -   参数query\_cache\_size要求设置值为1024的整数倍，否则会提示**指定参数无效**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8311/155478966033698_zh-CN.png)

-   **开启**

    参数query\_cache\_size大于0并且query\_cache\_type设置为1或者2的情况下，查询缓存开启。

-   **关闭**

    设置参数query\_cache\_size为0或者设置query\_cache\_type为0关闭查询缓存。

-   **建议**
    -   query\_cache\_size不建议设置的过大。过大的空间不但挤占实例其他内存结构的空间，而且会增加在缓存中搜索的开销。建议根据实例规格，初始值设置为10MB到100 MB之间的值，而后根据运行使用情况调整。
    -   建议通过调整query\_cache\_size的值来开启、关闭查询缓存，因为修改query\_cache\_type参数需要重启实例生效。
    -   查询缓存适用于特定的场景，建议充分测试后，再考虑开启，避免引起性能下降或引入其他问题。

## 验证效果 {#section_ftc_mhf_1gb .section}

-   **控制台**

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8311/155478966033699_zh-CN.png)

-   **SQL命令**

    可以通过如下命令来获取查询缓存的使用状态。

    ```
    show global status like ‘Qca%’;
    ```

    -   Qcache\_hits：查询缓存命中次数。

    -   Qcache\_inserts：将查询和结果集写入到查询缓存中的次数。

    -   Qcache\_not\_cached：不可以缓存的查询次数。

    -   Qcache\_queries\_in\_cache：查询缓存中缓存的查询量。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8311/155478966033700_zh-CN.png)


