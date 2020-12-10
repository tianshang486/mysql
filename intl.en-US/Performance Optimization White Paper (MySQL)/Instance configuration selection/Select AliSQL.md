# Select AliSQL

AliSQL is an independent MySQL branch that is developed by Alibaba Cloud based on the MySQL Community edition. AliSQL provides more further enhanced features than the MySQL Community edition.

AliSQL is an independent MySQL branch that is developed by Alibaba Cloud. AliSQL provides all of the features that are available in the MySQL Community edition. AliSQL also provides some similar features that you can find in the MySQL Enterprise edition. These similar features include enterprise-grade backup and restoration, thread pool, and parallel query. In addition, AliSQL provides Oracle-compatible features, such as the Sequence engine. ApsaraDB RDS for MySQL with AliSQL provides all the basic features of MySQL and a wide range of advanced features. These advanced features include enterprise-grade security, backup and restoration, monitoring, performance optimization, and read-only instance.

AliSQL encompasses a wide range of innovations that are engineered to optimize the functionality, performance, stability, and security of ApsaraDB RDS for MySQL. These innovations include the following features that are designed to optimize performance:

-   [A new version is available.](/intl.en-US/Proprietary AliSQL/Performance/Fast query cache.md)

    The fast query cache is developed by Alibaba Cloud based on the native MySQL query cache. The fast query cache uses a new design and implementation mechanism to optimize concurrency control, memory management, and caching. These optimizations increase query performance.

-   [Binlog in Redo](/intl.en-US/Proprietary AliSQL/Performance/Binlog in Redo.md)

    The Binlog in Redo feature allows ApsaraDB RDS for MySQL to synchronously write binary logs into the redo log file when transactions are committed. This reduces operations on disks and increases database performance.

-   [Statement Queue](/intl.en-US/Proprietary AliSQL/Performance/Statement Queue.md)

    The statement queue feature allows statements to queue in the same bucket. These statements may be executed on the same resources. For example, these statements are executed on the same row of a table. This reduces overheads that are caused by potential conflicts.

-   [Inventory Hint](/intl.en-US/Proprietary AliSQL/Performance/Inventory Hint.md)

    In business scenarios such as seckilling, inventory reduction is a common task model that requires high concurrency and serialization. In this model, AliSQL uses queues and transactional hints to control concurrency and to commit or roll back transactions at fast speeds. This increases the throughput of your business.


For more information about the AliSQL features that are supported by different MySQL versions, see [Overview of AliSQL features](/intl.en-US/Proprietary AliSQL/Overview of AliSQL features.md).

