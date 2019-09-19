# Migrate data from an RDS for PostgreSQL database to an on-premises PostgreSQL database {#concept_jzm_bzv_ydb .concept}

Migrating data from ApsaraDB RDS for PostgreSQL to an on-premises database by using logical backup files is supported.

## Procedure {#section_ysb_qzv_ydb .section}

1.  Connect the PostgreSQL client to ApsaraDB RDS for PostgreSQL.
2.  Run the following command to back up the data.

    ```
    pg_dump -U username -h hostname -p port databasename -f filename
    ```

    The following list describes the parameters:

    -   username: The username to log on to the ApsaraDB RDS for PostgreSQL database.
    -   hostname: The hostname of the ApsaraDB RDS for PostgreSQL database.
    -   port: The port number of the ApsaraDB RDS for PostgreSQL database.
    -   databasename: The ApsaraDB RDS for PostgreSQL database name that you want to back up.
    -   filename: The name of the backup file to be generated.
    For example,

    ```
    pg_dump -U myuser -h rds2z2tp80v3752wb455.pg.rds.aliyuncs.com -p 3433 pg001 -f pg001.sql
    ```

3.  Save the pg001.sql backup file to the target server.
4.  Run the following command to restore data to the on-premises database:

    ```
    psql -U username -h hostname -d desintationdb -p port -f dumpfilename.sql
    ```

    The following list describes the parameters:

    -   username: The username to log on to the on-premises PostgreSQL database.
    -   hostname: The hostname of the on-premises PostgreSQL database.
    -   port: The port number of the on-premises PostgreSQL database.
    -   desintationdb: The database name of the on-premises PostgreSQL database.
    -   dumpfilename: The name of the backup file to be restored.
    For example,

    ```
    psql -U myuser -h localhost -d pg001 -p 5432 -f pg001.sql
    ```

    Due to the permission settings of the ApsaraDB RDS for PostgreSQL database are different from those of the on-premises database, some permission-related warnings or errors may occur during the data import. These warnings and errors can be ignored, for example,

    ```
    WARNING: No privileges could be revoked for "xxxxx".
    ERROR: Role "xxxxx" does not exist.
    ```


