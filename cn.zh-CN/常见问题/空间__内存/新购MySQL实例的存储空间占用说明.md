# 新购MySQL实例的存储空间占用说明 {#concept_ecy_fl4_hhb .concept}

系统文件ib\_logfile0和ib\_logfile1会占用新购MySQL实例的存储空间。

对于新购的RDS for MySQL实例，您会发现虽然还没有写入任何数据，但是存储空间已经被占用了几个GB，其实这是系统文件ib\_logfile0和ib\_logfile1占用的空间。

ib\_logfile0和ib\_logfile1这两个日志文件用于保存InnoDB引擎表的事务日志信息，其文件大小尺寸固定（约2GB左右）且不可改变。另外，较大的ib\_logfile0和ib\_logfile1文件尺寸在高并发事务的场景下有利于减少事务日志文件切换的次数，可提高实例的性能。

