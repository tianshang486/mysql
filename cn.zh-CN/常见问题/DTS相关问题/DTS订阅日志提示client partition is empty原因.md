# DTS订阅日志提示client partition is empty原因 {#concept_187599 .concept}

## 日志内容 {#section_uzg_ltv_8kk .section}

DTS订阅日志如下：

``` {#codeblock_ojx_oz7_k34}
[ Thread-1:11039 ] - [ INFO ] client partition is empty,wait partition balance
```

## 原因 {#section_5po_ikt_g36 .section}

一个订阅ID只能被一个客户端拉取数据，如果用这个订阅ID启动了多个客户端的话，只有一个会拉取到数据，其他客户端就会打印这个日志，当拉取数据的客户端出现故障，其他客户端之一就可以拉取到数据，这个是DTS的一个容灾功能。

