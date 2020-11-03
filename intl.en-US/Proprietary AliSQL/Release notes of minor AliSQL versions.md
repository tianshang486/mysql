# Release notes of minor AliSQL versions

This topic describes the release notes of minor AliSQL versions.

## ApsaraDB RDS for MySQL 8.0

20200831

-   New features:
    -   An option is added to disable parallel scan for the `COUNT (*)` function.
    -   Start global transaction identifiers \(GTIDs\) and end GTIDs are introduced to the mysqlbinlog plug-in.
    -   Various log sequence numbers \(LSNs\) in the redo log are supported.
        -   innodb\_lsn: the LSN of each record in the redo log.
        -   innodb\_log\_checkpoint\_lsn: the LSN of the last checkpoint.
        -   innodb\_log\_write\_lsn: the LSN of each record that is written into the redo log.
        -   innodb\_log\_ready\_for\_write\_lsn: the LSN of the last record that is written into the log buffer.
        -   innodb\_log\_flush\_lsn: the LSN of each record that is flushed from the redo log to the disk.
        -   innodb\_log\_dirty\_pages\_added\_up\_to\_lsn: the LSN of each record that logs a page as dirty.
        -   innodb\_log\_oldest\_lsn: the LSN of each record that logs an update to a page.
-   Performance optimization:
    -   The concurrency control \(CCL\) mechanism is optimized to better determine how transactions wait and concurrently run.
    -   The CCL mechanism is optimized to better prioritize the stored procedures that are to run.
-   Bugs fixed:
    -   The bug that prevents the recursively called interpreter from checking the memory size is fixed.
    -   The bug that prevents you from modifying table definitions when transparent data encryption \(TDE\) is enabled is fixed.
    -   The bug that causes the event scheduler to leak memory is fixed.

20200630

-   New features:
    -   The faster DDL feature is introduced to provide an optimized buffer pool management mechanism. This mechanism reduces the impact of data definition language \(DDL\) operations and increases the number of concurrent DDL operations that are allowed. For more information, see [Faster DDL](/intl.en-US/Proprietary AliSQL/Stability/Faster DDL.md).
    -   The maximum number of connections that are allowed is increased to 500,000.
-   Performance optimization:
    -   The thread pool feature is optimized.
    -   The memory allocation mechanism is optimized. You can specify the maximum number of memory resources that are allowed for Performance Schema based on the instance type.
    -   SQL log files are no longer detected.
    -   TDE is optimized to cache the keys that are provided by Alibaba Cloud Key Management Service \(KMS\).
    -   The status of threads that are managed by the CCL mechanism is modified. For more information, see [Statement concurrency control](/intl.en-US/Proprietary AliSQL/Stability/Statement concurrency control.md).
-   Bugs fixed:
    -   The bug that causes the system to consider a semicolon \(;\) to be a part of the command used to create an outline is fixed.
    -   The bug that causes the server to unexpectedly exit in the event of table modifications is fixed.
    -   The bug that causes earlier versions to disallow the memory and array keywords supported in later versions is fixed.
    -   The bug that causes the system to incorrectly count the number of waits when commands are read from a client is fixed.
    -   The bug that causes failures in minor engine version updates is fixed.

20200430

-   New features:
    -   The Binlog in Redo feature is introduced. It writes binary logs into redo log files before the binary logs are written to the disk. This reduces I/O consumption and improves database performance. For more information, see [Binlog in Redo](/intl.en-US/Proprietary AliSQL/Performance/Binlog in Redo.md).
    -   The data protection feature is introduced. It supports the customization of security policies that are used to manage the permissions on DROP and TRUNCATE statements. This allows you to avoid data losses that are caused by the unintentional execution of these statements. For more information, see [Data Protect](/intl.en-US/Proprietary AliSQL/Security/Data Protect.md).
    -   A restructured row caching mechanism is introduced to the X-Engine storage engine.
    -   The XA\_RECOVER\_ADMIN permission is provided.
-   Performance optimization:
    -   The code that is used to scan data when operations are performed on a temporary InnoDB table is optimized. This allows the system to scan only dirty pages instead of the entire buffer pool.
    -   The global parameter opt\_readonly\_trans\_implicit\_commit is renamed to rds\_disable\_explicit\_trans. This ensures compatibility with MySQL 5.6.
    -   The SQL Explorer \(SQL Audit\) feature is optimized, so it does not log upgrades to RDS instances.
    -   Memory resources that are consumed by DDL operations on X-Engine tables are reduced.
-   Bugs fixed:
    -   The bug that causes the sizes of X-Engine tables stored on the disk to be inconsistent with the statistical information in the INFORMATION\_SCHEMA schema is fixed.
    -   The bug that causes the system to initialize X-Engine logs when the error log file is re-opened is fixed.

20200331

-   New feature:

    The `TRUNCATE TABLE` statement is supported. After you execute this statement on a table, this statement moves the table to a dedicated directory that is used for the recycle bin. Then, this statement creates a table by using the schema of the table that you truncate. For more information, see [Recycle bin](/intl.en-US/Proprietary AliSQL/Security/Recycle bin.md).

