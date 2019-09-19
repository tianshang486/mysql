# Use internal SQL statements to verify the effect of read/write splitting {#concept_o2g_cdv_ydb .concept}

This topic describes how to verify the effect of read/write splitting for an RDS for MySQL instance by running the `/*PROXY_INTERNAL*/show last route;` command.

**Note:** Currently, do not use this SQL statement in the production environment because it is still being tested internally and may be adjusted later as required.

## View the database to which an SQL statement is sent for execution {#section_4wb_482_mgo .section}

You can view the ID of the instance on which an SQL statement is executed by running the following command:

``` {#codeblock_2ld_2ns_ujp}
/*PROXY_INTERNAL*/show last route;
```

**Note:** RDS provides a built-in hint SQL statement \(which can only be executed by using read/write splitting VIP\). When running this statement on the MySQL client, the -c option must be selected. Otherwise, the client filters out the hit and the following error is returned:

``` {#codeblock_e9y_fi5_b6s}
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that
corresponds to your MySQL server version for the right syntax to use near 'last route' at
line 1
```

The returned result `last_bkid` indicates the ID of the database to which the last SQL statement \(the one before the hit\) was sent. This ID is the unique identification of an RDS instance. The following figure shows the details.

![查看结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7923/15688835094252_en-US.png)

**Note:** Given that the SQL load for RDS is measured in batches with a minimum unit of 100 entries, the first 100 `select` statements are executed on the same instance before the 101st `select` statement is routed to another instance. To verify this, you can write a simple SQL file such as a.sql:

``` {#codeblock_mlc_6k9_w0f}
select 1;
/*PROXY_INTERNAL*/show last route;select 1;
***100 entries***;
select 1;
/*PROXY_INTERNAL*/show last route;
```

Now you can see that the 101st SQL statement is routed to another instance \(assuming that more than two read-only instances are available for sharing the load\).

## Verify that all write requests are forwarded to the master database \(master instance\) for execution {#section_2zf_jj7_jfg .section}

Once read/write splitting is enabled for RDS instances, write requests can only be forwarded to the master database because read-only databases only process read requests. Even when a system or routing error occurs, for example, a write SQL statement is routed to a read-only database, such write request can be routed back to the master database for execution according to the error reason \(read\_only error\).

Additionally, you can run the `insert` statement, and then run the following hint SQL statement to verify that all write requests are forwarded to the master database.

``` {#codeblock_bjf_e8n_7hk}
/*PROXY_INTERNAL*/show last route;
```

