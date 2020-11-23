# Features of ApsaraDB RDS for SQL Server

This topic provides an overview of the features that are supported in different SQL Server versions, RDS editions, and storage types of ApsaraDB RDS for SQL Server.

**Note:** In the following tables, the check sign \(√\) indicates that the feature is supported, and the cross sign \(×\) indicates that the feature is not supported.

## SQL Server 2019

|Category|Feature|SQL Server 2019|
|SE|
|RDS High-availability Edition|
|Standard SSD|ESSD, ESSD PL2, or ESSD PL3|
|--------|-------|---------------|
|--|
|-----------------------------|
|------------|---------------------------|
|Data migration|[Migrate the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Data migration/Data migration solutions.md)|√|√|
|Instance management|[Create an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Change the specifications of an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Change the specifications of an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Migrate an RDS instance across zones](/intl.en-US/RDS SQL Server Database/Instance/Migrate an ApsaraDB RDS for SQL Server instance across zones in the same region.md)|×|×|
|[Switch over services between primary and secondary RDS instances](/intl.en-US/RDS SQL Server Database/Instance/Perform a manual or automatic switchover of services between primary and secondary ApsaraDB RDS for SQL Server instances.md)|√|√|
|[Restart an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Restart an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Set the maintenance window of an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Set the maintenance window of an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Release an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Release or unsubscribe from an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Manage ApsaraDB RDS for SQL Server instances in the recycle bin](/intl.en-US/RDS SQL Server Database/Instance/Manage ApsaraDB RDS for SQL Server instances in the recycle bin.md)|√|√|
|[DBCC](/intl.en-US/RDS SQL Server Database/Instance/DBCC features of ApsaraDB RDS for SQL Server.md)|√|√|
|Account management|[Create an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Create an account for an RDS SQL Server instancy.md)|√|√|
|[Reset the password of an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Reset the password of an account on an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Modify the permissions of an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Modify the permissions of a standard account on an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Authorize the service account of an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Authorize a service account for an ApsaraDB RDS for SQL Server instance.md)|×|×|
|[Delete an account from an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Delete an account for an RDS SQL Server instance.md)|√|√|
|Database management|[Create a database on an RDS instance](/intl.en-US/RDS SQL Server Database/Database/Create a database on an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Delete a database from an RDS instance](/intl.en-US/RDS SQL Server Database/Database/Delete a database from an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Copy a database between RDS instances](/intl.en-US/RDS SQL Server Database/Database/Database replication/Copy a database of ApsaraDB RDS SQL Server 2012 or later.md)|√|√|
|Database connection|[Connect to an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Connect to an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Configure an endpoint for an RDS instance]()|√|√|
|[View the endpoints and ports of an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Apply for a public endpoint for an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/Apply for or release a public endpoint on an ApsaraDB RDS for SQL Server instance.md)|√|√|
|Monitoring and alerting|[View the monitoring data of an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Set the monitoring frequency of an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/Set the monitoring frequency.md)|√|√|
|[Configure an alert rule for an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for SQL Server instance.md)|√|√|
|Network management|[Change the network type of an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/Change the network type of an ApsaraDB RDS for SQL Server instance.md)|×|×|
|Read-only instance and read/write splitting|[Create a read-only RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Read-only instances/Overview of read-only ApsaraDB RDS for SQL Server instances.md)|×|×|
|[Enable read/write splitting for an RDS instance](/intl.en-US/RDS SQL Server Database/Read/write splitting/Read/write splitting overview.md)|×|×|
|[Modify the read weights of read-only RDS instances](/intl.en-US/RDS SQL Server Database/Read/write splitting/Modify the read weights.md)|×|×|
|Security management|[Control access to an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Configure a whitelist for an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Configure SSL encryption for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure SSL encryption on an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Configure TDE for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure TDE for an ApsaraDB RDS for SQL Server instance.md)|×|×|
|[Configure a distributed transaction whitelist for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure a distributed transaction whitelist for an ApsaraDB RDS for SQL Server instance.md)|√|√|
|Audit|[View the logs of an RDS instance](/intl.en-US/RDS SQL Server Database/Audit/Manage logs.md)|×|×|
|Backup|[Back up the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[t1986080.md\#]()|√|√|
|[Free quota for backup storage](/intl.en-US/RDS SQL Server Database/Backup/View the free quota for backup usage of an ApsaraDB RDS for SQL Server instance.md)|√|√|
|[Download a backup file of an RDS instance](/intl.en-US/RDS SQL Server Database/Backup/Download data and log backup files from an ApsaraDB RDS for SQL Server instance.md)|√|√|
|Restoration|[Restore the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Restoration/Restore the data of an ApsaraDB RDS for SQL Server instance.md)|√|√|
|Tag management|[Create tags](/intl.en-US/RDS SQL Server Database/Tag/Create tags.md)|√|√|
|[Delete tags](/intl.en-US/RDS SQL Server Database/Tag/Delete tags.md)|√|√|
|[Use tags to filter ApsaraDB RDS for SQL Server instances](/intl.en-US/RDS SQL Server Database/Tag/Use tags to filter ApsaraDB RDS for SQL Server instances.md)|√|√|

## SQL Server 2017

|Category|Feature|SQL Server 2017|
|EE|SE|
|RDS Cluster Edition|RDS High-availability Edition|
|Standard SSD|ESSD, ESSD PL2, or ESSD PL3|Standard SSD|ESSD, ESSD PL2, or ESSD PL3|
|--------|-------|---------------|
|--|--|
|-------------------|-----------------------------|
|------------|---------------------------|------------|---------------------------|
|Data migration|[Migrate the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Data migration/Data migration solutions.md)|√|√|√|√|
|Instance management|[Create an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Change the specifications of an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Change the specifications of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Migrate an RDS instance across zones](/intl.en-US/RDS SQL Server Database/Instance/Migrate an ApsaraDB RDS for SQL Server instance across zones in the same region.md)|×|×|×|×|
|[Switch over services between primary and secondary RDS instances](/intl.en-US/RDS SQL Server Database/Instance/Perform a manual or automatic switchover of services between primary and secondary ApsaraDB RDS for SQL Server instances.md)|√|√|√|√|
|[Restart an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Restart an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Set the maintenance window of an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Set the maintenance window of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Release an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Release or unsubscribe from an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Manage ApsaraDB RDS for SQL Server instances in the recycle bin](/intl.en-US/RDS SQL Server Database/Instance/Manage ApsaraDB RDS for SQL Server instances in the recycle bin.md)|√|√|√|√|
|[DBCC](/intl.en-US/RDS SQL Server Database/Instance/DBCC features of ApsaraDB RDS for SQL Server.md)|√|√|√|√|
|Account management|[Create an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Create an account for an RDS SQL Server instancy.md)|√|√|√|√|
|[Reset the password of an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Reset the password of an account on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Modify the permissions of an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Modify the permissions of a standard account on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Authorize the service account of an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Authorize a service account for an ApsaraDB RDS for SQL Server instance.md)|×|×|×|×|
|[Delete an account from an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Delete an account for an RDS SQL Server instance.md)|√|√|√|√|
|Database management|[Create a database on an RDS instance](/intl.en-US/RDS SQL Server Database/Database/Create a database on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Delete a database from an RDS instance](/intl.en-US/RDS SQL Server Database/Database/Delete a database from an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Copy a database between RDS instances](/intl.en-US/RDS SQL Server Database/Database/Database replication/Copy a database of ApsaraDB RDS SQL Server 2012 or later.md)|√|√|√|√|
|Database connection|[Connect to an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Connect to an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Configure an endpoint for an RDS instance]()|√|√|√|√|
|[View the endpoints and ports of an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Apply for a public endpoint for an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/Apply for or release a public endpoint on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|Monitoring and alerting|[View the monitoring data of an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Set the monitoring frequency of an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/Set the monitoring frequency.md)|√|√|√|√|
|[Configure an alert rule for an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|Network management|[Change the network type of an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/Change the network type of an ApsaraDB RDS for SQL Server instance.md)|×|×|×|×|
|Read-only instance and read/write splitting|[Create a read-only RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Read-only instances/Overview of read-only ApsaraDB RDS for SQL Server instances.md)|√|√|×|×|
|[Enable read/write splitting for an RDS instance](/intl.en-US/RDS SQL Server Database/Read/write splitting/Read/write splitting overview.md)|√|√|×|×|
|[Modify the read weights of read-only RDS instances](/intl.en-US/RDS SQL Server Database/Read/write splitting/Modify the read weights.md)|√|√|×|×|
|Security management|[Control access to an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Configure a whitelist for an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Configure SSL encryption for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure SSL encryption on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Configure TDE for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure TDE for an ApsaraDB RDS for SQL Server instance.md)|√|√|×|×|
|[Configure a distributed transaction whitelist for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure a distributed transaction whitelist for an ApsaraDB RDS for SQL Server instance.md)|×|×|√|√|
|Audit|[View the logs of an RDS instance](/intl.en-US/RDS SQL Server Database/Audit/Manage logs.md)|×|×|×|×|
|Backup|[Back up the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[t1986080.md\#]()|√|√|√|√|
|[Free quota for backup storage](/intl.en-US/RDS SQL Server Database/Backup/View the free quota for backup usage of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|[Download a backup file of an RDS instance](/intl.en-US/RDS SQL Server Database/Backup/Download data and log backup files from an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|Restoration|[Restore the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Restoration/Restore the data of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|
|Tag management|[Create tags](/intl.en-US/RDS SQL Server Database/Tag/Create tags.md)|√|√|√|√|
|[Delete tags](/intl.en-US/RDS SQL Server Database/Tag/Delete tags.md)|√|√|√|√|
|[Use tags to filter ApsaraDB RDS for SQL Server instances](/intl.en-US/RDS SQL Server Database/Tag/Use tags to filter ApsaraDB RDS for SQL Server instances.md)|√|√|√|√|

## SQL Server 2016

|Category|Feature|SQL Server 2016|
|EE|SE|WEB|
|RDS High-availability Edition|RDS Basic Edition|RDS High-availability Edition|RDS Basic Edition|
|Standard SSD|ESSD, ESSD PL2, or ESSD PL3|Standard SSD|ESSD|Standard SSD|ESSD, ESSD PL2, or ESSD PL3|Standard SSD|ESSD|
|--------|-------|---------------|
|--|--|---|
|-----------------------------|-----------------|-----------------------------|-----------------|
|------------|---------------------------|------------|----|------------|---------------------------|------------|----|
|Data migration|[Migrate the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Data migration/Data migration solutions.md)|√|√|√|√|√|√|√|√|
|Instance management|[Create an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Change the specifications of an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Change the specifications of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Migrate an RDS instance across zones](/intl.en-US/RDS SQL Server Database/Instance/Migrate an ApsaraDB RDS for SQL Server instance across zones in the same region.md)|×|×|×|×|×|×|×|×|
|[Switch over services between primary and secondary RDS instances](/intl.en-US/RDS SQL Server Database/Instance/Perform a manual or automatic switchover of services between primary and secondary ApsaraDB RDS for SQL Server instances.md)|√|√|×|×|√|√|×|×|
|[Restart an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Restart an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Set the maintenance window of an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Set the maintenance window of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Release an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Release or unsubscribe from an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Manage ApsaraDB RDS for SQL Server instances in the recycle bin](/intl.en-US/RDS SQL Server Database/Instance/Manage ApsaraDB RDS for SQL Server instances in the recycle bin.md)|√|√|√|√|√|√|√|√|
|[DBCC](/intl.en-US/RDS SQL Server Database/Instance/DBCC features of ApsaraDB RDS for SQL Server.md)|√|√|√|√|√|√|√|√|
|Instance upgrade|[Upgrade an RDS instance from the Basic Edition to the High-availability Edition](/intl.en-US/RDS SQL Server Database/Version upgrade/Upgrade from Basic Edition to High-availability Edition.md)|×|×|√|√|×|×|√|√|
|Account management|[Create an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Create an account for an RDS SQL Server instancy.md)|√|√|√|√|√|√|√|√|
|[Reset the password of an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Reset the password of an account on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Modify the permissions of an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Modify the permissions of a standard account on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Authorize the service account of an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Authorize a service account for an ApsaraDB RDS for SQL Server instance.md)|×|×|×|×|×|×|×|×|
|[Delete an account from an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Delete an account for an RDS SQL Server instance.md)|√|√|√|√|√|√|√|√|
|Database management|[Create a database on an RDS instance](/intl.en-US/RDS SQL Server Database/Database/Create a database on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Delete a database from an RDS instance](/intl.en-US/RDS SQL Server Database/Database/Delete a database from an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Copy a database between RDS instances](/intl.en-US/RDS SQL Server Database/Database/Database replication/Copy a database of ApsaraDB RDS SQL Server 2012 or later.md)|√|√|√|√|√|√|√|√|
|Database connection|[Connect to an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Connect to an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Configure an endpoint for an RDS instance]()|√|√|√|√|√|√|√|√|
|[View the endpoints and ports of an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Apply for a public endpoint for an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/Apply for or release a public endpoint on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|Monitoring and alerting|[View the monitoring data of an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Set the monitoring frequency of an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/Set the monitoring frequency.md)|√|√|√|√|√|√|√|√|
|[Configure an alert rule for an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|Network management|[Change the network type of an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/Change the network type of an ApsaraDB RDS for SQL Server instance.md)|×|×|√|√|×|×|√|√|
|Read-only instance and read/write splitting|[Create a read-only RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Read-only instances/Overview of read-only ApsaraDB RDS for SQL Server instances.md)|×|×|×|×|×|×|×|×|
|[Enable read/write splitting for an RDS instance](/intl.en-US/RDS SQL Server Database/Read/write splitting/Read/write splitting overview.md)|×|×|×|×|×|×|×|×|
|[Modify the read weights of read-only RDS instances](/intl.en-US/RDS SQL Server Database/Read/write splitting/Modify the read weights.md)|×|×|×|×|×|×|×|×|
|Security management|[Control access to an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Configure a whitelist for an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Configure SSL encryption for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure SSL encryption on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Configure TDE for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure TDE for an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|×|×|×|×|
|[Configure a distributed transaction whitelist for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure a distributed transaction whitelist for an ApsaraDB RDS for SQL Server instance.md)|√|√|×|×|√|√|×|×|
|Audit|[View the logs of an RDS instance](/intl.en-US/RDS SQL Server Database/Audit/Manage logs.md)|×|×|×|×|×|×|×|×|
|Backup|[Back up the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[t1986080.md\#]()|√|√|√|√|√|√|√|√|
|[Free quota for backup storage](/intl.en-US/RDS SQL Server Database/Backup/View the free quota for backup usage of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Download a backup file of an RDS instance](/intl.en-US/RDS SQL Server Database/Backup/Download data and log backup files from an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|Restoration|[Restore the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Restoration/Restore the data of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|Tag management|[Create tags](/intl.en-US/RDS SQL Server Database/Tag/Create tags.md)|√|√|√|√|√|√|√|√|
|[Delete tags](/intl.en-US/RDS SQL Server Database/Tag/Delete tags.md)|√|√|√|√|√|√|√|√|
|[Use tags to filter ApsaraDB RDS for SQL Server instances](/intl.en-US/RDS SQL Server Database/Tag/Use tags to filter ApsaraDB RDS for SQL Server instances.md)|√|√|√|√|√|√|√|√|

## SQL Server 2012

|Category|Feature|SQL Server 2012|
|EE|EE Basic|SE|WEB|
|RDS High-availability Edition|RDS Basic Edition|RDS High-availability Edition|RDS Basic Edition|
|Standard SSD|ESSD, ESSD PL2, or ESSD PL3|Standard SSD|ESSD|Standard SSD|ESSD, ESSD PL2, or ESSD PL3|Standard SSD|ESSD|
|--------|-------|---------------|
|--|--------|--|---|
|-----------------------------|-----------------|-----------------------------|-----------------|
|------------|---------------------------|------------|----|------------|---------------------------|------------|----|
|Data migration|[Migrate the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Data migration/Data migration solutions.md)|√|√|√|√|√|√|√|√|
|Instance management|[Create an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Change the specifications of an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Change the specifications of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Migrate an RDS instance across zones](/intl.en-US/RDS SQL Server Database/Instance/Migrate an ApsaraDB RDS for SQL Server instance across zones in the same region.md)|×|×|×|×|×|×|×|×|
|[Switch over services between primary and secondary RDS instances](/intl.en-US/RDS SQL Server Database/Instance/Perform a manual or automatic switchover of services between primary and secondary ApsaraDB RDS for SQL Server instances.md)|√|√|×|×|√|√|×|×|
|[Restart an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Restart an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Set the maintenance window of an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Set the maintenance window of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Release an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Release or unsubscribe from an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Manage ApsaraDB RDS for SQL Server instances in the recycle bin](/intl.en-US/RDS SQL Server Database/Instance/Manage ApsaraDB RDS for SQL Server instances in the recycle bin.md)|√|√|√|√|√|√|√|√|
|[DBCC](/intl.en-US/RDS SQL Server Database/Instance/DBCC features of ApsaraDB RDS for SQL Server.md)|√|√|√|√|√|√|√|√|
|Instance upgrade|[Upgrade an RDS instance from the Basic Edition to the High-availability Edition](/intl.en-US/RDS SQL Server Database/Version upgrade/Upgrade from Basic Edition to High-availability Edition.md)|×|×|√|√|×|×|√|√|
|[Upgrade an RDS instance from SQL Server 2012 to SQL Server 2016](/intl.en-US/RDS SQL Server Database/Version upgrade/Upgrade an instance from SQL Server 2012 to SQL Server 2016.md)|×|×|√|√|×|×|√|√|
|Account management|[Create an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Create an account for an RDS SQL Server instancy.md)|√|√|√|√|√|√|√|√|
|[Reset the password of an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Reset the password of an account on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Modify the permissions of an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Modify the permissions of a standard account on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Authorize the service account of an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Authorize a service account for an ApsaraDB RDS for SQL Server instance.md)|×|×|×|×|×|×|×|×|
|[Delete an account from an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Delete an account for an RDS SQL Server instance.md)|√|√|√|√|√|√|√|√|
|Database management|[Create a database on an RDS instance](/intl.en-US/RDS SQL Server Database/Database/Create a database on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Delete a database from an RDS instance](/intl.en-US/RDS SQL Server Database/Database/Delete a database from an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Copy a database between RDS instances](/intl.en-US/RDS SQL Server Database/Database/Database replication/Copy a database of ApsaraDB RDS SQL Server 2012 or later.md)|√|√|√|√|√|√|√|√|
|Database connection|[Connect to an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Connect to an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Configure an endpoint for an RDS instance]()|√|√|√|√|√|√|√|√|
|[View the endpoints and ports of an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Apply for a public endpoint for an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/Apply for or release a public endpoint on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|Monitoring and alerting|[View the monitoring data of an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Set the monitoring frequency of an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/Set the monitoring frequency.md)|√|√|√|√|√|√|√|√|
|[Configure an alert rule for an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|Network management|[Change the network type of an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/Change the network type of an ApsaraDB RDS for SQL Server instance.md)|×|×|√|√|×|×|√|√|
|Read-only instance and read/write splitting|[Create a read-only RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Read-only instances/Overview of read-only ApsaraDB RDS for SQL Server instances.md)|×|×|×|×|×|×|×|×|
|[Enable read/write splitting for an RDS instance](/intl.en-US/RDS SQL Server Database/Read/write splitting/Read/write splitting overview.md)|×|×|×|×|×|×|×|×|
|[Modify the read weights of read-only RDS instances](/intl.en-US/RDS SQL Server Database/Read/write splitting/Modify the read weights.md)|×|×|×|×|×|×|×|×|
|Security management|[Control access to an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Configure a whitelist for an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Configure SSL encryption for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure SSL encryption on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Configure TDE for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure TDE for an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|×|×|×|×|
|[Configure a distributed transaction whitelist for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure a distributed transaction whitelist for an ApsaraDB RDS for SQL Server instance.md)|√|√|×|×|√|√|×|×|
|Audit|[View the logs of an RDS instance](/intl.en-US/RDS SQL Server Database/Audit/Manage logs.md)|×|×|×|×|×|×|×|×|
|Backup|[Back up the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[t1986080.md\#]()|√|√|√|√|√|√|√|√|
|[Free quota for backup storage](/intl.en-US/RDS SQL Server Database/Backup/View the free quota for backup usage of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|[Download a backup file of an RDS instance](/intl.en-US/RDS SQL Server Database/Backup/Download data and log backup files from an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|Restoration|[Restore the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Restoration/Restore the data of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|√|√|√|√|√|
|Tag management|[Create tags](/intl.en-US/RDS SQL Server Database/Tag/Create tags.md)|√|√|√|√|√|√|√|√|
|[Delete tags](/intl.en-US/RDS SQL Server Database/Tag/Delete tags.md)|√|√|√|√|√|√|√|√|
|[Use tags to filter ApsaraDB RDS for SQL Server instances](/intl.en-US/RDS SQL Server Database/Tag/Use tags to filter ApsaraDB RDS for SQL Server instances.md)|√|√|√|√|√|√|√|√|

## SQL Server 2008 R2

|Category|Feature|SQL Server 2008 R2|
|RDS High-availability Edition|
|Local SSD|Standard SSD|ESSD, ESSD PL2, or ESSD PL3|
|--------|-------|------------------|
|-----------------------------|
|---------|------------|---------------------------|
|Data migration|[Migrate the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Data migration/Data migration solutions.md)|√|√|√|
|Instance management|[Create an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Change the specifications of an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Change the specifications of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Migrate an RDS instance across zones](/intl.en-US/RDS SQL Server Database/Instance/Migrate an ApsaraDB RDS for SQL Server instance across zones in the same region.md)|√|×|×|
|[Switch over services between primary and secondary RDS instances](/intl.en-US/RDS SQL Server Database/Instance/Perform a manual or automatic switchover of services between primary and secondary ApsaraDB RDS for SQL Server instances.md)|√|√|√|
|[Restart an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Restart an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Set the maintenance window of an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Set the maintenance window of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Release an RDS instance](/intl.en-US/RDS SQL Server Database/Instance/Release or unsubscribe from an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Manage ApsaraDB RDS for SQL Server instances in the recycle bin](/intl.en-US/RDS SQL Server Database/Instance/Manage ApsaraDB RDS for SQL Server instances in the recycle bin.md)|√|√|√|
|[DBCC](/intl.en-US/RDS SQL Server Database/Instance/DBCC features of ApsaraDB RDS for SQL Server.md)|×|√|√|
|Instance upgrade|[Upgrade an RDS instance from SQL Server 2008 R2 to SQL Server 2012 or SQL Server 2016](/intl.en-US/RDS SQL Server Database/Version upgrade/Upgrade a local SSD-based instance from SQL Server 2008 R2 to SQL Server 2012 or 2016.md)|√|×|×|
|Account management|[Create an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Create an account for an RDS SQL Server instancy.md)|√|√|√|
|[Reset the password of an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Reset the password of an account on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Modify the permissions of an account on an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Modify the permissions of a standard account on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Authorize the service account of an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Authorize a service account for an ApsaraDB RDS for SQL Server instance.md)|√|×|×|
|[Delete an account from an RDS instance](/intl.en-US/RDS SQL Server Database/Account/Delete an account for an RDS SQL Server instance.md)|√|√|√|
|Database management|[Create a database on an RDS instance](/intl.en-US/RDS SQL Server Database/Database/Create a database on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Delete a database from an RDS instance](/intl.en-US/RDS SQL Server Database/Database/Delete a database from an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Copy a database between RDS instances](/intl.en-US/RDS SQL Server Database/Database/Database replication/Copy a database of ApsaraDB RDS SQL Server 2008 R2.md)|√|√|√|
|Database connection|[Connect to an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Connect to an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Configure an endpoint for an RDS instance]()|√|√|√|
|[View the endpoints and ports of an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Apply for a public endpoint for an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/Apply for or release a public endpoint on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|Monitoring and alerting|[View the monitoring data of an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Set the monitoring frequency of an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/Set the monitoring frequency.md)|√|√|√|
|[Configure an alert rule for an RDS instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|Network management|[Change the network type of an RDS instance](/intl.en-US/RDS SQL Server Database/Database connection/Change the network type of an ApsaraDB RDS for SQL Server instance.md)|×|×|×|
|Read-only instance and read/write splitting|[Create a read-only RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Read-only instances/Overview of read-only ApsaraDB RDS for SQL Server instances.md)|×|×|×|
|[Enable read/write splitting for an RDS instance](/intl.en-US/RDS SQL Server Database/Read/write splitting/Read/write splitting overview.md)|×|×|×|
|[Modify the read weights of read-only RDS instances](/intl.en-US/RDS SQL Server Database/Read/write splitting/Modify the read weights.md)|×|×|×|
|Security management|[Control access to an RDS instance](/intl.en-US/RDS SQL Server Database/Quick start/Configure a whitelist for an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Configure SSL encryption for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure SSL encryption on an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Configure TDE for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure TDE for an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Configure a distributed transaction whitelist for an RDS instance](/intl.en-US/RDS SQL Server Database/Data security/Configure a distributed transaction whitelist for an ApsaraDB RDS for SQL Server instance.md)|×|×|×|
|Audit|[View the logs of an RDS instance](/intl.en-US/RDS SQL Server Database/Audit/Manage logs.md)|√|×|×|
|Backup|[Back up the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[t1986080.md\#]()|×|√|√|
|[Free quota for backup storage](/intl.en-US/RDS SQL Server Database/Backup/View the free quota for backup usage of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|[Download a backup file of an RDS instance](/intl.en-US/RDS SQL Server Database/Backup/Download data and log backup files from an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|Restoration|[Restore the data of an RDS instance](/intl.en-US/RDS SQL Server Database/Restoration/Restore the data of an ApsaraDB RDS for SQL Server instance.md)|√|√|√|
|Tag management|[Create tags](/intl.en-US/RDS SQL Server Database/Tag/Create tags.md)|√|√|√|
|[Delete tags](/intl.en-US/RDS SQL Server Database/Tag/Delete tags.md)|√|√|√|
|[Use tags to filter ApsaraDB RDS for SQL Server instances](/intl.en-US/RDS SQL Server Database/Tag/Use tags to filter ApsaraDB RDS for SQL Server instances.md)|√|√|√|

