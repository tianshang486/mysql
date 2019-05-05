# Use mysqldump to migrate MySQL data {#concept_uyq_mn5_ydb .concept}

mysqldump can be used to migrate MySQL data. The disadvantage of mysqldump is that the service downtime is long. Use mysqldump if the data volume is small or if a long service downtime is allowed.

## Background information {#section_lcf_c45_ydb .section}

As RDS is fully compatible with MySQL, the procedure for migrating local databases to an RDS instance is similar to the procedure for migrating data from one MySQL server to another.

## Precautions {#section_ns2_so4_x44 .section}

After the migration, all table names are case-insensitive and lowercase.

## Prerequisites {#section_ats_k45_ydb .section}

-   You have set a whitelist, applied for an Internet IP address, and created databases and accounts for the RDS instance. For more information, see [Quick Start](intl.en-US/User Guide/Quick start.md).
-   An ECS instance has been created.

## Procedure {#section_qhs_m45_ydb .section}

Before data migration, create a migration account in the local database, and grant read and write permissions of the database to the migration account.

1.  Create a migration account in the local database.

    ```
    CREATE USER 'username'@'host' IDENTIFIED BY 'password';
    ```

    Parameter description:

    -   username: indicates the account to be created.
    -   host: indicates the host from which you log on to the database using the account. As a local user, you can use localhost to log on to the database. To log on from any host, you can use the wildcard %.
    -   password: indicates the logon password of the account.
    In the following example, the user name is William and password is Changme123. The user is allowed to log on to the local database from any host.

    ```
    CREATE USER 'William'@'%' IDENTIFIED BY 'Changme123';
    ```

2.  Grant permissions to the migration account in the local database.

    ```
    GRANT SELECT ON databasename.tablename TO 'username'@'host' WITH GRANT OPTION;
    GRANT REPLICATION SLAVE ON databasename.tablename TO 'username'@'host' WITH GRANT OPTION;
    ```

    Parameter description:

    -   privileges: indicates the operating authorization of the account, such as SELECT, INSERT, and UPDATE. To grant all permissions to the account, use ALL.
    -   databasename: indicates the database name. To grant all database permissions to the account, use the wildcard \*.
    -   tablename: indicates the table name. To grant all table permissions to the account, use the wildcard \*.
    -   username: indicates the name of the account to be granted permissions.
    -   host: indicates the host authorized for the account to log on to the database. As a local user, you can use localhost to log on to the database. To log on from any host, you can use the wildcard %
    -   WITH GRANT OPTION: indicates an optional parameter that enables the account to use the `GRANT` command.
    In the following example, the account *William* is granted all database and table permissions:

    ```
    GRANT ALL ON *.* TO 'William'@'%';
    ```

3.  Use the data export tool of mysqldump to export data in the database as data files.

    **Note:** Do not update data during data export. This step is used to export data only, excluding stored procedures, triggers, and functions.

    ```
    mysqldump -h localIp -u userName -p --opt --default-character-set=utf8 --hex-blob dbName --skip-triggers > /tmp/dbName.sql
    ```

    Parameter description:

    -   localIp: IP address of the local database server
    -   userName: Migration account of the local database
    -   dbName: Name of the database to be migrated
    -   /tmp/dbName.sql: Backup file name
4.  Use mysqldump to export stored procedures, triggers, and functions.

    **Note:** If no stored procedures, triggers, and functions are used in the database, you may skip this step. When exporting stored procedures, triggers, and functions, you must remove `definer` for compatibility with RDS.

    ```
    mysqldump -h localIp -u userName -p --opt --default-character-set=utf8 --hex-blob dbName -R | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' > /tmp/triggerProcedure.sql
    ```

    Parameter description:

    -   localIp: IP address of the local database server
    -   userName: Migration account of the local database
    -   dbName: Name of the database to be migrated
    -   /tmp/triggerProcedure.sql: Backup file name
5.  Upload the data files and stored procedure files to ECS.

    The example in this document describes how to upload files to the following path.

    ```
    /tmp/dbName.sql
    /tmp/triggerProcedure.sql
    ```

6.  Log on to ECS and import data files and stored procedure files to the target RDS.

    ```
    mysql -h intranet4example.mysql.rds.aliyuncs.com –u userName -p dbName < /tmp/dbName.sql
    mysql -h intranet4example.mysql.rds.aliyuncs.com -u userName -p dbName < /tmp/triggerProcedure.sql
    ```

    Parameter description:

    -   intranet4example.mysql.rds.aliyuncs.com: RDS instance connection address. An intranet IP address is used as an example.
    -   userName: Migration account of the RDS database
    -   dbName: Name of the database to be imported
    -   /tmp/dbName.sql: Name of the data file to be imported
    -   /tmp/triggerProcedure.sql: Name of the stored procedure file to be imported

