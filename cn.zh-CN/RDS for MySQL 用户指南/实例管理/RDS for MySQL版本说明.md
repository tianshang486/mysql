# RDS for MySQL版本说明 {#concept_kry_21l_n2b .concept}

## MySQL 5.7 {#section_qws_5xk_n2b .section}

-   **20181226版本**

    -   新特性：支持动态修改binlog-row-event-max-size，加速无主键表的复制。
    -   修复Proxy实例内存申请异常的问题。
-   **20181010版本**

    新特性：

    -   支持隐式主键；
    -   加快无主键表的主备复制；
    -   支持Native AIO，提升I/O性能。
-   **20180431版本**

-   新特性：
    -   支持高可用版；
    -   支持[ZH-CN\_TP\_7947.md\#](cn.zh-CN/用户指南/数据安全性/SQL审计.md#)；
    -   增强对处于快照备份状态的实例的保护。

## MySQL 5.6 {#section_d3k_zxk_n2b .section}

-   **20181010版本**

    添加参数rocksdb\_ddl\_commit\_in\_the\_middle（MyRocks）。如果这个参数被打开，部分DDL在执行过程中将会执行commit操作。

-   **201806\*\* （5.6.16）版本**

    新特性：slow log精度提升为微秒。

-   **20180426（5.6.16）版本**
    -   新特性：引入隐藏索引，支持将索引设置为不可见，详情请[参考文档](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2017-07-16)#1-invisible-indexes)。
    -   修复备库apply线程的bug；
    -   修复备库apply分区表更新时性能下降问题；
    -   修复TokuDB下alter table comment重建整张表问题，详情请[参考文档](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2018-05-01)#1-alter-tokudb-table-comment-rebuild-whole-engine-data)；
    -   修复由show slave status/show status可能触发的死锁问题。
-   **20171205（5.6.16）版本**
    -   修复OPTIMIZE TABLE和ONLINE ALTER TABLE同时执行时会触发死锁的问题；
    -   修复SEQUENCE与隐含主键冲突的问题；
    -   修复SHOW CREATE SEQUENCE问题；
    -   修复TokuDB引擎的表统计信息错误；
    -   修复并行OPTIMIZE表引入的死锁问题；
    -   修复QUERY\_LOG\_EVENT中记录的字符集问题；
    -   修复信号处理引起的数据库无法停止问题，详情请[参考文档](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-%282017-10-10%29#1-the-ack-receiver-thread-didnt-handle-signal-correctly)；
    -   修复RESET MASTER引入的问题；
    -   修复备库陷入等待的问题；
    -   修复SHOW CREATE TABLE可能触发的进程崩溃问题。
-   **20170927（5.6.16）版本**
    -   修复TokuDB表查询时使用错误索引问题。
-   **20170901（5.6.16）版本**
    -   新特性：
        -   升级SSL加密版本到TLS 1.2，详情请[参考文档](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2017-10-10)#2-upgrade-ssl-tlsv12)；
        -   支持Sequence。
    -   修复NOT IN查询在特定场景下返回结果集有误的问题。
-   **20170530 \(5.6.16\)版本**
    -   新特性：支持高权限账号Kill其他账号下的连接。
-   **20170221（5.6.16）版本**
    -   新特性：支持[读写分离](cn.zh-CN/用户指南/读写分离/读写分离简介.md#)。

