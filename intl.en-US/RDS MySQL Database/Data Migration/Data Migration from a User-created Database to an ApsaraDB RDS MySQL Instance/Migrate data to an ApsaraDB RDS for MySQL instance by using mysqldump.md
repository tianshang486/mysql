# Migrate data to an ApsaraDB RDS for MySQL instance by using mysqldump

mysqldump is easy to use but requires extensive downtime. This tool is suitable for scenarios where the volume of data is small or extensive downtime is allowed.

## Background information

ApsaraDB RDS for MySQL is fully compatible with open source MySQL. The process of migrating data from an open source MySQL database to an ApsaraDB RDS for MySQL instance is similar to that of migrating data from one MySQL server to another.

## Precautions

After migration, table names are all in lowercase and not case-sensitive.

## Prerequisites

-   On the RDS instance, whitelists are configured, the public endpoint is obtained, and databases and accounts are created. For more information, see [Quick start](/intl.en-US/RDS MySQL Database/Quick start/General workflow to use RDS for MySQL.md).
-   An Elastic Compute Service \(ECS\) instance is purchased.

## Procedure

Before you migrate data, create a migration account in the on-premises database, and grant read and write permissions on the database to the migration account.

1.  Create a migration account in the on-premises database.

    ```
    CREATE USER'username'@'host' IDENTIFIED BY 'password';
    ```

    Parameters:

    -   username: the username of the account.
    -   host: the host from which the account is authorized to log on to the database. If you want to allow access from a local host, set the value of this parameter to localhost. If you want to allow access from all hosts, set the value of this parameter to a percent sign \(%\) wildcard.
    -   password: the password of the account.
    For example, you can execute the following statement to create an account William with the password Changme123. The account is authorized to log on to the database from all hosts.

    ```
    CREATE USER'William'@'%' IDENTIFIED BY 'Changme123';
    ```

2.  Grant permissions to the migration account in the on-premises database.

    ```
    GRANT SELECT ON databasename.tablename TO 'username'@'host' WITH GRANT OPTION;
    GRANT REPLICATION SLAVE ON databasename.tablename TO 'username'@'host' WITH GRANT OPTION;
    ```

    Parameters:

    -   privileges: the operation permissions to be granted, such as permissions on SELECT, INSERT, and UPDATE. If you want to grant all permissions to the account, set the value of this parameter to ALL.
    -   databasename: the name of the on-premises database. If you want to grant permissions on all databases \(if any\) to the account, set the value of this parameter to an asterisk \(\*\) wildcard.
    -   tablename: the name of a table. If you want to grant permissions on all tables to the account, set the value of this parameter to an asterisk \(\*\) wildcard.
    -   username: the account to which you want to grant permissions.
    -   host: the host from which the account is authorized to log on to the database. If you want to allow access from a local host, set the value of this parameter to localhost. If you want to allow access from all hosts, set the value of this parameter to a percent sign \(%\) wildcard.
    -   WITH GRANT OPTION: authorizes the account to execute the GRANT statement. This parameter is optional.
    For example, you can execute the following statement to grant permissions on all databases and tables to the William account. The account is authorized to log on to the databases from all hosts.

    ```
    GRANT ALL ON*. * TO 'William'@'%';
    ```

3.  Use mysqldump to export data from the on-premises database to a data file.

    **Note:** Do not update data during the data export. This step exports only data. It does not export stored procedures, triggers, or functions.

    ```
    mysqldump -h localIp -u userName -p --opt --default-character-set=utf8 --hex-blob dbName --skip-triggers --skip-lock-tables > /tmp/dbName.sql
    ```

    Parameters:

    -   localIp: the IP address of the on-premises database server.
    -   userName: the migration account of the on-premises database.
    -   dbName: the name of the source database to be exported.
    -   /tmp/dbName.sql: the name of the data file after export.
4.  Use mysqldump to export stored procedures, triggers, and functions.

    **Note:** If the on-premises database does not have stored procedures, triggers, or functions, skip this step. In this export process, you must remove DEFINER to ensure compatibility with ApsaraDB RDS for MySQL.

    ```
    mysqldump -h localIp -u userName -p --opt --default-character-set=utf8 --hex-blob dbName -R | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' > /tmp/triggerProcedure.sql
    ```

    Parameters:

    -   localIp: the IP address of the on-premises database server.
    -   userName: the migration account of the on-premises database.
    -   dbName: the name of the source database to be exported.
    -   /tmp/triggerProcedure.sql: the name of the stored procedure file after export.
5.  Upload the data and stored procedure files to the ECS instance.

    For this example, upload the files to the following paths:

    ```
    /tmp/dbName.sql
    /tmp/triggerProcedure.sql
    ```

6.  Log on to the ECS instance and import the files to the target RDS instance.

    ```
    mysql -h intranet4example.mysql.rds.aliyuncs.com -u userName -p dbName < /tmp/dbName.sql
    mysql -h intranet4example.mysql.rds.aliyuncs.com -u userName -p dbName < /tmp/triggerProcedure.sql
    ```

    Parameters:

    -   intranet4example.mysql.rds.aliyuncs.com: the endpoint of the RDS instance. In this example, the internal endpoint is used.
    -   userName: the privileged account of the RDS instance or an account that has read/write permissions.
    -   dbName: the name of the destination database to be imported.
    -   /tmp/dbName.sql: the name of the data file to be imported.
    -   /tmp/triggerProcedure.sql: the name of the stored procedure file to be imported.

## FAQ

Q: Data migration by using mysqldump is complex. Is there any simpler method?

A: You can use Data Transmission Service \(DTS\) to migrate data from a user-created MySQL database to an ApsaraDB RDS for MySQL instance. For more information, see [Migrate data from a user-created MySQL database to an ApsaraDB RDS for MySQL instance]().

