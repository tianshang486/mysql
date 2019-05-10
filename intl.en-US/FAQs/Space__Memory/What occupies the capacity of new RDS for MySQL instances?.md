# What occupies the capacity of new RDS for MySQL instances? {#concept_ecy_fl4_hhb .concept}

In RDS for MySQL instances, system files ib\_logfile0 and ib\_logfile1 occupy certain storage capacity.

After creating an RDS for MySQL instance, you can see that a few GB of storage space has been used. This is because of the system files ib\_logfile0 and ib\_logfile1.

The two log files are used to store the transaction log of the InnoDB engine table. Their size is always approximately 2 GB and cannot be changed. Due to the large size of the two files, the transaction log files do not need to be switched frequently when there are highly concurrent transactions. Therefore, the instance performance is improved.

