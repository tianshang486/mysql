# High-availability Edition {#concept_1443745 .concept}

RDS instances are divided into Basic Edition, High-availability Edition, Cluster Edition, and Three-node Enterprise Edition. This topic describes High-availability Edition.

High-availability Edition is a widely used database edition that uses a primary/secondary architecture to implement high availability. High-availability Edition is suitable for over 80% of user scenarios such as the Internet, IoT, retail e-commerce, logistics, and gaming.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1148653/156577162154376_en-US.png)

## Topology {#section_8tb_m8n_26x .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1148653/156577162153963_en-US.png)

## Benefits {#section_b3n_xqz_nld .section}

**High availability**

High-availability Edition instances each have a secondary instance. Data between the primary and secondary instances is synchronized in real time. If the primary instance cannot be accessed, your business is automatically switched to the secondary instance.

**Comprehensive features**

High-availability Edition instances provide comprehensive features such as auto scaling, backup and restoration, performance optimization, and read/write splitting. The instances also provide the SQL explorer feature to query SQL execution records. This feature makes database access traceable and ensures the security of core data.

## Upgrade to High-availability Edition {#section_41j_10c_sl8 .section}

Basic Edition instances do not have secondary instances for hot backup. Therefore, when a Basic Edition instance fails, changes specifications, or upgrades the version, it may remain unavailable for a long period of time. We recommend that you use High-availability Edition instances if your business has high database availability requirements.

In addition to creating new High-availability Edition instances, you can also upgrade existing Basic Edition instances to High-availability Edition instances to avoid having to migrate data and release instances.

**Note:** 

-   RDS for MySQL 5.7 Basic Edition instances can be upgraded to High-availability Edition instances. For more information, see [Change configurations](../../../../intl.en-US/User Guide/Instance management/Change configurations.md#).
-   RDS for SQL Server Basic Edition instances can be upgraded to High-availability Edition instances in the console. For more information, see [Upgrade from Basic Edition to High-availability Edition](https://www.alibabacloud.com/help/zh/doc-detail/127275.htm).

