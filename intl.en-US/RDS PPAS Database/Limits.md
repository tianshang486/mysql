# Limits

Before you use ApsaraDB RDS for PPAS, you must understand its limits and take the necessary precautions.

The following table lists the limits of ApsaraDB RDS for PPAS.

|Item|Limit|
|----|-----|
|Database parameter reconfiguration|Not supported.|
|Root permissions of databases|ApsaraDB RDS for PPAS does not provide superuser accounts.|
|Database backup|Data can be backed up only by using the pg\_dump plug-in.|
|Data import|Backed up data can be restored only by using the psql plug-in.|
|Database replication|-   The system automatically builds High-availability \(HA\) database systems based on PPAS streaming replication.
-   Secondary RDS instances are hidden and cannot be directly accessed. |
|Instance restart|RDS instances must be restarted by using the ApsaraDB for RDS console or API operations.|