-   Performance optimization:
    -   The output of Transmission Control Protocol \(TCP\) errors is disabled by default.
    -   The performance of the thread pool feature with the default configuration is improved.
-   Bugs fixed:
    -   The bug that databases and tables become invalid because the names of partitioned tables are separated by using a pound key and a letter p \(`#p`\) is fixed.
    -   The bug that causes the CCL-managed statements to be case-sensitive is fixed.
-   Changes incorporated: Changes in MySQL 8.0.17 and MySQL 8.0.18 are incorporated. For more information, see [Changes in MySQL 8.0.17](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-17.html) and [Changes in MySQL 8.0.18](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-18.html).

20200229

-   New features:
    -   The performance agent feature is introduced. For more information, see [Performance Agent](/intl.en-US/Proprietary AliSQL/Stability/Performance Agent.md). This feature is provided as a MySQL plug-in. It allows you to collect and analyze the performance metrics of an RDS instance.
    -   Network round-trip time is supported for the semi-synchronous mode. This allows you to better understand the performance of an RDS instance.
-   Performance optimization:
    -   Statement-level CCL is allowed on read-only RDS instances.
    -   Outlines are supported for secondary RDS instances.
    -   The database proxy feature is enhanced to optimize short-lived connections.
    -   The time that is required to execute a PAUSE statement is reduced in various CPU architectures.
    -   A memory table is introduced to present the running status of thread pools.
-   Bugs fixed:
    -   The bug that causes the system to forbid the ppoll function and replace the ppoll function with the poll function in Linux kernels earlier than 4.9 is fixed.
    -   The bug that causes errors when the system calls the wrap\_sm4\_encrypt function is fixed.
    -   The bug that causes the system to lock global variables when SQL logs are rotated is fixed.
    -   The bug that causes errors in restoration inconsistency checks is fixed.
    -   The bug that causes inaccurate time values in the io\_statistics table is fixed.
    -   The bug that causes the system to unexpectedly exit when invalid compression algorithms are invoked is fixed.
    -   The bug that causes user columns in MySQL 8.0 and MySQL 5.6 to be incompatible is fixed.

20200110

-   New feature:

    Three hints are introduced. These hints can be used in SELECT, UPDATE, INSERT, and DELETE statements to commit and roll back transactions at high speeds. This allows you to increase the throughput of your application. For more information, see [Inventory Hint](/intl.en-US/Proprietary AliSQL/Performance/Inventory Hint.md).

-   Performance optimization:
    -   The CCL mechanism is optimized. When an RDS instance is started, CCL queue structures are initialized before CCL rules are initialized.
    -   The file deletion mechanism is optimized. When you asynchronously delete small files, links to the small files are canceled.
    -   The performance of thread pools is optimized. For more information, see [Thread Pool](/intl.en-US/Proprietary AliSQL/Feature/Thread Pool.md).
    -   Restoration inconsistency checks are disabled by default.
    -   The permissions that are required to configure variables are changed.
        -   The user role that is authorized to configure the following variables is changed to standard user:
            -   auto\_increment\_increment
            -   auto\_increment\_offset
            -   bulk\_insert\_buffer\_size
            -   binlog\_rows\_query\_log\_events
        -   The user role that is authorized to configure the following variables is changed to superuser or system variable administrator:
            -   binlog\_format
            -   binlog\_row\_image
            -   binlog\_direct
            -   sql\_log\_off
            -   sql\_log\_bin

20191225

-   New feature:

    The recycle bin feature is introduced. All of the tables that you delete are moved to the recycle bin. You can specify a retention period within which you can retrieve the deleted tables from the recycle bin. For more information, see [Recycle bin](/intl.en-US/Proprietary AliSQL/Security/Recycle bin.md).

-   Performance optimization:
    -   The mechanism that is used to process short-lived connections is optimized.
    -   A dedicated thread is used to serve the maintain user. This allows you to avoid high availability \(HA\) failures.
    -   The locking mechanism is optimized. If an error occurs when binary logs are flushed by using redo logs, ApsaraDB RDS can explicitly release the lock that is triggered by file synchronization.
    -   The deletion of unnecessary TCP error logs is supported.
    -   Thread pools are enabled by default.
-   Bugs fixed:
    -   The bug that causes errors in updates to slow query logs is fixed.
    -   The bug that causes an inappropriate lock scope is fixed.
    -   The bug that causes errors in core dumps when the system invokes the select function for TDE is fixed.

20191115

New feature:

The statement queue feature is introduced. It allows statements to queue in the same bucket. These statements may be executed on the same resources. For example, these statements are executed on the same row of a table. This reduces overheads from possible conflicts. For more information, see [Statement Queue](/intl.en-US/Proprietary AliSQL/Performance/Statement Queue.md).

20191101

