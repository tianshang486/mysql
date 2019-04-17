# RDS for MySQL默认关闭MyISAM引擎 {#concept_185690 .concept}

MyISAM引擎表不支持事务，读写操作会相互冲突，仅支持表级别锁。当查询或者写入操作时间比较长的时候，会阻塞其他操作，容易导致连接堆积，而且在宕机后存在数据丢失的风险，因此RDS for MySQL推荐使用Innodb引擎。 目前RDS for MySQL如果导入表、新建表是MyISAM引擎或调整表引擎为MyISAM，会自动修改为Innodb引擎。

