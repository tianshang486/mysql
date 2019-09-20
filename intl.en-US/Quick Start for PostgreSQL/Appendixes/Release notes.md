# Release notes {#concept_svn_wng_wdb .concept}

This topic provides the release notes of RDS for PostgreSQL versions.

## Release notes 2016-08-01 {#section_tzb_qmg_wdb .section}

PostGIS is upgraded from 2.1.7 to 2.2.2. The default version of the new PostGIS plugin is 2.2.2.

The following command can be used to upgrade the existing PostGIS 2.1.7 plugin.

**Note:** We recommend that you perform application testing before the upgrade to avoid incompatibility between the new PostGIS version and applications.

``` {#codeblock_rnd_peq_yu7}
-- Upgrade PostGIS (includes raster)
ALTER EXTENSION postgis UPDATE TO "2.2.2";
-- Upgrade Topology 
ALTER EXTENSION postgis_topology UPDATE TO "2.2.2"; 
-- Upgrade US Tiger Geocoder
ALTER EXTENSION postgis_tiger_geocoder UPDATE TO "2.2.2";
```

## Release notes 2016-07-01 {#section_ymj_5mg_wdb .section}

Syntax

-   set supports multiple variables, including set par1=val1 and par2=val2.
-   The rds discard all syntax is supported \(including the proxy transparent connection pool, clearing virtual pid and virtual cancel key\).
-   A new syntax is added for rds\_superuser creation: CREATE ROLE | ALTER ROLE | CEATE GROUP xxx \[WITH\] RDS\_SUPERUSER

High availability

-   HA transparent switchover does not require reconnection.
-   Proxy transparency.

Stream replication

-   The WAL Sender rate limiting function is introduced to solve the competition problem of synchronizing the xlog data of multiple instances to network cards.
-   Logical incremental replication is supported through alidecode, enabling incremental replication from RDS to other databases or full replication from MySQL to RDS PG.

Management

-   The maximum length of a row in logger printing is limited to 2 KB to reduce the performance impact caused by frequent and long SQL statements.
-   RDS SUPERUSER is allowed to run CREATE EXTENSION for plugin creation.
-   The max\_connect soft switch is introduced to dynamically adjust the number of connections without restarting the database cluster.
-   The OOM signal is added to asynchronously monitor the memory usage of PG instances. The terminating effect is enhanced to reduce memory overheads.
-   Users with the rds\_superuser permission are allowed to run REASSIGN OWNED BY and other commands.
-   No error is returned when users without the rds\_superuser permission specify tablespace as pg\_default during database creation.
-   The OOM probability is reduced.
-   The storage full issue caused by logs is avoided.

Security

-   The hash index is automatically changed to the b-tree index and the unlogged table is changed to a common table in the kernel to prevent data loss after HA switchover caused by the PostgreSQL replication policy.
-   Common users run CREATE EXTENSION or ALTER EXTENSION without the rds\_superuser permission if a trigger, rule, or function is triggered.
-   Security definer traps \(triggers and rules\) are fixed.
-   The unencrypted password and pg\_hba.conf password is disabled, and the password complexity requirements are increased.
-   The pg\_authid MD5 code security vulnerability is fixed.

Performance

-   Database optimization and data file pre-distribution are supported. Inode write operations and the I/O hang probability are reduced.
-   The checkpoint is optimized. The amount of updated dirty pages is reduced during fsync. The probability of I/O hang caused by dirty page update is reduced when metadata is written due to data=ordered.
-   The clog is optimized. The clog buffer is increased. fsync is implemented at the checkpoint.

Plugin

The extension list is supported.

-   Plugins of the community version

    ``` {#codeblock_yi0_db3_wcz}
     plpgsql,  
     pg_stat_statements,  
     btree_gin,  
     btree_gist,  
     chkpass,  
     citext,  
     cube,  
     dblink,  
     dict_int,  
     earthdistance,  
     hstore,intagg,  
     intarray,  
     isn,  
     ltree,  
     pgcrypto,  
     pgrowlocks,  
     pg_prewarm,  
     pg_trgm,  
     postgres_fdw,  
     sslinfo,  
     tablefunc,  
     tsearch2,  
     unaccent,  
     pgstattuple,  
     "uuid-ossp" NOTE: uuid-ossp must be enclosed by the double quotation marks (" ").
    ```

-   New plugins

    ``` {#codeblock_cn4_89w_fwp}
    postgis,  
     postgis_topology,  
     fuzzystrmatch,  
     postgis_tiger_geocoder,  
     plperl,  
     pltcl,  
     plv8,  
     plls,  
     plcoffee,  
     zhparser, which supports custom word segmentation  
     pgrouting,  
     rdkit,  
     pg_hint_plan,  
     jsonbx,  
     www_fdw,  
     oss_fdw,  
     pg_rewind  
    ```


## Access to other databases of a instance through dblink and postgres\_fdw {#section_wqq_qng_wdb .section}

Monitoring

-   Error: Database error log
-   Space: Available space, data directory space, and XLOG directory space \(archived and unarchived\)
-   Junk data
    -   Table expansion
    -   Index expansion
    -   Deadtuple
    -   Unreferenced large object
-   Running condition
    -   Database age
    -   Long transaction and 2PC
    -   Sequence depletion
    -   Unlogged table
    -   Hash index
-   Performance view
    -   Slave database delay
    -   Stream replication SLOT delay
    -   Cache hit rate
    -   Transaction rollback percentage
    -   Lock wait
    -   Slow SQL
    -   TOP SQL
    -   Connections
    -   Instance memory usage
    -   Instance CPU usage
    -   Instance IOPS usage
-   Configuration
    -   Password expiration time
    -   Configuration inconsistency between master and slave databases
    -   Configuration file inconsistency between master and slave databases

