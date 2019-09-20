# Limits of RDS for PostgreSQL {#concept_zvw_n1g_wdb .concept}

This topic describes the limits of RDS for PostgreSQL. To guarantee stability and security, you must note the limits when using RDS for PostgreSQL instances.

The following table describes the limits of RDS for PostgreSQL.

|Operations|RDS restrictions|
|----------|----------------|
|Modify database parameter settings|Currently it is not supported.|
|Database root permission|RDS does not offer the superuser permission.|
|Database backup|Data backup can only be performed through pg\_dump.|
|Data migration|Data backed up through pg\_dump can only be restored through psql.|
|Build database replication| The system automatically builds the HA mode based on PostgreSQL stream replication.

 The PostgreSQL standby node is invisible and cannot be accessed directly.

 |
|Restart the RDS instance|The instance must be restarted through the RDS console or OpenAPI.|
|Network setting|If the [access mode](../../../../intl.en-US/User Guide/Connection management/Disabling the database proxy mode.md#) of the instance is safe connection mode, enabling net.ipv4.tcp\_timestamps in SNAT mode is not allowed.|

