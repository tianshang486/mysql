# Verify the allocated read weights {#concept_e4z_gsp_wdb .concept}

This topic describes how to verify the allocated read weights when read/write splitting is enabled.

To verify the load ratio of each read weight, you can run the `select @@server_id;` command for 10,000 times by using persistent connections and collect the number of times that each `server_id` appears in the output.

Alternatively, you can check whether the load ratio of read weight is consistent with the distributed ratio by using one of the following two methods:

## Verify the load ratio based on monitoring data in the console {#section_6e7_08k_pyi .section}

1.  Log on to the [RDS console](https://rdsnew.console.aliyun.com/console/index?spm=5176.doc51070.2.3.bIzwWm#/rdsList/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156888543136543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Monitoring and Alerts**.
5.  On the **Monitoring** tab, select the monitoring type **Engine Monitoring**.
6.  View the **TPS \(Transactions per Second\)/QPS \(Queries per Second\)** chart to obtain the number of read and write operations on each of the master and read-only instances.

    **Note:** Refreshing the TPS/QPS chart takes about five minutes.

7.  Compare the QPS/TPS of each instance to verify whether the load ratio is correct.

## Verify the SQL load by directly connecting to each instance {#section_9e3_5pc_ev5 .section}

You can view the number of SQL statements executed by each instance by connecting to the master database and read-only databases involving read/write splitting.

**Note:** To verify this, the connection addresses of the master database and read-only databases instead of the read/write splitting address are needed.

Run either of the following commands to verify the SQL load:

``` {#codeblock_ful_ea7_hd5}
select * from information_schema.global_status where VARIABLE_NAME = 'COM_SELECT';
```

``` {#codeblock_wyh_vju_zif}
select * from information_schema.global_status where VARIABLE_NAME = 'COM_INSERT;
```

