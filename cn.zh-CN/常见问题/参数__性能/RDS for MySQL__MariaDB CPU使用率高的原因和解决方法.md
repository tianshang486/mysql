# RDS for MySQL/MariaDB CPU使用率高的原因和解决方法 {#concept_j4b_2js_g2b .concept}

RDS for MySQL/MariaDB使用过程中，会遇到CPU使用率过高甚至达到100%的情况。本文将介绍造成该状况的常见原因以及解决方法，并通过CPU使用率为100%的典型场景，来分析引起该状况的原因及其相应的解决方案。

## 常见原因 {#section_ivq_s22_ggb .section}

系统执行应用提交查询（包括数据修改操作）时需要大量的逻辑读（逻辑IO，执行查询所需访问的表的数据行数），所以系统需要消耗大量的CPU资源以维护从存储系统读取到内存中的数据一致性。

**说明：** 大量行锁冲突、行锁等待或后台任务也有可能会导致实例的CPU使用率过高，但这些情况出现的概率非常低，本文不做讨论。

下文通过一个简化的模型来说明系统资源、语句执行成本以及QPS（Query Per Second每秒执行的查询数）之间的关系：

-   条件：应用模型恒定（应用没有修改）。
-   avg\_lgc\_io：执行每条查询需要的平均逻辑 IO。
-   total\_lgc\_io：实例的 CPU 资源在单位时间内能够处理的逻辑 IO 总量。
-   关系公式：total\_lgc\_io = avg\_lgc\_io x QPS -- 单位时间 CPU 资源 = 查询执行的平均成本 x 单位时间执行的查询数量。

## 解决方法 {#section_q1r_sf2_ggb .section}

