# Storage space usage of the newly purchased MySQL instance

The system files ib\_logfile0 and ib\_logfile1 consume the storage space of the newly purchased MySQL instance.

For a newly purchased RDS for MySQL instance, you can find that although no data has been written, several GB of the storage space is already occupied, which is actually the space occupied by the system files ib\_logfile0 and ib\_logfile1.

The ib\_logfile0 and ib\_logfile1 log files are used to store transaction log of InnoDB tables. The log file size is fixed \(approximately 2GB\) and cannot be changed. In addition, larger ib\_logfile0 and ib\_logfile1 files reduce the number of transaction log file switching times and improve instance performance in scenarios of high-concurrency transactions.

## References

-   [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)
-   [View the free quota for backup storage of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/View the free quota for backup storage of an ApsaraDB RDS for MySQL instance.md)

