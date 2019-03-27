# RDS for MySQL release notes {#concept_kry_21l_n2b .concept}

## MySQL 5.7 {#section_qws_5xk_n2b .section}

-   **Version 20181226**

    -   Supported dynamic modification of binlog-row-event-max-size to accelerate the replication of tables without primary keys.
    -   Fixed the memory request problem of proxy-based instances.
-   **Version 20181121**

    -   Fixed the compatibility issue with DTS.
    -   Prohibited common users to delete system databases.
-   **Version 20181010**

-   Supported implicit primary keys.
-   Accelerated master/slave replication for tables without primary keys.
-   **Version 20180910**

    Supported Native AIO to improve the I/O performance.

-   **Version 20180601**

    -   Prohibits non-super users from running RESET SLAVE.
    -   Fixed the thread ID overflow.
-   **Version 20180431**
    -   Supported the High-availability Edition.
    -   Supported [SQL explorer](intl.en-US/User Guide/SQL explorer.md).
    -   Enhanced protection for instances that are generating snapshots.

## MySQL 5.6 {#section_d3k_zxk_n2b .section}

-   **Version 20181010**

    Added the parameter rocksdb\_ddl\_commit\_in\_the\_middle \(MyRocks\). If this parameter is turned on, certain DDL operations run the COMMIT command when being executed.

-   **Version 201806\*\* \(5.6.16\)**

    Increased the slow log precision to milliseconds.

-   **Version mysql\_20180426 \(5.6.16\)**
    -   Supported hidden indexes so that you can set invisible indexes. For more information, see [Reference](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2017-07-16)#1-invisible-indexes).
    -   Fixed bugs that occur when backup instances are applying threads.
    -   Resolved the performance deterioration that occurs when backup instances are applying partition updates.
    -   Resolved the problem that an entire TokuDB table is rebuilt by the ALTER TABLE COMMENT command. For more information, see [Reference](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2018-05-01)#1-alter-tokudb-table-comment-rebuild-whole-engine-data).
    -   Resolved possible deadlocks triggered by the SHOW SLAVE STATUS or SHOW STATUS command.
-   **Version mysql\_20171205 \(5.6.16\)**
-   -   Resolved the problem that concurrent execution of OPTIMIZE TABLE and ONLINE ALTER TABLE causes deadlocks.
-   Resolved conflicts between SEQUENCE and implicit primary keys.
-   Resolved problems related to SHOW CREATE SEQUENCE.
-   Resolved the problem that TokuDB table statistics are incorrect.
-   Resolved the problem that parallel OPTIMIZE table commands cause deadlocks.
-   Resolved the character set problems recorded in QUERY\_LOG\_EVENT.
-   Resolved the problem that databases cannot be stopped due to signal processing. For more information, see [Reference](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-%282017-10-10%29#1-the-ack-receiver-thread-didnt-handle-signal-correctly).
-   Resolved problems caused by RESET MASTER.
-   Resolved the problem that backup databases are stuck in the waiting state.
-   Resolved the possible process termination caused by SHOW CREATE TABLE.
-   **Version 20170927 \(5.6.16\)**
    -   Resolved the problem that TokuDB table queries use incorrect indexes.
-   **Version 20170901 \(5.6.16\)**
-   -   Upgraded the SSL encryption version to TLS1.2. For more information, see [Reference](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2017-10-10)#2-upgrade-ssl-tlsv12).
-   Supported SEQUENCE.
-   Resolved the problem that NOT IN queries return incorrect results in certain scenarios.
-   **Version 20170530 \(5.6.16\)**

    Allowed master accounts to kill connections of common accounts.

-   **Version 20170221 \(5.6.16\)**

    Supported [Introduction to read/write splitting](intl.en-US/User Guide/Read__write splitting/Introduction to read__write splitting.md).


