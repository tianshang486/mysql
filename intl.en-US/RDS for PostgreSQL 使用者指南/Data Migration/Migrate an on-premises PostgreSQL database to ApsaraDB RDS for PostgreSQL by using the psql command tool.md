# Migrate an on-premises PostgreSQL database to ApsaraDB RDS for PostgreSQL by using the psql command tool {#concept_qhq_gbw_ydb .concept}

This topic describes how to use the psql command to restore the PostgreSQL data backup files to an ApsaraDB for RDS instance.

## Background {#section_rdh_5bw_ydb .section}

PostgreSQL supports logical backups. To import PostgreSQL data, you can export the logical backup files by using the pg\_dump tool and then import the backup files into the ApsaraDB for RDS instance .

## Prerequisites {#section_pbc_vbw_ydb .section}

The database backup of the ApsaraDB for RDS instance has been completed, see [Apply for a public endpoint](../../../../reseller.en-US/Quick Start for PostgreSQL/Initial configuration for RDS for PostgreSQL instances/Apply for a public endpoint.md#) and [Create databases and accounts](../../../../reseller.en-US/Quick Start for PostgreSQL/Initial configuration for RDS for PostgreSQL instances/Create databases and accounts.md#).

## Backup data for the on-premises PostgreSQL database {#section_us5_vbw_ydb .section}

1.  Connect to the on-premises PostgreSQL database through the PostgreSQL client.
2.  Run the following command to back up the data:

    ``` {#codeblock_cjh_sru_yur}
    pg_dump -U username -h hostname -p port databasename -f filename
    ```

    The following list describes the parameters:

    -   username: The username to log on to the on-premises PostgreSQL database.
    -   hostname: The hostname of the on-premises database. You can use *localhost* as the hostname if you log on to the local database host.
    -   port: The port number of the on-premises PostgreSQL database.
    -   databasename: The name of the on-premises database to be backed up.
    -   filename: The name of the backup file to be generated.
    For example, if you want to back up the on-premises PostgreSQL database using the account William, log on to the PostgreSQL database host and run the following command:

    ``` {#codeblock_6ih_dso_6hk}
    pg_dump -U William -h localhost -p 3433 pg001 -f pg001.sql
    ```


## Perform the migration {#section_d1b_1cw_ydb .section}

**Note:** We recommend that you restore data to ApsaraDB for RDS through the internal network connection that is more stable and secure. You can upload the data to the ECS and then restore data to the target ApsaraDB for RDS through the internal network connection. If the data file is too large, you need to compress the file before uploading. The following example describes how to restore data to ApsaraDB for RDS through the internal network connection.

1.  Log on to ECS.
2.  Run the following command through the PostgreSQL client to import the data .

    ``` {#codeblock_jtm_0co_lyx}
    psql -U username -h hostname -d desintationdb -p port -f dumpfilename.sql
    ```

    The following list describes the parameters:

    -   username: The username to log on to the ApsaraDB RDS for PostgreSQL database.
    -   hostname: The hostname of the ApsaraDB RDS for PostgreSQL database.
    -   port: The port number of the ApsaraDB RDS for PostgreSQL database.
    -   desintationdb: The ApsaraDB RDS for PostgreSQL database name.
    -   dumpfilename: The name of the backup file to be restored.
    For example,

    ``` {#codeblock_we5_w2e_ytb}
    psql -U William -h postgresql.rds.aliyuncs.com -d pg001 -p 3433 -f pg001.sql
    ```

    Due to the permission settings of the ApsaraDB RDS for PostgreSQL database are different from those of the on-premises database, some permission-related warnings or errors may occur during the data import. These warnings and errors can be ignored, for example,

    ``` {#codeblock_izl_sgt_2wl}
    WARNING: No privileges could be revoked for "xxxxx".
    ERROR: Role "xxxxx" does not exist.
    ```


