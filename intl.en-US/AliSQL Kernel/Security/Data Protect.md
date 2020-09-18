# Data Protect

This topic describes the data protection feature provided by ApsaraDB RDS for MySQL. This feature controls permissions to perform high-risk operations.

The instance runs one of the following MySQL versions:

-   MySQL 8.0 \(The [kernel version](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance.md) is 20200430 or later.\)
-   MySQL 5.7 \(The [kernel version](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance.md) is 20200430 or later.\)
-   MySQL 5.6 \(The [kernel version](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance.md) is 20200430 or later.\)

Data protection takes effect on the following database operation commands:

-   High-risk data operation commands
    -   `Drop Table`
    -   `Truncate Table`
    -   `Alter Table Drop Paritition`
    -   `Alter Table Truncate Partition`
    -   `Alter Table Exchange Paritition`
    -   `Drop Tablespace`
-   Extended commands

    -   `DROP View`
    -   `ALTER View`
    -   `Drop Function`
    -   `Drop Procedure`
    -   `Drop Trigger`
    -   `Purge Binary Logs`
    **Note:** Data protection is applied to the extended commands to ensure the running of application code.


## Parameters

The data protection feature involves the following four parameters:

-   rds\_data\_protect\_level

    Specifies the level of data protection. Valid values:

    -   NONE: disables data protection.
    -   DDL: blocks DROP and TRUNCATE operations on databases and tables.
    -   ALL: blocks all DROP and TRUNCATE operations, including the operations on views, stored procedures, functions, and triggers.
    **Note:** We recommend that you configure a data protection level in the non-maintenance or non-publishing phase and disable data protection in the maintenance or publishing phase.

-   rds\_data\_protect\_ignore

    Specifies a list of databases that do not need to be protected. For example, this parameter can be used in scenarios where development and production databases are created on the same RDS instance. You can specify that the development databases are not protected.

-   rds\_data\_protect\_admin

    Specifies which users can delete data when the rds\_data\_protect\_control parameter is set to USER.

-   rds\_data\_protect\_control

    Specifies a data protection policy. The following protection policies are supported:

    -   USER: Only users specified by the rds\_data\_protect\_admin parameter or users who have the SUPER\_ACL permissions can delete data. This value applies to most business scenarios on the cloud.
    -   SUPER: Only users who have the SUPER\_ACL permissions can delete data. You can use SUPER\_ACL to implement precise data protection for common on-premises applications.
    -   MAINTAIN: Only users with the SUPER\_ACL and MAINTAIN permissions can delete data. The MAINTAIN permissions allow users to initiate connections from Alibaba Cloud. This value applies to scenarios where you want to delete data on Alibaba Cloud.
    -   LOCAL: Only users with the SUPER\_ACL and MAINTAIN permissions can delete data by logging on to the instance over local connections. This value applies to core applications. If you configure this value, you cannot delete data by logging on to the instance over remote connections. You must log on to the physical server.

## Enable data protection

Data protection is in the invitational preview. You can [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to enable this feature.

