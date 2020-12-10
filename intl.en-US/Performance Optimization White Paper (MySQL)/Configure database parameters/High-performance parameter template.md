# High-performance parameter template

To ensure service availability, ApsaraDB RDS for MySQL does not allow you to configure some important parameters. However, to meet your needs in various scenarios, ApsaraDB RDS for MySQL provides parameter templates. For example, if you pursue higher performance, you can select the high-performance parameter template.

The high-performance parameter template delivers medium security but the fastest speed. If you select this template, data is replicated in asynchronous mode. The following parameters settings are specified in this template to protect data:

-   innodb\_flush\_log\_at\_trx\_commit = 2
-   sync\_binlog = 1000

The following table describes the parameters.

|Parameter|Value|Description|
|---------|-----|-----------|
|innodb\_flush\_log\_at\_trx\_commit|1|When you commit a transaction, the system writes the transaction log from the buffer to the log file and synchronizes the log file to the disk immediately.|
|2|When you commit a transaction, the system writes the transaction log from the buffer to the log file but does not immediately synchronize the log file to the disk. The log file is written to the disk every second. If the system stops responding before a write operation is performed, logs generated within the last second will be lost.|
|sync\_binlog|1|When you commit a transaction, the binary log file is written to the disk and the disk is immediately refreshed. The log file is not written to the buffer.|
|1000|The buffer is written to the disk and the disk is refreshed whenever 1,000 records are submitted to the buffer. This may result in data loss.|

For more information about parameter templates and how to use the parameter templates, see [Use a parameter template to manage parameters](/intl.en-US/RDS MySQL Database/Instance parameters/Use a parameter template to manage parameters.md).

