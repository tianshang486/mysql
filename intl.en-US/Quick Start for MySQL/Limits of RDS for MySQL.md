# Limits of RDS for MySQL {#concept_hb5_px2_vdb .concept}

This topic describes the limits of RDS for MySQL. To guarantee stability and security, you must note the limits when using RDS for MySQL instances.

The following table describes the limits of RDS for MySQL.

|Items|Restrictions|
|-----|------------|
|Parameter modification|The [RDS console](https://rds.console.aliyun.com/) or APIs must be used to modify database parameters. But some parameters cannot be modified. For more information, see [Set parameters through the RDS console](../../../../intl.en-US/User Guide/Instance management/Set instance parameters/Set parameters through the RDS console.md#).|
|Root permission|The root or sa permission is not provided.|
|Backup| -   Command lines or graphical interfaces can be used for logical backup.
-   For physical backup, the [RDS console](https://rds.console.aliyun.com/) or APIs must be used.

 |
|Restoration| -   Command lines or graphical interfaces can be used for logical restoration.
-   For physical restoration, the [RDS console](https://rds.console.aliyun.com/) or APIs must be used.

 |
|Migration| -   Command lines or graphical interfaces can be used for logical import.
-   You can use the MySQL command line tool or Data Transmission Service \(DTS\) to migrate data.

 |
|MySQL storage engine| -   Currently only InnoDB and TokuDB are supported. The MyISAM engine has defects and may cause data loss. If you create MyISAM engine tables, they are automatically converted to InnoDB engine tables. For more information, see [Why does RDS for MySQL not support the MyISAM engine?](https://www.alibabacloud.com/help/doc-detail/52558.htm)
-   The InnoDB storage engine is recommended for performance and security requirements.
-   The Memory engine is not supported. If you create Memory engine tables, they are automatically converted to InnoDB engine tables.

 |
|Replication|MySQL provides a dual-node cluster based on the master/slave replication architecture, so you manual deployment is not required. The slave instance in the architecture is invisible to you, and your application cannot access to the slave instance directly.|
|Restarting RDS instances|Instances must be restarted through the [RDS console](https://rds.console.aliyun.com/) or APIs.|
|User, password, and database management|By default, [RDS console](https://rds.console.aliyun.com/) is used to manage users, passwords, and databases, including operations such as instance creation, instance deletion, permission modification, and password modification. MySQL also allows you to create a master account for finer-grained management.|
|Common account| -   Does not support customized authorization.
-   The account management and database management interfaces are provided on the RDS console.
-   Instances that support common accounts also support master accounts.

 |
|Master account| -   Support customized authorization.
-   SQL statements can be used for management.

 |
|Network settings|If a MySQL 5.5/5.6 instance is in a classic network and its [access mode](../../../../intl.en-US/User Guide/Connection management/Disabling the database proxy mode.md) is safe connection mode, do not enable net.ipv4.tcp\_timestamps in SNAT mode.|

