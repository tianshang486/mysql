# Best practices of X-Engine

This topic describes the best practices of X-Engine, which uses a tiered storage architecture.

The tiered storage architecture of X-Engine is ideal for the following services:

-   Accesses to data show distinct time characteristics. For example, most of the read and update operations are performed on the recently written data instead of on the historical data. X-Engine caches the recently written data in the memory and uses an efficient structure to index the data. This significantly expedites data reads and writes. The rarely accessed historical data is stored on disks. As a result, the read/write performance for the historical data is slightly inferior to that for the recently written data.
-   The volume of data in your tables and databases is large. The disk space that is required to store the data in X-Engine is 10% to 50% of the disk space that is required to store the data in InnoDB. The reduction in disk usage varies based on the data characteristics. After you migrate the data from InnoDB to X-Engine, you do not need to shard your databases or tables. You can store up to 10 TB of data in a single database.

As a leading e-commerce service provider in China, Alibaba Group serves a large user base. A number of online services that are offered by Alibaba Group require huge storage costs. The following sections provide the use cases of X-Engine within Alibaba Group.

**Note:**

-   For more information about X-Engine, see [Usage notes](/intl.en-US/Proprietary AliSQL/X-Engine/Usage notes.md).
-   For more information about how to convert tables from InnoDB to X-Engine in , see [Convert the storage engine of DRDS from InnoDB to X-Engine](/intl.en-US/Proprietary AliSQL/Best practices/Convert the storage engine of DRDS from InnoDB to X-Engine.md).

## Manage historical transaction orders for Tmall at Taobao

Taobao is a leading online seller in China, and Tmall is a dedicated business-to-consumer \(B2C\) platform of Taobao. If InnoDB is used, the database instance that is used to store the historical transaction orders of all Tmall users faces the following challenges:

-   Trillions of data records need petabytes of disk space.
-   Highly concurrent write requests need instant responses during sales promotions.

If you cannot scale out the single database instance to meet the requirements of this large data volume, you can create more database instances to improve performance and increase storage capacity. However, this makes operations and maintenance \(O&M\) and management more complicated and increases storage costs.

X-Engine provides a compact page-based storage format and an efficient compression algorithm. This allows you to store and process up to 20 TB of raw datasets. The volume of data that can be processed per instance when X-Engine is used is three times higher than when InnoDB is used.

Accesses to data in transaction order databases show the following characteristic: Recently generated data records are frequently updated and read. X-Engine supports the separation of hot data from cold data. It caches the recently generated data records into the memory and properly indexes the data records. This ensures that the data records are processed at high speeds and low latencies.

For more information, see [Storage engine that processes trillions of Taobao orders](/intl.en-US/Proprietary AliSQL/Best practices/Storage engine that processes trillions of Taobao orders.md).

## Manage chat history for DingTalk

DingTalk is a leading enterprise-level instant messaging \(IM\) tool that serves hundreds of millions of users in China. Unlike a traditional user-level IM tool, an enterprise-level IM tool must store the chat history permanently and allow a single user to log on to multiple terminals at the same time. As the user base and chat history grow explosively, DingTalk faces great challenges to reduce storage costs and maintain stable read/write performance.

At the early development stage when InnoDB was used, the DingTalk team considered various solutions to reduce storage costs. These solutions included NoSQL services such as HBase. However, enterprise-level IM requires strict data consistency and relies on advanced database features, such as secondary indexing, to handle diverse workloads.

After X-Engine is introduced, the disk usage drops by 62%. In addition, X-Engine supports advanced database features, such as transaction processing and secondary indexing. The DingTalk team can migrate the chat history to X-Engine without the need to modify code.

For more information, see [DingTalk secures App Store top rank with X-Engine](/intl.en-US/Proprietary AliSQL/Best practices/DingTalk secures App Store top rank with X-Engine.md).

## Manage image space for Alibaba Group

Alibaba Group offers a free image space service. This service is used by Taobao and Tmall sellers to store and manage a large volume of images. However, this service faces great challenges to increase storage capacity and improve write performance, especially prior to Double 11 when the data volume surges because sellers frequently update the Stock Keeping Units \(SKUs\) of their items.

Most of the metadata of the images that are stored in the image space is text. The metadata includes URL attributes. X-Engine provides a prefix compression algorithm that is best suited to this scenario. This algorithm works with the compact page-based storage format and other common compression algorithms to compress the metadata at a high compression ratio. After the image space service is migrated from InnoDB to X-Engine, the disk usage drops by six sevenths.

In addition to saving petabytes of disk space, X-Engine offers a stable rate of transactions per second \(TPS\) that is comparable to the TPS provided by InnoDB. X-Engine also offers a response latency that is acceptable to online services.

