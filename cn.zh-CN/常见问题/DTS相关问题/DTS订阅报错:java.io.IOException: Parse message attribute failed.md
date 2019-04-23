# DTS订阅报错:java.io.IOException: Parse message attribute failed {#concept_187410 .concept}

## 错误信息 {#section_97z_hgc_nzv .section}

DTS订阅报错如下：

``` {#codeblock_i6i_nkv_gar}
java.io.IOException: Parse message attribute failed because Store aliyun_hz_ecs_rdsxxxxxxxxx-1-0.0000000003 find aliyun_hz_ecs_rdsxxxxxxxxx-1-0 without server id and 1444709748 failed error
at com.aliyun.drc.client.message.Builder.build(Builder.java:48)
at com.aliyun.drc.client.impl.HttpHandler.recvDRCPResponse(HttpHandler.java:245)
at com.aliyun.drc.client.impl.ServerProxy.getResponse(ServerProxy.java:138)
at com.aliyun.drc.client.impl.DRCClientImpl.run(DRCClientImpl.java:363)
at java.lang.Thread.run(Unknown Source)
```

## 错误原因 {#section_u0r_sue_gjc .section}

DTS订阅只能查询当前时间前24小时之内的数据，时间点不在该范围内就会报这个错误。

## 解决方案 {#section_w1q_mfh_jka .section}

您可以修改DTS的消费位点，请参见[修改消费位点](https://help.aliyun.com/document_detail/26642.html)。

