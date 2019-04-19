# DTS订阅报错:Connection timed out {#concept_186446 .concept}

## 错误信息 {#section_a77_q7e_jqp .section}

DTS数据订阅出现超时错误如下：

``` {#codeblock_ka0_gq6_58f}
2015-11-11 16:16:36,724 INFO [com.aliyun.drc.clusterclient.partition.PartitionPool] - client partition is empty,wait partition balance
2015-11-11 16:16:46,748 INFO [com.aliyun.drc.clusterclient.partition.PartitionPool] - client partition is empty,wait partition balance
2015-11-11 16:16:56,802 INFO [com.aliyun.drc.clusterclient.partition.PartitionPool] - start new partition: {“tables”:[“xxxx.*”],”topic”:”aliyun_bj_ecs_rdsxxxxxxxx-1-0”,”guid”:”dts_rdsxxxxxxxx_nSj”,”partition”:{“name”:”0f59329ace868558b1xxxxxxxx”,”gmt”:1447229810},”offset”:”::::1447229563:”,”group”:”111111111111111”}
2015-11-11 16:08:34,933 ERROR [com.aliyun.drc.clusterclient.partition.PartitionPool] - keep alive error
java.net.ConnectException: Connection timed out
```

## 解决方案 {#section_ygf_lwl_zzd .section}

运行SDK的服务器是否使用公网IP连接DTS，检查是否设置了`context.setUsePublicIp(false);`，修改为`context.setUsePublicIp(true);`。

