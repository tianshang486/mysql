# Release notes of dedicated proxy versions

This topic describes the release notes of dedicated proxy versions.

**Note:** For more information about the minor engine versions of ApsaraDB RDS for MySQL, see [Release notes of minor AliSQL versions](/intl.en-US/Proprietary AliSQL/Release notes of minor AliSQL versions.md).

## View the dedicated proxy version of your RDS instance

If you are not using the latest dedicated proxy version, click **Upgrade Dedicated Proxy Version** on the **Database Proxy** page of your RDS instance. In the dialog box that appears, you can view the current dedicated proxy version \(**Current Version**\) and the available dedicated proxy version \(**Available Upgrade**\).

**Note:** If you are using the latest dedicated proxy version, the Upgrade Dedicated Proxy Version button does not appear. You can also call an API operation to view the dedicated proxy version. For more information, see [Query dedicated proxy details](/intl.en-US/API Reference/Database proxy/Query dedicated proxy details.md).

![View the dedicated proxy version of an RDS instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0885047061/p173582.png)

## Release notes

|Dedicated proxy version|Description|
|-----------------------|-----------|
|1.12.7|-   New features:
    -   The `SHOW FULL PROCESSLIST` statement is supported.
    -   The syntax for XA transactions is supported.
-   Bugs fixed:
    -   The bug that causes errors in executing the `SHOW PROCESSLIST` statement on an RDS instance is fixed. This exception occurs if the RDS instance runs MySQL 8.0.
    -   Some bugs that are related to transaction connection pools are fixed.
    -   Some bugs that prevent connections from being established are fixed. |
|1.11.12|-   New feature:

Transaction connection pools are supported. For more information, see [Connection pool](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Connection pool.md).

-   Bugs fixed:
    -   The bug that prevents new requests over the previous persistent connections to an RDS instance from being routed to the RDS instance is fixed. This exception occurs if the RDS instance is restored from an abnormal state to a normal state. The bug is fixed by optimizing the mechanism that is used to balance loads among persistent connections.
    -   The but that prevents the PREPARE statement from being sent in unicast mode is fixed by optimizing the syntax of the PREPARE statement.
    -   The bug that causes failures in connecting MySQL 5.7 databases and MySQL 5.6 databases when the Deprecate EOF feature is enabled is fixed.
    -   The bug that causes disconnections to an RDS instance when stored procedures are called to modify the RDS instance is fixed.
    -   The bug that causes a client to report the `Packets out of order` error message when the size of a single row in a result set exceeds 16 MB is fixed.
    -   The bug that causes failures in terminating the transactions that are started by using the `SET autocommit=0` statement on a read-only RDS instance in a timely manner is fixed.
    -   The bug that causes a statement to be routed to a read-only RDS instance is fixed. This exception occurs if the statement has `LOCK IN SHARE MODE` specified.
    -   The bug that causes the `SELECT handler FROM abc` statement to be routed to a read-only RDS instance is fixed. This exception occurs if the statement has FOR UPDATE specified.
    -   The bug that causes failures in authenticating a user from more than one host is fixed. |
|1.10.7|Bugs fixed:

Some bugs that are related to session connection pools are fixed. |
|1.9.23|-   New features:
    -   Connections to RDS instances by using the credentials of the root user are supported.
    -   SSL connections are supported.
-   Bugs fixed:
    -   The bug that causes failures in running the `change user` command is fixed.
    -   The bug that causes failures in running the `load file` command is fixed.
    -   The bug that causes a client to report the `Exception: Packets out of order` error message is fixed. This exception occurs if the client receives a packet that is not in the expected order.
    -   The bug that causes a read-only RDS instance to be disconnected when its primary RDS instance is in an abnormal state is fixed. |
|1.9.14|-   New feature:

The `/*FORCE_SLAVE*/` and /\*FORCE\_MASTE\*/ hints are supported.

-   Bugs fixed:
    -   The bug that causes garbled characters if the default value of the charset parameter is invalid is fixed.
    -   The bug that causes the system from returning an invalid string for the MySQL version is fixed. |