-   New features:
    -   The SM4 encryption algorithm is supported for TDE. For more information, see [Configure TDE for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md).
    -   Data protection for secondary RDS instances is supported. Only the accounts with the SUPER or REPLICATION\_SLAVE\_ADMIN role have the permissions to insert, delete, and modify data in the slave\_master\_info, slave\_relay\_log\_info, and slave\_worker\_info tables.
    -   A mechanism is introduced to increase the priorities of auto-increment keys. If a table does not have a primary key or it does not have a unique key without a null value, the auto-increment key without a null value has the highest priority.
    -   A mechanism is introduced to prevent the automatic conversion of tables from the MEMORY to MyISAM storage engines. These tables include system tables. These tables also include the tables that are invoked by threads in the initializing state.
    -   A mechanism is introduced to flush binary log files to the disk before redo log files.
    -   A mechanism is introduced to stop the creation of temporary tables on an RDS instance when the RDS instance is locked.
    -   The X-Engine storage engine is provided to store transactions based on a log-structured merge \(LSM\) tree.
-   Performance optimization:
    -   The thread pool feature is optimized to reduce mutexes. For more information, see [Thread Pool](/intl.en-US/Proprietary AliSQL/Feature/Thread Pool.md).
    -   The performance insight feature is optimized to monitor thread pools. For more information, see [Performance Insight](/intl.en-US/Proprietary AliSQL/Stability/Performance Insight.md).
    -   The following parameters are adjusted:
        -   `primary_fast_lookup`: a session parameter. Default value: true.
        -   `thread_pool_enabled`: a global parameter. Default value: true.

20191015

-   New features:
    -   The TDE feature is introduced to support real-time I/O encryption and decryption on data files. Data is encrypted before it is written to the disk and decrypted before it is read from the disk to the memory. For more information, see [Configure TDE for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md).
    -   The returning feature is introduced. It allows data manipulation language \(DML\) statements to return result sets. In addition, the DBMS\_TRANS package is provided for you to use this feature. For more information, see [Returning](/intl.en-US/Proprietary AliSQL/Feature/Returning.md).
    -   The forced conversion from the MyISAM or MEMORY storage engine to the InnoDB storage engine is supported. If the global variable **force\_mysiam\_to\_innodb** or **force\_memory\_to\_innodb** is set to **ON**, a table is converted from the MyISAM or MEMORY storage engine to the InnoDB storage engine when the table is created or modified.
    -   A mechanism is introduced to forbid standard accounts from performing primary/secondary switchovers. Only privileged accounts have the permissions to perform primary/secondary switchovers.
    -   A performance proxy plug-in is provided. This plug-in obtains performance data and saves the data as TXT files to your computer. These files are deleted in a circular manner. Only the latest files at the single-digit second level are retained.
    -   A configurable timeout period is introduced for mutexes in InnoDB: This timeout period can be changed by setting the global variable **innodb\_fatal\_semaphore\_wait\_threshold**. The default value of the global variable is 600.
    -   Index hint errors can be ignored by setting the global variable **ignore\_index\_hint\_error**. The default value of the global variable is false.
    -   The SSL encryption feature can be disabled. For more information, see [Configure SSL encryption on an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure SSL encryption on an ApsaraDB RDS for MySQL instance.md).
    -   The output of TCP errors is supported. TCP errors in read, read-wait, and write-wait events are returned with their error codes by using end\_connection events. In addition, logs with information about the errors are generated.
-   Bugs fixed:
    -   The bug that prevents a Linux operating system from merging local asynchronous I/O \(AIO\) requests before linear Read Ahead is triggered is fixed.
    -   The bug that prevents the proper collection of table and index statistics is fixed.
    -   The bug that prevents the system direct access to the primary key index of a table with a primary key is fixed.

20190915

Bug fixed:

The bug that causes memory leaks when the Cmd\_set\_current\_connection process runs is fixed.

20190816

-   New features:
    -   The thread pool feature is introduced to separate threads from sessions. If a large number of sessions exist, the system can run a small number of threads to complete the tasks in active sessions. For more information, see [Thread Pool](/intl.en-US/Proprietary AliSQL/Feature/Thread Pool.md).
    -   The CCL mechanism is introduced. It allows you to specify the maximum number of concurrent requests that are allowed. This enables the system to handle traffic bursts, process statements that consume excessive resources, and adapt to changes of SQL models. This also ensures the continuity and stability of your database service. For more information, see [Statement concurrency control](/intl.en-US/Proprietary AliSQL/Stability/Statement concurrency control.md).
    -   The statement outline feature is introduced to support optimizer hints and index hints. These hints are used to stabilize the execution of query plans on an RDS instance. For more information, see [Statement outline](/intl.en-US/Proprietary AliSQL/Feature/Statement outline.md).
    -   The Sequence engine is introduced to simplify the acquisition of sequence values. For more information, see [Sequence Engine](/intl.en-US/Proprietary AliSQL/Feature/Sequence Engine.md).
    -   The Purge Large File Asynchronously feature is introduced to asynchronously delete files. Before you delete a tablespace, the system renames the files in the tablespace as temporary files. Then, a background thread is started to asynchronously delete the temporary files. For more information, see [Purge Large File Asynchronously](/intl.en-US/Proprietary AliSQL/Stability/Purge Large File Asynchronously.md).
    -   The performance insight feature is introduced to support load monitoring, association analysis, and performance optimization at the instance level. This feature allows you to evaluate the loads of an RDS instance. This feature also allows you to locate performance issues to ensure the stability of your database service. For more information, see [Performance Insight](/intl.en-US/Proprietary AliSQL/Stability/Performance Insight.md).
    -   An optimized instance locking mechanism is introduced. You can delete tables from an RDS instance by using DROP or TRUNCATE statements even if the RDS instance is locked.
