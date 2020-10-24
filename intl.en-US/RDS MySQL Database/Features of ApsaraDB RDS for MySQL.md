# Features of ApsaraDB RDS for MySQL

This topic provides an overview of the features supported by ApsaraDB RDS for MySQL with different database engine versions, RDS editions, and storage types. In the following table, the check sign \(√\) indicates that the feature is supported, and the cross sign \(×\) indicates that the feature is not supported.

## MySQL 8.0

|Category|Feature|MySQL 8.0|
|Enterprise Edition|High-availability Edition|Basic Edition|
|Local SSD|Local SSD|Standard or Enhanced SSD|Enhanced SSD|Standard or Enhanced SSD|
|--------|-------|---------|
|------------------|-------------------------|-------------|
|---------|---------|------------------------|------------|------------------------|
|Data migration|[Overview of data migration](/intl.en-US/RDS MySQL Database/Data Migration/Overview of data migration.md)|√|√|√|√|√|
|Data synchronization|[Overview of data synchronization](/intl.en-US/RDS MySQL Database/Data Synchronization/Overview of data synchronization.md)|√|√|√|√|√|
|Instance management|[Create an RDS instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Change the specifications of an RDS instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Migrate an RDS instance across zones in the same region](/intl.en-US/RDS MySQL Database/Instance Change/Migrate an ApsaraDB RDS for MySQL instance across zones in the same region.md)|√|√|×|×|×|
|[Switch over services between a primary RDS instance and its secondary instance](/intl.en-US/RDS MySQL Database/Instance Change/Perform a manual or automatic switchover of services between a primary ApsaraDB RDS for MySQL instance and its secondary instance.md)|×|√|√|√|×|
|[Change the data replication mode of an RDS instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the data replication mode of an ApsaraDB RDS for MySQL instance.md)|×|√|×|×|×|
|[Apply a parameter template to an RDS instance](/intl.en-US/RDS MySQL Database/Instance parameters/Use a parameter template to manage parameters.md)|√|√|√|√|√|
|[Create a disaster recovery instance](/intl.en-US/RDS MySQL Database/Disaster recovery instances/Create a disaster recovery ApsaraDB RDS for MySQL instance.md)|√|√|√|√|×|
|[Restart an RDS instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Restart an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Set the maintenance window of an RDS instance](/intl.en-US/RDS MySQL Database/Instance Change/Set the maintenance window of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Release an RDS instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Release or unsubscribe from an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Manage ApsaraDB RDS for MySQL instances in the recycle bin](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Manage ApsaraDB RDS for MySQL instances in the recycle bin.md)|√|√|√|√|√|
|Instance upgrade|[Upgrade the minor engine version of an RDS instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Upgrade the database engine version of an RDS instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the database engine version of an RDS MySQL instance.md)|×|×|×|×|×|
|Account management|[Create an account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Create an account on an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Reset the password of an account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Reset the password of an account on an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Modify the permissions of an account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Account permission/Modify the permissions of a standard account on an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Authorize the service account of an RDS instance](/intl.en-US/RDS MySQL Database/Account/Authorize the service account of an ApsaraDB RDS for MySQL instance.md)|√|√|×|×|×|
|[Delete an account from an RDS instance](/intl.en-US/RDS MySQL Database/Account/Delete an account for an RDS MySQL instance.md)|√|√|√|√|√|
|[Reset the permissions of the privileged account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Reset the permissions of the privileged account for an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|Database management|[Create a database for an RDS instance](/intl.en-US/RDS MySQL Database/Database/Create a database on an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Delete a database from an RDS instance](/intl.en-US/RDS MySQL Database/Database/Delete a database from an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|Database connection|[Connect to an RDS instance](/intl.en-US/RDS MySQL Database/Quick start/Connect to an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Configure endpoints for an RDS instance]()|√|√|√|√|√|
|[View the endpoints and ports of an RDS instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md)|√|√|√|√|√|
|[Apply for a public endpoint for an RDS instance](/intl.en-US/RDS MySQL Database/Database connection/Apply for or release a public endpoint for an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|Monitoring and alerting|[View the monitoring data of an RDS instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Set the monitoring frequency of an RDS instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Set the monitoring frequency of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Configure an alert rule for an RDS instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|Network management|[Change the network type of an RDS instance](/intl.en-US/RDS MySQL Database/Database connection/Change the network type of an ApsaraDB RDS for MySQL instance.md)|√|√|×|×|×|
|[Switch an RDS instance to a new VPC and VSwitch](/intl.en-US/RDS MySQL Database/Database connection/Switch to a new VPC and VSwitch for an RDS MySQL instance.md)|√|√|×|×|×|
|Read-only instance and read/write splitting|[Create a read-only instance](/intl.en-US/RDS MySQL Database/Read-only instances/Create a read-only ApsaraDB RDS for MySQL instance.md)|√|√|√|√|×|
|[Enable read/write splitting for an RDS instance](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/Enable the read/write splitting function in the shared proxy of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|×|
|[Change the network type of the read/write splitting endpoint for an RDS instance](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|√|√|√|√|×|
|Security management|[Configure a whitelist for an RDS instance](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Switch an RDS instance to the enhanced whitelist mode](/intl.en-US/RDS MySQL Database/Data security/Switch an ApsaraDB RDS for MySQL instance to the enhanced whitelist mode.md)|×|×|×|×|×|
|[Configure SSL encryption for an RDS instance](/intl.en-US/RDS MySQL Database/Data security/Configure SSL encryption on an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|×|
|[Configure Transparent Data Encryption \(TDE\) for an RDS instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md)|×|√|×|×|×|
|Audit|[SQL Explorer](/intl.en-US/RDS MySQL Database/Audit/SQL Explorer.md)|√|√|√|√|×|
|[Log management](/intl.en-US/RDS MySQL Database/Audit/Manage logs.md)|√|√|√|√|×|
|Database backup|[Back up an RDS instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[View the free quota for backup storage of an RDS instance](/intl.en-US/RDS MySQL Database/Backup/View the free quota for backup storage of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Download a backup file of an RDS instance](/intl.en-US/RDS MySQL Database/Backup/Download data and log backup files of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Back up an RDS instance across regions](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance across regions.md)|×|√|×|×|×|
|Database restoration|[Restore an RDS instance](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Restore individual databases or tables of an RDS instance](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md)|×|√|×|×|×|
|[Restore an RDS instance across regions](/intl.en-US/RDS MySQL Database/Restoration/Restore an ApsaraDB RDS for MySQL instance across regions.md)|×|√|×|×|×|
|Dedicated proxy|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|√|√|√|√|×|
|AliSQL|[AliSQL](/intl.en-US/Proprietary AliSQL/Features of AliSQL.md)|√|√|√|√|√|
|Tag management|[Create tags](/intl.en-US/RDS MySQL Database/Tag/Create tags.md)|√|√|√|√|√|
|[Unbind a tag](/intl.en-US/RDS MySQL Database/Tag/Unbind a tag.md)|√|√|√|√|√|
|[Filter RDS instances by tag](/intl.en-US/RDS MySQL Database/Tag/Filter RDS instances by tag.md)|√|√|√|√|√|

## MySQL 5.7

|Category|Feature|MySQL 5.7|
|Enterprise Edition|High-availability Edition|Basic Edition|
|Local SSD|Local SSD|Standard or Enhanced SSD|Enhanced SSD|Standard or Enhanced SSD|
|--------|-------|---------|
|------------------|-------------------------|-------------|
|---------|---------|------------------------|------------|------------------------|
|Data migration|[Overview of data migration](/intl.en-US/RDS MySQL Database/Data Migration/Overview of data migration.md)|√|√|√|√|√|
|Data synchronization|[Overview of data synchronization](/intl.en-US/RDS MySQL Database/Data Synchronization/Overview of data synchronization.md)|√|√|√|√|√|
|Instance management|[Create an RDS instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Change the specifications of an RDS instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Migrate an RDS instance across zones in the same region](/intl.en-US/RDS MySQL Database/Instance Change/Migrate an ApsaraDB RDS for MySQL instance across zones in the same region.md)|√|√|×|×|×|
|[Switch over services between a primary RDS instance and its secondary instance](/intl.en-US/RDS MySQL Database/Instance Change/Perform a manual or automatic switchover of services between a primary ApsaraDB RDS for MySQL instance and its secondary instance.md)|×|√|√|√|×|
|[Change the data replication mode of an RDS instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the data replication mode of an ApsaraDB RDS for MySQL instance.md)|×|√|×|×|×|
|[Apply a parameter template to an RDS instance](/intl.en-US/RDS MySQL Database/Instance parameters/Use a parameter template to manage parameters.md)|√|√|√|√|√|
|[Create a disaster recovery instance](/intl.en-US/RDS MySQL Database/Disaster recovery instances/Create a disaster recovery ApsaraDB RDS for MySQL instance.md)|√|√|√|√|×|
|[Restart an RDS instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Restart an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Set the maintenance window of an RDS instance](/intl.en-US/RDS MySQL Database/Instance Change/Set the maintenance window of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Release an RDS instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Release or unsubscribe from an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Manage ApsaraDB RDS for MySQL instances in the recycle bin](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Manage ApsaraDB RDS for MySQL instances in the recycle bin.md)|√|√|√|√|√|
|Instance upgrade|[Upgrade the minor engine version of an RDS instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Upgrade the database engine version of an RDS instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the database engine version of an RDS MySQL instance.md)|×|×|×|×|×|
|Account management|[Create an account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Create an account on an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Reset the password of an account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Reset the password of an account on an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Modify the permissions of an account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Account permission/Modify the permissions of a standard account on an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Authorize the service account of an RDS instance](/intl.en-US/RDS MySQL Database/Account/Authorize the service account of an ApsaraDB RDS for MySQL instance.md)|√|√|×|×|×|
|[Delete an account from an RDS instance](/intl.en-US/RDS MySQL Database/Account/Delete an account for an RDS MySQL instance.md)|√|√|√|√|√|
|[Reset the permissions of the privileged account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Reset the permissions of the privileged account for an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|Database management|[Create a database for an RDS instance](/intl.en-US/RDS MySQL Database/Database/Create a database on an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Delete a database from an RDS instance](/intl.en-US/RDS MySQL Database/Database/Delete a database from an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|Database connection|[Connect to an RDS instance](/intl.en-US/RDS MySQL Database/Quick start/Connect to an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Configure endpoints for an RDS instance]()|√|√|√|√|√|
|[View the endpoints and ports of an RDS instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md)|√|√|√|√|√|
|[Apply for a public endpoint for an RDS instance](/intl.en-US/RDS MySQL Database/Database connection/Apply for or release a public endpoint for an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|Monitoring and alerting|[View the monitoring data of an RDS instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Set the monitoring frequency of an RDS instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Set the monitoring frequency of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Configure an alert rule for an RDS instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|Network management|[Change the network type of an RDS instance](/intl.en-US/RDS MySQL Database/Database connection/Change the network type of an ApsaraDB RDS for MySQL instance.md)|√|√|×|×|√|
|[Switch an RDS instance to a new VPC and VSwitch](/intl.en-US/RDS MySQL Database/Database connection/Switch to a new VPC and VSwitch for an RDS MySQL instance.md)|√|√|×|×|×|
|Read-only instance and read/write splitting|[Create a read-only instance](/intl.en-US/RDS MySQL Database/Read-only instances/Create a read-only ApsaraDB RDS for MySQL instance.md)|√|√|√|√|×|
|[Enable read/write splitting for an RDS instance](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/Enable the read/write splitting function in the shared proxy of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|×|
|[Change the network type of the read/write splitting endpoint for an RDS instance](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|√|√|√|√|×|
|Security management|[Configure a whitelist for an RDS instance](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Switch an RDS instance to the enhanced whitelist mode](/intl.en-US/RDS MySQL Database/Data security/Switch an ApsaraDB RDS for MySQL instance to the enhanced whitelist mode.md)|√|√|√|√|×|
|[Configure SSL encryption for an RDS instance](/intl.en-US/RDS MySQL Database/Data security/Configure SSL encryption on an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|×|
|[Configure TDE for an RDS instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md)|×|√|×|×|×|
|Audit|[SQL Explorer](/intl.en-US/RDS MySQL Database/Audit/SQL Explorer.md)|√|√|√|√|×|
|[Log management](/intl.en-US/RDS MySQL Database/Audit/Manage logs.md)|√|√|√|√|×|
|Database backup|[Back up an RDS instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[View the free quota for backup storage of an RDS instance](/intl.en-US/RDS MySQL Database/Backup/View the free quota for backup storage of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Download a backup file of an RDS instance](/intl.en-US/RDS MySQL Database/Backup/Download data and log backup files of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Back up an RDS instance across regions](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance across regions.md)|×|√|×|×|×|
|Database restoration|[Restore an RDS instance](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance.md)|√|√|√|√|√|
|[Restore individual databases or tables of an RDS instance](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md)|×|√|×|×|×|
|[Restore an RDS instance across regions](/intl.en-US/RDS MySQL Database/Restoration/Restore an ApsaraDB RDS for MySQL instance across regions.md)|×|√|×|×|×|
|Dedicated proxy|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|√|√|√|√|×|
|AliSQL|[AliSQL](/intl.en-US/Proprietary AliSQL/Features of AliSQL.md)|√|√|√|√|√|
|Tag management|[Create tags](/intl.en-US/RDS MySQL Database/Tag/Create tags.md)|√|√|√|√|√|
|[Unbind a tag](/intl.en-US/RDS MySQL Database/Tag/Unbind a tag.md)|√|√|√|√|√|
|[Filter RDS instances by tag](/intl.en-US/RDS MySQL Database/Tag/Filter RDS instances by tag.md)|√|√|√|√|√|

## MySQL 5.6

|Category|Feature|MySQL 5.6|
|High-availability Edition|
|Local SSD|
|--------|-------|---------|
|-------------------------|
|---------|
|Data migration|[Overview of data migration](/intl.en-US/RDS MySQL Database/Data Migration/Overview of data migration.md)|√|
|Data synchronization|[Overview of data synchronization](/intl.en-US/RDS MySQL Database/Data Synchronization/Overview of data synchronization.md)|√|
|Instance management|[Create an RDS instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)|√|
|[Change the specifications of an RDS instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md)|√|
|[Migrate an RDS instance across zones in the same region](/intl.en-US/RDS MySQL Database/Instance Change/Migrate an ApsaraDB RDS for MySQL instance across zones in the same region.md)|√|
|[Switch over services between a primary RDS instance and its secondary instance](/intl.en-US/RDS MySQL Database/Instance Change/Perform a manual or automatic switchover of services between a primary ApsaraDB RDS for MySQL instance and its secondary instance.md)|√|
|[Change the data replication mode of an RDS instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the data replication mode of an ApsaraDB RDS for MySQL instance.md)|√|
|[Apply a parameter template to an RDS instance](/intl.en-US/RDS MySQL Database/Instance parameters/Use a parameter template to manage parameters.md)|√|
|[Restart an RDS instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Restart an ApsaraDB RDS for MySQL instance.md)|√|
|[Set the maintenance window of an RDS instance](/intl.en-US/RDS MySQL Database/Instance Change/Set the maintenance window of an ApsaraDB RDS for MySQL instance.md)|√|
|[Release an RDS instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Release or unsubscribe from an ApsaraDB RDS for MySQL instance.md)|√|
|[Manage ApsaraDB RDS for MySQL instances in the recycle bin](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Manage ApsaraDB RDS for MySQL instances in the recycle bin.md)|√|
|Instance upgrade|[Upgrade the minor engine version of an RDS instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance.md)|√|
|[Upgrade the database engine version of an RDS instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the database engine version of an RDS MySQL instance.md)|×|
|Account management|[Create an account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Create an account on an ApsaraDB RDS for MySQL instance.md)|√|
|[Reset the password of an account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Reset the password of an account on an ApsaraDB RDS for MySQL instance.md)|√|
|[Modify the permissions of an account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Account permission/Modify the permissions of a standard account on an ApsaraDB RDS for MySQL instance.md)|√|
|[Authorize the service account of an RDS instance](/intl.en-US/RDS MySQL Database/Account/Authorize the service account of an ApsaraDB RDS for MySQL instance.md)|√|
|[Delete an account from an RDS instance](/intl.en-US/RDS MySQL Database/Account/Delete an account for an RDS MySQL instance.md)|√|
|[Reset the permissions of the privileged account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Reset the permissions of the privileged account for an ApsaraDB RDS for MySQL instance.md)|√|
|Database management|[Create a database for an RDS instance](/intl.en-US/RDS MySQL Database/Database/Create a database on an ApsaraDB RDS for MySQL instance.md)|√|
|[Delete a database from an RDS instance](/intl.en-US/RDS MySQL Database/Database/Delete a database from an ApsaraDB RDS for MySQL instance.md)|√|
|Database connection|[Connect to an RDS instance](/intl.en-US/RDS MySQL Database/Quick start/Connect to an ApsaraDB RDS for MySQL instance.md)|√|
|[Configure endpoints for an RDS instance]()|√|
|[View the endpoints and ports of an RDS instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md)|√|
|[Apply for a public endpoint for an RDS instance](/intl.en-US/RDS MySQL Database/Database connection/Apply for or release a public endpoint for an ApsaraDB RDS for MySQL instance.md)|√|
|Monitoring and alerting|[View the monitoring data of an RDS instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for MySQL instance.md)|√|
|[Set the monitoring frequency of an RDS instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Set the monitoring frequency of an ApsaraDB RDS for MySQL instance.md)|√|
|[Configure an alert rule for an RDS instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for MySQL instance.md)|√|
|Network management|[Change the network type of an RDS instance](/intl.en-US/RDS MySQL Database/Database connection/Change the network type of an ApsaraDB RDS for MySQL instance.md)|√|
|[Switch an RDS instance to a new VPC and VSwitch](/intl.en-US/RDS MySQL Database/Database connection/Switch to a new VPC and VSwitch for an RDS MySQL instance.md)|√|
|Read-only instance and read/write splitting|[Create a read-only instance](/intl.en-US/RDS MySQL Database/Read-only instances/Create a read-only ApsaraDB RDS for MySQL instance.md)|√|
|[Enable read/write splitting for an RDS instance](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/Enable the read/write splitting function in the shared proxy of an ApsaraDB RDS for MySQL instance.md)|√|
|[Change the network type of the read/write splitting endpoint for an RDS instance](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|√|
|Security management|[Configure a whitelist for an RDS instance](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.md)|√|
|[Switch an RDS instance to the enhanced whitelist mode](/intl.en-US/RDS MySQL Database/Data security/Switch an ApsaraDB RDS for MySQL instance to the enhanced whitelist mode.md)|√|
|[Configure SSL encryption for an RDS instance](/intl.en-US/RDS MySQL Database/Data security/Configure SSL encryption on an ApsaraDB RDS for MySQL instance.md)|√|
|[Configure TDE for an RDS instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md)|√|
|Audit|[SQL Explorer](/intl.en-US/RDS MySQL Database/Audit/SQL Explorer.md)|√|
|[Log management](/intl.en-US/RDS MySQL Database/Audit/Manage logs.md)|√|
|Database backup|[Back up an RDS instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md)|√|
|[View the free quota for backup storage of an RDS instance](/intl.en-US/RDS MySQL Database/Backup/View the free quota for backup storage of an ApsaraDB RDS for MySQL instance.md)|√|
|[Download a backup file of an RDS instance](/intl.en-US/RDS MySQL Database/Backup/Download data and log backup files of an ApsaraDB RDS for MySQL instance.md)|√|
|[Back up an RDS instance across regions](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance across regions.md)|√|
|Database restoration|[Restore an RDS instance](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance.md)|√|
|[Restore individual databases or tables of an RDS instance](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md)|√|
|[Restore an RDS instance across regions](/intl.en-US/RDS MySQL Database/Restoration/Restore an ApsaraDB RDS for MySQL instance across regions.md)|√|
|Dedicated proxy|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|×|
|AliSQL|[AliSQL](/intl.en-US/Proprietary AliSQL/Features of AliSQL.md)|√|
|Tag management|[Create tags](/intl.en-US/RDS MySQL Database/Tag/Create tags.md)|√|
|[Unbind a tag](/intl.en-US/RDS MySQL Database/Tag/Unbind a tag.md)|√|
|[Filter RDS instances by tag](/intl.en-US/RDS MySQL Database/Tag/Filter RDS instances by tag.md)|√|

## MySQL 5.5

|Category|Feature|MySQL 5.5|
|High-availability Edition|
|Local SSD|
|--------|-------|---------|
|-------------------------|
|---------|
|Data migration|[Overview of data migration](/intl.en-US/RDS MySQL Database/Data Migration/Overview of data migration.md)|√|
|Data synchronization|[Overview of data synchronization](/intl.en-US/RDS MySQL Database/Data Synchronization/Overview of data synchronization.md)|√|
|Instance management|[Create an RDS instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)|√|
|[Change the specifications of an RDS instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md)|√|
|[Migrate an RDS instance across zones in the same region](/intl.en-US/RDS MySQL Database/Instance Change/Migrate an ApsaraDB RDS for MySQL instance across zones in the same region.md)|√|
|[Switch over services between a primary RDS instance and its secondary instance](/intl.en-US/RDS MySQL Database/Instance Change/Perform a manual or automatic switchover of services between a primary ApsaraDB RDS for MySQL instance and its secondary instance.md)|√|
|[Change the data replication mode of an RDS instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the data replication mode of an ApsaraDB RDS for MySQL instance.md)|√|
|[Apply a parameter template to an RDS instance](/intl.en-US/RDS MySQL Database/Instance parameters/Use a parameter template to manage parameters.md)|×|
|[Create a disaster recovery instance](/intl.en-US/RDS MySQL Database/Disaster recovery instances/Create a disaster recovery ApsaraDB RDS for MySQL instance.md)|×|
|[Restart an RDS instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Restart an ApsaraDB RDS for MySQL instance.md)|√|
|[Set the maintenance window of an RDS instance](/intl.en-US/RDS MySQL Database/Instance Change/Set the maintenance window of an ApsaraDB RDS for MySQL instance.md)|√|
|[Release an RDS instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Release or unsubscribe from an ApsaraDB RDS for MySQL instance.md)|√|
|[Manage ApsaraDB RDS for MySQL instances in the recycle bin](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Manage ApsaraDB RDS for MySQL instances in the recycle bin.md)|√|
|Instance upgrade|[Upgrade the minor engine version of an RDS instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance.md)|√|
|[Upgrade the database engine version of an RDS instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the database engine version of an RDS MySQL instance.md)|√|
|Account management|[Create an account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Create an account on an ApsaraDB RDS for MySQL instance.md)|√|
|[Reset the password of an account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Reset the password of an account on an ApsaraDB RDS for MySQL instance.md)|√|
|[Modify the permissions of an account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Account permission/Modify the permissions of a standard account on an ApsaraDB RDS for MySQL instance.md)|√|
|[Authorize the service account of an RDS instance](/intl.en-US/RDS MySQL Database/Account/Authorize the service account of an ApsaraDB RDS for MySQL instance.md)|√|
|[Delete an account from an RDS instance](/intl.en-US/RDS MySQL Database/Account/Delete an account for an RDS MySQL instance.md)|√|
|[Reset the permissions of the privileged account for an RDS instance](/intl.en-US/RDS MySQL Database/Account/Reset the permissions of the privileged account for an ApsaraDB RDS for MySQL instance.md)|√|
|Database management|[Create a database for an RDS instance](/intl.en-US/RDS MySQL Database/Database/Create a database on an ApsaraDB RDS for MySQL instance.md)|√|
|[Delete a database from an RDS instance](/intl.en-US/RDS MySQL Database/Database/Delete a database from an ApsaraDB RDS for MySQL instance.md)|√|
|Database connection|[Connect to an RDS instance](/intl.en-US/RDS MySQL Database/Quick start/Connect to an ApsaraDB RDS for MySQL instance.md)|√|
|[Configure endpoints for an RDS instance]()|√|
|[View the endpoints and ports of an RDS instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md)|√|
|[Apply for a public endpoint for an RDS instance](/intl.en-US/RDS MySQL Database/Database connection/Apply for or release a public endpoint for an ApsaraDB RDS for MySQL instance.md)|√|
|Monitoring and alerting|[View the monitoring data of an RDS instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for MySQL instance.md)|√|
|[Set the monitoring frequency of an RDS instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Set the monitoring frequency of an ApsaraDB RDS for MySQL instance.md)|√|
|[Configure an alert rule for an RDS instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for MySQL instance.md)|√|
|Network management|[Change the network type of an RDS instance](/intl.en-US/RDS MySQL Database/Database connection/Change the network type of an ApsaraDB RDS for MySQL instance.md)|√|
|[Switch an RDS instance to a new VPC and VSwitch](/intl.en-US/RDS MySQL Database/Database connection/Switch to a new VPC and VSwitch for an RDS MySQL instance.md)|√|
|Read-only instance and read/write splitting|[Create a read-only instance](/intl.en-US/RDS MySQL Database/Read-only instances/Create a read-only ApsaraDB RDS for MySQL instance.md)|×|
|[Enable read/write splitting for an RDS instance](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/Enable the read/write splitting function in the shared proxy of an ApsaraDB RDS for MySQL instance.md)|×|
|[Change the network type of the read/write splitting endpoint for an RDS instance](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|×|
|Security management|[Configure a whitelist for an RDS instance](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.md)|√|
|[Switch an RDS instance to the enhanced whitelist mode](/intl.en-US/RDS MySQL Database/Data security/Switch an ApsaraDB RDS for MySQL instance to the enhanced whitelist mode.md)|√|
|[Configure SSL encryption for an RDS instance](/intl.en-US/RDS MySQL Database/Data security/Configure SSL encryption on an ApsaraDB RDS for MySQL instance.md)|×|
|[Configure TDE for an RDS instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md)|×|
|Audit|[SQL Explorer](/intl.en-US/RDS MySQL Database/Audit/SQL Explorer.md)|√|
|[Log management](/intl.en-US/RDS MySQL Database/Audit/Manage logs.md)|√|
|Database backup|[Back up the data of an RDS instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md)|√|
|[View the free quota for backup storage of an RDS instance](/intl.en-US/RDS MySQL Database/Backup/View the free quota for backup storage of an ApsaraDB RDS for MySQL instance.md)|√|
|[Download a backup file of an RDS instance](/intl.en-US/RDS MySQL Database/Backup/Download data and log backup files of an ApsaraDB RDS for MySQL instance.md)|√|
|[Back up the data of an RDS instance across regions](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance across regions.md)|×|
|Database restoration|[Restore an RDS instance](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance.md)|√|
|[Restore individual databases or tables of an RDS instance](/intl.en-US/RDS MySQL Database/Restoration/Restore individual databases and tables of an ApsaraDB RDS for MySQL instance.md)|×|
|[Restore an RDS instance across regions](/intl.en-US/RDS MySQL Database/Restoration/Restore an ApsaraDB RDS for MySQL instance across regions.md)|×|
|Dedicated proxy|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md)|×|
|AliSQL|[AliSQL](/intl.en-US/Proprietary AliSQL/Features of AliSQL.md)|x|
|Tag management|[Create tags](/intl.en-US/RDS MySQL Database/Tag/Create tags.md)|√|
|[Unbind a tag](/intl.en-US/RDS MySQL Database/Tag/Unbind a tag.md)|√|
|[Filter RDS instances by tag](/intl.en-US/RDS MySQL Database/Tag/Filter RDS instances by tag.md)|√|

