# Migrate data from an ApsaraDB RDS for PostgreSQL database to an on-premises PostgreSQL database

This topic describes how to migrate data from an ApsaraDB RDS for PostgreSQL database to an on-premises PostgreSQL database. You can perform the migration by using a logical backup file.

## Procedure

1.  Connect to the ApsaraDB RDS for PostgreSQL database by using the PostgreSQL client. For more information, visit the [pgAdmin download page](https://www.pgadmin.org/download/).
2.  Run the following command to back up the ApsaraDB RDS for PostgreSQL database:

    ```
    pg_dump -U username -h hostname -p port databasename -f filename --exclude-table=public.ha_health_check
    ```

    Parameter description:

    -   username: the username that is used to log on to the ApsaraDB RDS for PostgreSQL database.
    -   hostname: the name of the host where the ApsaraDB RDS for PostgreSQL database resides.
    -   port: the port number that is used to log on to the ApsaraDB RDS for PostgreSQL database.
    -   databasename: the name of the ApsaraDB RDS for PostgreSQL database.
    -   filename: the name to use for the logical backup file.
    -   --exclude-table=public.ha\_health\_check: specifies to skip the high-availability check.
    Example:

    ```
    pg_dump -U myuser -h rds2z2tp80v3752wb455.pg.rds.aliyuncs.com -p 3433 pg001 -f pg001.sql --exclude-table=public.ha_health_check
    ```

3.  Upload the logical backup file pg001.sql to the server where the on-premises PostgreSQL database resides.
4.  Run the following command to restore data from the logical backup file to the on-premises PostgreSQL database:

    ```
    psql -U username -h hostname -d desintationdb -p port -f dumpfilename.sql
    ```

    Parameter description:

    -   username: the username that is used to log on to the on-premises PostgreSQL database.
    -   hostname: the name of the host where the on-premises PostgreSQL database resides.
    -   port: the port number that is used to log on to the on-premises PostgreSQL database.
    -   desintationdb: the name of the on-premises PostgreSQL database.
    -   dumpfilename: the name of the logical backup file from which you want to restore data.
    Example:

    ```
    psql -U myuser -h localhost -d pg001 -p 5432 -f pg001.sql
    ```

    The ApsaraDB RDS for PostgreSQL database and the on-premises PostgreSQL database have different parameter settings. As a result, some permission-related warnings or errors may occur when you import data into the on-premises PostgreSQL database. You can ignore these warnings and errors. Examples:

    ```
    WARNING:  no privileges could be revoked for "xxxxx"
    ERROR:  role "xxxxx" does not exist
    ```