-   Bugs fixed:
    -   The bug that causes the system to incorrectly calculate file sizes is fixed.
    -   The bug that allows irrelevant processes to reuse released memory resources is fixed.
    -   The bug that causes a host to exit unexpectedly when the available cache size on the host is 0 is fixed.
    -   The bug that causes conflicts between implicit primary keys and CTS statements is fixed.
    -   The bug that causes the system to incorrectly log slow queries is fixed.

20190601

-   Performance optimization:
    -   Metadata locking on logging tables is reduced.
    -   The code for termination options is restructured.
-   Bugs fixed:
    -   The bug that prevents the SQL Explorer \(SQL Audit\) feature from logging precompiled statements is fixed.
    -   The bug that prevents the system from filtering out error logs in logging tables with invalid names is fixed.

## ApsaraDB RDS for MySQL 5.7 on RDS Basic or High-availability Edition

20200831

-   New features:
    -   Changes incorporated: Changes in MySQL 5.7.30 are incorporated. For more information, visit [GitHub](https://github.com/mysql/mysql-server).
    -   An optimized CCL mechanism is introduced to better determine how transactions wait and concurrently run.
    -   Start GTIDs and end GTIDs are introduced to the mysqlbinlog plug-in.
    -   Various LSNs in the redo log are supported.
        -   innodb\_lsn: the LSN of each record in the redo log.
        -   innodb\_log\_write\_lsn: the LSN of each record that is written into the redo log.
        -   innodb\_log\_checkpoint\_lsn: the LSN of the last checkpoint.
        -   innodb\_log\_flushed\_lsn: the LSN of each record that is flushed from the redo log to the disk.
        -   innodb\_log\_Pages\_flushed: the LSN of each record that logs an update to a page.
-   Performance optimization:

    The CCL mechanism is optimized to better prioritize the stored procedures that are to run.

-   Bug fixed:

    Some major bugs that cause the server to unexpectedly stop when you shut down the server are fixed.


20200630

-   New features:
    -   Three hints are introduced to the inventory hint feature. These hints are used in SELECT, UPDATE, INSERT, and DELETE statements to commit and roll back transactions at high speeds. This allows you to increase the throughput of your application. For more information, see [Inventory Hint](/intl.en-US/Proprietary AliSQL/Performance/Inventory Hint.md).
    -   The CCL mechanism is introduced. It allows you to specify the maximum number of concurrent requests that are allowed. This enables the system to handle traffic bursts, process statements that consume excessive resources, and adapt to changes of SQL models. This also ensures the continuity and stability of your database service. For more information, see [Statement concurrency control](/intl.en-US/Proprietary AliSQL/Stability/Statement concurrency control.md).
    -   The statement queue feature is introduced. It allows statements to queue in the same bucket. These statements may be executed on the same resources. For example, these statements are executed on the same row of a table. This reduces overheads from possible conflicts. For more information, see [Statement Queue](/intl.en-US/Proprietary AliSQL/Performance/Statement Queue.md).
    -   The statement outline feature is introduced to support optimizer hints and index hints. These hints are used to stabilize the execution of query plans on an RDS instance. For more information, see [Statement outline](/intl.en-US/Proprietary AliSQL/Feature/Statement outline.md).
    -   The faster DDL feature is introduced to provide an optimized buffer pool management mechanism. This mechanism reduces the impact of DDL operations and increases the number of concurrent DDL operations that are allowed. For more information, see [Faster DDL](/intl.en-US/Proprietary AliSQL/Stability/Faster DDL.md).
    -   The maximum number of connections that are allowed is increased to 500,000.
-   Performance optimization:
    -   The `call dbms_admin.show_native_procedure();` command is provided to view all of the procedures on an RDS instance.
    -   A new function is provided to delete orphan tables.
    -   The thread pool feature is optimized.
    -   Query caching is optimized.
    -   The memory allocation mechanism is optimized. You can specify the maximum number of memory resources that are allowed for Performance Schema based on the instance type.
-   Bug fixed:

    The bug that causes an audit update thread to enter an infinite loop is fixed.


20200430

-   New feature:

    The data protection feature is introduced. It supports the customization of security policies that are used to manage the permissions on DROP and TRUNCATE statements. This allows you to avoid data losses that are caused by the unintentional execution of these statements. For more information, see [Data Protect](/intl.en-US/Proprietary AliSQL/Security/Data Protect.md).

-   Performance optimization:

    Read-write locks are no longer supported in the query cache. The default hash function is changed from LF\_hash to murmur3 hash.

-   Bug fixed:

    Two bugs that occur after the system hits the query cache during the execution of transactions at the REPEATABLE\_READ isolation level are fixed.


20200331

-   New features:
    -   The fast query cache is introduced. It is developed by Alibaba Cloud based on the native MySQL query cache. It uses a new design and implementation mechanism to improve query performance. For more information, see [A new version is available.](/intl.en-US/Proprietary AliSQL/Performance/Fast query cache.md).
    -   Two metadata locks are introduced from Percona Server 5.7: LOCK TABLES FOR BACKUP \(LTFB\) and LOCK BINLOG FOR BACKUP \(LBFB\).
-   Performance optimization:
    -   The thread pool feature is optimized to ensure compatibility with earlier MySQL versions.
    -   The output of TCP errors is disabled by default.
    -   The performance of the thread pool feature with the default configuration is improved.
-   Bugs fixed:
    -   The bug that causes the system to delete temporary files when you delete large files is fixed.
    -   The bug that causes dump threads in thread pools to time out is fixed.
    -   The bug that causes the system to incorrectly count the value of the IPK field in the procedure context is fixed.
    -   The bug that causes rds\_change\_user to incur pfs thread leakage and release is fixed.
-   Changes incorporated: Changes in MySQL 5.7.28 are incorporated. For more information, visit [GitHub](https://github.com/mysql/mysql-server).

20200229

-   New features:
    -   The performance agent feature is introduced. For more information, see [Performance Agent](/intl.en-US/Proprietary AliSQL/Stability/Performance Agent.md). This feature is provided as a MySQL plug-in. It allows you to collect and analyze the performance metrics of an RDS instance.
    -   Network round-trip time is supported for the semi-synchronous mode. This allows you to better understand the performance of an RDS instance.
-   Performance optimization:
    -   The time that is required to execute a PAUSE statement is reduced in various CPU architectures.
    -   The database proxy feature is enhanced to optimize short-lived connections.
    -   A memory table is introduced to present the running status of thread pools.
-   Bugs fixed:
    -   The bug that causes DDL redo logs that are not secure is fixed.
    -   The bug that causes inaccurate time values in the io\_statistics table is fixed.
    -   The bug that causes the server to unexpectedly exit in the event of table modifications is fixed.
    -   The bugs in MySQL test cases are fixed.

20200110

Performance optimization:

-   The file deletion mechanism is optimized. When you asynchronously delete small files, links to the small files are canceled.
-   The performance of the thread pool feature is optimized. For more information, see [Thread Pool](/intl.en-US/Proprietary AliSQL/Feature/Thread Pool.md).
-   The default value of the thread\_pool\_enabled parameter is changed to OFF.

20191225

-   New feature:

    The management of internal accounts is supported. This allows you to manage user permissions and protect your data.

-   Performance optimization:
    -   The mechanism that is used to process short-lived connections is optimized.
    -   A dedicated thread is used to serve the maintain user. This allows you to avoid HA failures.
    -   The deletion of unnecessary TCP error logs is supported.
    -   The thread pool feature is optimized.
-   Bugs fixed:
    -   The bug that causes the mysqld process to unexpectedly exit when the read/write splitting function is enabled is fixed.
    -   The bug that causes errors in core dumps when the system uses a keyring is fixed.

20191115

Bug fixed:

The bug that causes the system to display variables in SQL logs that are generated from primary/secondary switchovers is fixed.

20191101

-   New features:
    -   The SM4 encryption algorithm is supported for TDE. For more information, see [Configure TDE for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md).
    -   A mechanism is introduced to allow the system to access the primary index of a table with a primary key.
    -   A mechanism is introduced to prevent the automatic conversion of tables from the MEMORY to MyISAM storage engines. These tables include system tables. These tables also include the tables that are invoked by threads in the initializing state.
-   Performance optimization:
    -   The thread pool feature is optimized to reduce mutexes. For more information, see [Thread Pool](/intl.en-US/Proprietary AliSQL/Feature/Thread Pool.md).
    -   An SQL log caching mechanism is introduced to increase SQL logging performance.
    -   The performance insight feature is optimized to monitor thread pools. For more information, see [Performance Insight](/intl.en-US/Proprietary AliSQL/Stability/Performance Insight.md).
    -   The thread pool feature is enabled by default. For more information, see [Thread Pool](/intl.en-US/Proprietary AliSQL/Feature/Thread Pool.md).
-   Bugs fixed:
    -   The bug that prevents the release of locks on user tables when these tables are being managed or maintained is fixed.
    -   More TCP errors are added.

20191015

-   New features:
    -   The rotation of slow query logs is supported. Each CSV slow query log file is assigned a unique name and a new file. This prevents data losses during the collection of slow query logs. You can run the `show variables like '%rotate_log_table%';` command to check whether the rotation of slow query logs is enabled.
    -   A performance proxy plug-in is provided. This plug-in obtains performance data and saves the data as TXT files to your computer. These files are deleted in a circular manner. Only the latest files at the single-digit second level are retained.
    -   The forced conversion from the MEMORY to InnoDB storage engines is supported. If the global variable **rds\_force\_memory\_to\_innodb** is set to **ON**, a table is converted from the MEMORY to InnoDB storage engines when the table is created or modified.
    -   The keyring-rds plug-in is introduced to TDE. This plug-in allows ApsaraDB RDS to communicate with the administration system or Alibaba Cloud KMS.
    -   The output of TCP errors is supported. TCP errors in read, read-wait, and write-wait events are returned with their error codes by using end\_connection events. In addition, logs with information about the errors are generated.
-   Bug fixed:

    The bug that causes Error 1290 in DDL operations is fixed.


20190925

Parameter adjustment:

-   The default value of the system variable auto\_generate\_certs is changed from true to false.
-   The global read-only variable auto\_detact\_certs is introduced. Valid values: true and false. Default value: false. This variable is supported only when code is compiled by using OpenSSL on the server. This variable specifies whether the server automatically searches for SSL certificate and key files in the data directory.

20190915

New feature:

The thread pool feature is introduced to separate threads from sessions. If a large number of sessions exist, the system can run a small number of threads to complete the tasks in active sessions. For more information, see [Thread Pool](/intl.en-US/Proprietary AliSQL/Feature/Thread Pool.md).

20190815

-   New features:
    -   The Purge Large File Asynchronously feature is introduced to asynchronously delete files. Before you delete a tablespace, the system renames the files in the tablespace as temporary files. Then, a background thread is started to asynchronously delete the temporary files. For more information, see [Purge Large File Asynchronously](/intl.en-US/Proprietary AliSQL/Stability/Purge Large File Asynchronously.md).
    -   The performance insight feature is introduced to support load monitoring, association analysis, and performance optimization at the instance level. This feature allows you to evaluate the loads of an RDS instance. This feature also allows you to locate performance issues to ensure the stability of your database service. For more information, see [Performance Insight](/intl.en-US/Proprietary AliSQL/Stability/Performance Insight.md).
    -   An optimized instance locking mechanism is introduced. You can delete tables from an RDS instance by using DROP or TRUNCATE statements even if the RDS instance is locked.
-   Bugs fixed:
    -   The bug that allows you to set the rds\_prepare\_begin\_id option in the `set rds_current_connection` command is fixed.
    -   The bug that prevents the system from updating information about locked accounts is fixed.
    -   The bug that allows you to use actual as a keyword in table names is fixed.
    -   The bug that causes the overflow of timestamps in slow query logs is fixed.

20190510

New feature: The creation of temporary tables in transactions is supported.

20190319

New feature: The configuration of thread IDs in handshake packets is supported.

20190131

-   The upgrade to MySQL 5.7.25 is supported.
-   JeMalloc that is used for memory management is disabled.
-   The bug that causes the system to incorrectly calculate the value of the internal variable net\_lenth\_size is fixed.

20181226

-   New feature: Dynamic modifications to the system variable binlog-row-event-max-size are supported. This allows you to expedite the replication of tables that do not have a primary key.
-   Bug fixed: The bug that prevents the proxy instance of an RDS instance from applying for memory resources is fixed.

20181010

-   Implicit primary keys are supported.
-   The replication of tables that do not have a primary key between primary and secondary RDS instances is accelerated.
-   Native AIO is provided to improve I/O performance.

20180431

New features:

-   The RDS High-availability Edition is supported.
-   The SQL Audit feature is supported. For more information, see [SQL audit]().
-   The protection for RDS instances on which snapshot backups are being created is enhanced.

## ApsaraDB RDS for MySQL 5.7 on RDS Enterprise Edition

20191128

-   New feature:

    The read/write splitting function is supported.

-   Bugs fixed:
    -   The bug that causes the system to incorrectly calculate the value of the Second\_Behind\_Master metric for a follower is fixed.
    -   The bug that causes dead locks during the re-execution of table-level parallel replication transactions is fixed.
    -   XA-related bugs are fixed.

20191016

-   New features:
    -   The upgrade from the RDS High-availability Edition to the RDS Enterprise Edition is supported for RDS instances that use local SSDs.
    -   The GTID function that is provided by the MySQL Community edition is supported. This function is disabled by default.
    -   All of the Alibaba Cloud-proprietary AliSQL features and functions that are released in the RDS Basic and High-availability Editions before the minor version 20190915 are incorporated.
-   Bug fixed:

    The bug that causes the system to disable binary logs for reset secondary RDS instances is fixed.


20190909

-   New features:
    -   The execution of large transactions is accelerated. This applies when the synchronous mode is used to replicate data between primary and secondary RDS instances that run the RDS Enterprise Edition.
    -   The dumping of binary logs from a leader or a follower is supported.
    -   The creation of read-only RDS instances is supported.
    -   The InnoDB storage engine is used for system tables by default.
-   Bugs fixed:
    -   The bug that invalidates the commands that are run by a follower to delete logs is fixed.
    -   The bug that causes slave threads to unexpectedly exit when the slave\_sql\_verify\_checksum parameter is set to OFF and the binlog\_checksum parameter is set to crc32 is fixed.

20190709

New features:

-   The RDS Enterprise Edition is supported.
-   The disabling of the semi-sync plug-in is supported.
-   Table-level parallel replication and write set-level parallel replication are supported.
-   The pk\_access module is introduced to expedite queries that are run based on primary keys.
-   The thread pool feature is supported.
-   All of the Alibaba Cloud-proprietary AliSQL features and functions that are released for MySQL 5.7 in the RDS Basic and High-availability Editions before the minor version 20190510 are incorporated.

## ApsaraDB RDS for MySQL 5.6

20200831

-   New features:

    Various LSNs in the redo log are supported.

    -   innodb\_lsn: the LSN of each record in the redo log.
    -   innodb\_log\_write\_lsn: the LSN of each record that is written into the redo log.
    -   innodb\_log\_checkpoint\_lsn: the LSN of the last checkpoint.
    -   innodb\_log\_flushed\_lsn: the LSN of each record that is flushed from the redo log to the disk.
    -   innodb\_log\_Pages\_flushed: the LSN of each record that logs an update to a page.
-   Bugs fixed:
    -   The bug that causes inappropriate SHOW\_HA\_ROWS enumeration types is fixed.
    -   The bug that causes the system to incorrectly count the value of the IPK field in the procedure context is fixed.
    -   The bug that causes the server to unexpectedly exit when you query data from the INFORMATION\_SCHEMA schema is fixed.
    -   The bug that causes an audit update thread to enter an infinite loop is fixed.
    -   The bug that prevents secondary RDS instances from reporting data replication latencies is fixed.

20200630

-   New features:
    -   The performance agent feature is introduced. For more information, see [Performance Agent](/intl.en-US/Proprietary AliSQL/Stability/Performance Agent.md). This feature is provided as a MySQL plug-in. It allows you to collect and analyze the performance metrics of an RDS instance.
    -   The maximum number of connections that are allowed is increased to 500,000.
    -   The faster DDL feature is introduced. It provides an optimized buffer pool management mechanism. This mechanism reduces the impact of DDL operations and increases the number of concurrent DDL operations that are allowed. For more information, see [Faster DDL](/intl.en-US/Proprietary AliSQL/Stability/Faster DDL.md).
-   Performance optimization:
    -   The global parameter max\_execution\_time is introduced. If the execution duration of an SQL statement exceeds the value of this parameter, the execution is paused.
    -   The thread pool feature is optimized.
-   Bug fixed:

    The bug that causes the system to incorrectly count the number of waits when commands are read from a client is fixed.


20200430

-   The data protection feature is introduced. This feature supports the customization of security policies that are used to manage the permissions on DROP and TRUNCATE statements. This allows you to avoid data losses that are caused by the unintentional execution of these statements. For more information, see [Data Protect](/intl.en-US/Proprietary AliSQL/Security/Data Protect.md).
-   The mdl\_info table is provided to store information about metadata locks.
-   The bug that causes conflicts when the thread pool and ic\_reduce features are both enabled is fixed.

20200331

Performance optimization:

-   The performance of the thread pool feature with the default configuration is improved.
-   The output of TCP errors is disabled by default.

20200229

-   New feature:

    The read/write splitting function is supported for database proxies.

-   Performance optimization:
    -   The thread pool feature is optimized.
    -   The time that is required to execute a PAUSE statement is reduced in various CPU architectures.
-   Bug fixed:

    The bug that causes the system to partially commit XA transactions is fixed.


20200110

-   New feature:

    The thread pool feature is introduced to separate threads from sessions. If a large number of sessions exist, the system can run a small number of threads to complete the tasks in active sessions. For more information, see [Thread Pool](/intl.en-US/Proprietary AliSQL/Feature/Thread Pool.md).

-   Performance optimization:

    The file deletion mechanism is optimized. When you asynchronously delete small files, links to the small files are canceled.

-   Bugs fixed:
    -   The bug that cause the system to incorrectly calculate the sleep time of the page cleaner is fixed.
    -   The bug that causes the `SELECT @@global.gtid_executed` statement to cause a failover failure is fixed.
    -   The bug that causes the [IF CLIENT KILLED AFTER ROLLBACK TO SAVEPOINT PREVIOUS STMTS COMMITTED](https://bugs.mysql.com/bug.php?id=79596) error is fixed.

20191212

Performance optimization:

The deletion of unnecessary TCP error logs is supported.

20191115

Bug fixed:

The bug that causes overflow of timestamps in slow query logs is fixed.

20191101

Bugs fixed:

-   The bug that causes the system to rotate slow query logs when you update common logs is fixed.
-   Some display-related bugs are fixed.

20191015

-   New features:
    -   The rotation of slow query logs is supported. Each CSV slow query log file is assigned a unique name and a new file. This prevents data losses during the collection of slow query logs. You can run the `show variables like '%rotate_log_table%';` command to check whether the rotation of slow query logs is enabled.
    -   A new SM4 encryption algorithm is introduced to replace the original SM4 encryption algorithm.
    -   The Purge Large File Asynchronously feature is introduced to asynchronously delete files. Before you delete a tablespace, the system renames the files in the tablespace as temporary files. Then, a background thread is started to asynchronously delete the temporary files. For more information, see [Purge Large File Asynchronously](/intl.en-US/Proprietary AliSQL/Stability/Purge Large File Asynchronously.md).
    -   The output of TCP errors is supported. TCP errors in read, read-wait, and write-wait events are returned with their error codes by using end\_connection events. In addition, logs with information about the errors are generated.
    -   An SQL log caching mechanism is introduced to increase SQL logging performance.
-   Bugs fixed:
    -   The bug that prevents responses to the pstack command when a large number of connections are established is fixed. This is implemented by disabling the pstack command.
    -   The bug that causes conflicts between implicit primary keys and `CREATE TABLE AS SELECT` statements is fixed.
    -   The bug that prevents the system from automatically deleting the temporary files that are created from binary log files is fixed.

20190815

An optimized instance locking mechanism is introduced. You can delete tables from an RDS instance by using DROP or TRUNCATE statements even if the RDS instance is locked.

20190130

Bugs that compromise database stability are fixed.

20181010

The rocksdb\_ddl\_commit\_in\_the\_middle parameter is introduced to MyRocks. If this parameter is set to on, some DDL statements call the COMMIT operation when they are executed.

201806\*\* \(ApsaraDB RDS for MySQL 5.6.16\)

New feature: Microsecond-level time precision is supported for slow query logs.

20180426 \(ApsaraDB RDS for MySQL 5.6.16\)

-   Invisible indexes are supported. For more information, see [AliSQL 5.6.32 Release Notes \(2017-07-16\)](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2017-07-16)#1-invisible-indexes).
-   The bug that causes the system to apply threads on secondary RDS instances is fixed.
-   The bug that compromises database performance when updates to partitioned tables are applied on secondary RDS instances is fixed.
-   The bug that causes TokuDB to rebuild tables on which ALTER TABLE COMMENT statements are executed is fixed. For more information, see [AliSQL 5.6.32 Release Note \(2018-05-01\)](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2018-05-01)#1-alter-tokudb-table-comment-rebuild-whole-engine-data).
-   The bug that triggers deadlocks when SHOW SLAVE STATUS or SHOW STATUS statements are executed is fixed.

20171205 \(ApsaraDB RDS for MySQL 5.6.16\)

-   The bug that triggers deadlocks when OPTIMIZE TABLE and ONLINE ALTER TABLE statements are executed at the same time is fixed.
-   The bug that triggers conflicts between sequences and implicit primary keys is fixed.
-   The bug that prevents the proper execution of SHOW CREATE SEQUENCE statements is fixed.
-   The bug that causes the system to incorrectly collect statistics on TokuDB tables is fixed.
-   The bug that triggers deadlocks when OPTIMIZE statements are executed in parallel on tables is fixed.
-   The bug that causes the system to incorrectly record character sets in QUERY\_LOG\_EVENT is fixed.
-   The bug that prevents an RDS instance from stopping due to signal processing issues is fixed. For more information, see [AliSQL 5.6.32 Release Notes \(2017-10-10\)](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-%282017-10-10%29#1-the-ack-receiver-thread-didnt-handle-signal-correctly).
-   The bug that is caused by the execution of RESET MASTER statements is fixed.
-   The bug that causes secondary RDS instances to be in a constant waiting state is fixed.
-   The bug that prevents the system from updating the status of primary and secondary RDS instances after primary/secondary switchovers is fixed in the RDS Enterprise Edition.
-   The bug that causes the database process to unexpectedly exit due to the execution of SHOW CREATE TABLE statements is fixed.

20170927 \(ApsaraDB RDS for MySQL 5.6.16\)

The bug that causes the system to query tables from TokuDB based on inappropriate indexes is fixed.

20170901 \(ApsaraDB RDS for MySQL 5.6.16\)

-   New features:
    -   The upgrade of SSL encryption to TLS 1.2 is supported. For more information, see [AliSQL 5.6.32 Release Notes \(2017-10-10\)](https://github.com/alibaba/AliSQL/wiki/Changes-in-AliSQL-5.6.32-(2017-10-10)#2-upgrade-ssl-tlsv12).
    -   Sequences are supported.
-   Bug fixed: The bug that causes the system to return an inaccurate result set for the NOT IN operator is fixed.

20170530 \(ApsaraDB RDS for MySQL 5.6.16\)

New feature: The privileged account of an RDS instance is granted the permissions to close the connections that are established by all of the standard accounts created on the RDS instance.

20170221 \(ApsaraDB RDS for MySQL 5.6.16\)

New feature: The read/write splitting function is supported. For more information, see [Read/write splitting overview]().

## ApsaraDB RDS for MySQL 5.5

20181212

The bug that causes the `gettimeofday(2)` function to return an inaccurate time value is fixed. The returned time value is used to calculate the timeout period. If the returned time value is inaccurate, some operations never time out.