您可以利用数据管理（DMS）或者[CloudDBA](../../../../cn.zh-CN/RDS for MySQL 用户指南/性能优化__诊断（CloudDBA）/MySQL CloudDBA简介.md#)解决MySQL/MariaDB实例CPU使用率过高的问题。下文主要介绍使用DMS来解决CPU使用率过高的问题，如何通过CloudDBA来解决CPU使用率过高的问题，可以参考文档[利用CloudDBA解决MySQL实例CPU使用率过高的问题](https://help.aliyun.com/document_detail/65233.html)。

数据管理工具提供了几种辅助排查并解决实例性能问题的功能，主要有：

-   实例诊断报告。
-   SQL 窗口提供的查询优化建议和查看执行计划。
-   实例会话。

其中，实例诊断报告是排查和解决MySQL/MariaDB实例性能问题的最佳工具。无论何种原因导致的性能问题，建议您首先参考下实例诊断报告，尤其是诊断报告中的SQL优化、会话列表和慢SQL汇总分。

## 避免出现CPU使用率达到100%的一般原则 {#section_sqg_bg2_ggb .section}

-   设置CPU使用率告警，实例CPU使用率保证一定的冗余度。
-   应用设计和开发过程中，要考虑查询的优化，遵守MySQL优化的一般优化原则，降低查询的逻辑IO，提高应用可扩展性。
-   新功能、新模块上线前，要使用生产环境数据进行压力测试（可以考虑使用阿里云PTS压力测试工具）。
-   新功能、新模块上线前，建议使用生产环境数据进行回归测试。
-   建议经常关注和使用DMS中的诊断报告。

    **说明：** 关于如何访问DMS中的诊断报告，请参见[RDS如何访问诊断报告](https://help.aliyun.com/document_detail/41814.html)。


## 典型示例 {#section_gch_kg2_ggb .section}

以CPU使用率为100%的典型场景为例，下文介绍了两个引起该状况的原因及其解决方案，即应用负载（QPS）高和查询执行成本（查询访问表数据行数avg\_lgc\_io）高。其中，由于查询执行成本高（查询访问表数据行数多）而导致实例CPU使用率高是MySQL非常常见的问题。

-   应用负载（QPS）高
    -   现象描述
        -   特征：实例的QPS（每秒执行的查询次数）高，查询比较简单、执行效率高、优化余地小。
        -   表现：没有出现慢查询（或者慢查询不是主要原因），且QPS和CPU使用率曲线变化吻合。
        -   常见场景：该状况常见于应用优化过的在线事务交易系统（例如订单系统）、高读取率的热门Web网站应用、第三方压力工具测试（例如 Sysbench）等。
    -   解决方案

        对于由应用负载高导致的CPU使用率高的状况，使用SQL查询进行优化的余地不大，建议您从应用架构、实例规格等方面来解决，例如：

        -   升级实例规格，增加CPU资源。
        -   增加只读实例，将对数据一致性不敏感的查询（例如商品种类查询、列车车次查询）转移到只读实例上，分担主实例压力。
        -   使用阿里云DRDS产品，自动进行分库分表，将查询压力分担到多个RDS实例上。
        -   使用阿里云Memcache或者云Redis产品，尽量从缓存中获取常用的查询结果，减轻RDS实例的压力。
        -   对于查询数据比较静态、查询重复度高、查询结果集小于1MB 的应用，考虑开启查询缓存（Query Cache）。

            **说明：** 能否从开启查询缓存（Query Cache）中获益需要经过测试，具体设置请参见[RDS for MySQL 查询缓存（Query Cache）的设置和使用](https://help.aliyun.com/document_detail/41717.html?spm=a2c4g.11186623.2.17.a665446edOcZDv)。

        -   定期归档历史数据、采用分库分表或者分区的方式减小查询访问的数据量。
        -   尽量优化查询，减少查询的执行成本（逻辑IO，执行需要访问的表数据行数），提高应用可扩展性。
-   查询执行成本（查询访问表数据行数avg\_lgc\_io）高
    -   现象描述
        -   特征：实例的QPS（每秒执行的查询次数）不高；查询执行效率低、执行时需要扫描大量表中数据、优化余地大。
        -   表现：存在慢查询，QPS和CPU使用率曲线变化不吻合。
        -   原因分析：由于查询执行效率低，为获得预期的结果即需要访问大量的数据（平均逻辑IO高），在 QPS并不高的情况下（例如网站访问量不大），就会导致实例的CPU使用率高。
    -   解决方案

        解决该状况的原则是：定位效率低的查询、优化查询的执行效率、降低查询执行的成本。

        操作步骤

        1.  通过如下方式定位效率低的查询：
            -   通过 `show processlist;` 或 `show full processlist;` 命令查看当前执行的查询，如下图所示：

                ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8195/156868735135232_zh-CN.png)

                对于查询时间长、运行状态（State 列）是**Sending data**、**Copying to tmp table**、**Copying to tmp table on disk**、**Sorting result**、**Using filesort**等都可能是有性能问题的查询（SQL）。

                **说明：** 

                -   若在QPS高导致CPU使用率高的场景中，查询执行时间通常比较短，`show processlist;`命令或实例会话中可能会不容易捕捉到当前执行的查询。您可以通过执行如下命令进行查询：

                    ``` {#codeblock_32b_gqq_z9x}
                    explain select b.* from perf_test_no_idx_01 a, perf_test_no_idx_02 b where a.created_on >= 2015-01-01 and a.detail = b.detail
                    ```

                -   您可以通过执行类似`kill 101031643;`的命令来终止长时间执行的会话，终止会话请参见 [RDS for MySQL 如何终止会话](https://help.aliyun.com/document_detail/41713.html?spm=a2c4g.11186623.2.19.a665446edOcZDv)。关于长时间执行会话的管理，请参见 [RDS for MySQL 管理长时间运行查询](https://help.aliyun.com/document_detail/41735.html?spm=a2c4g.11186623.2.20.a665446edOcZDv)。
            -   通过DMS查看当前执行的查询，查询步骤如下：
                1.  在DMS控制台上[登录数据库](https://help.aliyun.com/document_detail/47714.html?spm=a2c4g.11186623.2.21.a665446edOcZDv)。
                2.  选择**性能** \> **实例会话**，打开实例会话页面，如下图所示。

                    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8195/156868735135253_zh-CN.png)

                3.  单击SQL列中的查询文本，即可显示完整的查询语句，如下图所示。

                    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8195/156868735135257_zh-CN.png)

        2.  得到需要优化的查询后，可以通过DMS控制台上SQL诊断来获取查询的优化建议：

            **说明：** 诊断报告同样适用于排查历史实例CPU使用率高的问题。

            1.  在DMS 控制台上[登录数据库](https://help.aliyun.com/document_detail/47714.html?spm=a2c4g.11186623.2.26.317b446eTd7q5l)。
            2.  选择**SQL操作** \> **SQL窗口**，如下图所示。

                ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8195/156868735135257_zh-CN.png)

            3.  单击SQL诊断，即可得到优化建议，如下图所示。

                ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8195/156868735135258_zh-CN.png)

        3.  根据优化建议，添加索引，查询执行成本就会大幅减少，实例CPU使用率100%的问题解决。

