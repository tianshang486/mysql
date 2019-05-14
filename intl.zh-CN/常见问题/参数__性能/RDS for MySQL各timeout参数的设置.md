# RDS for MySQL各timeout参数的设置 {#concept_265063 .concept}

RDS for MySQL提供了很多的timeout参数供用户设置，本文详细介绍下这些timeout参数的含义。

|参数名称|说明|
|----|--|
|connect\_timeout|该参数控制与服务器建立连接的时候等待三次握手成功的超时时间，该参数主要是对于网络质量较差导致连接超时，建议外网访问波动较大可以提高该参数。|
|delayed\_insert\_timeout|指INSERT语句执行的超时时间。|
|innodb\_lock\_wait\_timeout|指锁等待的超时时间，该锁不同于死锁是指正常一个事务等待另外一个事务的S锁或者X锁的超时时间。|
|innodb\_rollback\_on\_timeout|当事务超时超过该参数后即会回滚，如果设置为OFF即只回滚事务的最后一个请求。|
|interactive\_timeout wait\_timeout

 |mysql在关闭一个交互式/非交互式的连接之前所要等待的时间。建议不需要设置太长的时候，否则会占用实例的连接数资源。|
|lock\_wait\_timeout|指定尝试获取元数据锁的超时时间。|
|net\_read\_timeout net\_write\_timeout

 |指服务器端等待客户端发送的网络包和发送给客户端网络包的超时时间，这两个参数是对TCP/IP链接并且是Activity状态下的线程才有效的参数。|
|slave\_net\_timeout|备实例等待主服务器同步的超时时间，超时后中止同步并尝试重新连接。|

