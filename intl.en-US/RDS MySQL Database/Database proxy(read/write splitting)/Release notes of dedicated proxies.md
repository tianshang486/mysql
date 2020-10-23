# Release notes of dedicated proxies

This topic describes the release notes of dedicated proxies.

**Note:** For more information about the minor engine versions of ApsaraDB RDS for MySQL, see [Release notes of minor AliSQL versions](/intl.en-US/Proprietary AliSQL/Release notes of minor AliSQL versions.md).

## View the dedicated proxy version

If you are not using the latest dedicated proxy version, click **Upgrade Dedicated Proxy Version** on the **Database Proxy** page of your RDS instance. In the dialog box that appears, you can view **Current Version** and **Available Upgrade** of your RDS instance.

**Note:** If you are using the latest dedicated proxy version, the Upgrade Dedicated Proxy Version button does not appear. You can also call an API operation to view the dedicated proxy version. For more information, see [Query dedicated proxy details](/intl.en-US/API Reference/Database proxy/Query dedicated proxy details.md).

![View the dedicated proxy version of an RDS instance](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7723243061/p173582.png)

## Release notes

-   1.12.7
    -   New features:
        -   The `SHOW FULL PROCESSLIST` statement is supported.
        -   The XA transactions are supported.
    -   Bugs fixed:
        -   The bug that prevents the `SHOW PROCESSLIST` statement from being executed on RDS instances that run MySQL 8.0 is fixed.
        -   Some bugs that are related to transaction connection pools are fixed.
        -   Some bugs that prevent connections from being established are fixed.
-   1.11.12
    -   New feature:

        [Transaction connection pools](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Connection pool.md) are supported.

    -   Bugs fixed:
        -   Load balancing on persistent connections is optimized. After an RDS instance is restored from an abnormal state to a normal state, new requests that are initiated over the previous persistent connection are routed to the RDS instance.
        -   The PREPARE statement is optimized. The PREPARE statement can be sent in unicast mode.
        -   The bug that causes connection failures between MySQL 5.7 databases and MySQL 5.6 databases when the Deprecate EOF function is enabled is fixed.
        -   The bug that causes disconnections when stored procedures are called to modify databases of an RDS instance is fixed.
        -   The bug that causes a client to report the `Packets out of order` error message when a single row in a result set exceeds 16 MB in size is fixed.
        -   The bug that causes failures to end the transactions that are started by using the `SET autocommit=0` statement on a read-only RDS instance in a timely manner is fixed.
        -   The bug that causes a statement where `LOCK IN SHARE MODE` is specified to be routed to a read-only RDS instance is fixed.
        -   The bug that causes the `SELECT handler FROM abc` statement where FOR UPDATE is specified to be routed to a read-only RDS instance is fixed.
        -   The bug that causes failures in authenticating a user from more than one host is fixed.
-   1.10.7

    Bugs fixed:

    Some bugs that are related to session connection pools are fixed.

-   1.9.23
    -   New features:
        -   Connections to RDS instances by using the credentials of the root user are supported.
        -   SSL connections are supported.
    -   Bugs fixed:
        -   The bug that causes failures to run the `change user` command is fixed.
        -   The bug that causes failures to run the `load file` command is fixed.
        -   The bug that causes a client to report the `Exception: Packets out of order` error message after the client receives a packet that is not in the expected order is fixed.
        -   The bug that causes a read-only RDS instance to be disconnected when its primary RDS instance is in an abnormal state is fixed.
-   1.9.14
    -   New feature:

        The `/*FORCE_SLAVE*/, /*FORCE_MASTE*/` hint is supported.

    -   Bugs fixed:
        -   The bug that causes garbled characters if the default value of the charset parameter is invalid is fixed.
        -   The bug that causes an invalid string is returned for the MySQL version is fixed.

