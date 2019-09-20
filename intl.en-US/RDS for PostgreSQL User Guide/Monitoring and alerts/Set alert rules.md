# Set alert rules {#concept_ir2_twp_wdb .concept}

You can set alert rules for monitoring your system. When the monitored metric meets the conditions, an alert will be triggered and a notification will be sent to the alert contacts.

## Supported monitored metrics {#section_uh6_xjh_u7o .section}

|ApsaraDB RDS for PostgreSQL edition|Supported monitored metrics|
|-----------------------------------|---------------------------|
|PostgreSQL 11 Cluster Edition \(Standard SSD\) and PostgreSQL 10 Cluster Edition \(Standard SSD\)|IOPS usage|
|iNode usage|
|Storage usage|
|TPS|
|Connection usage|
|Average active connections per CPU|
|Longest bloat duration|
|CPU utilization|
|Memory usage|
|PostgreSQL 10 Cluster Edition \(Local SSD\), PostgreSQL 10 Basic Edition, and PostgreSQL 9.4|Connection usage|
|CPU utilization|
|Latency of read-only instances|
|Disk usage|
|IOPS usage|
|Memory usage|

## For PostgreSQL 10 Cluster Edition \(Local SSD\), PostgreSQL 10 Basic Edition, and PostgreSQL 9.4 {#section_wvv_wwp_wdb .section}

**Create alert rules**

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner of the page, select the region where the instance is located.

    ![Select a region](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156895918436543_en-US.png)

3.  Find the instance and click the instance ID.
4.  In the left-side navigation pane, click **Monitoring and Alerts**.
5.  Click the **Alerts** tab.
6.  Click **Set Alert Rules** to open the CloudMonitor console.

    **Note:** You can click **Refresh** to manually refresh the current status of the monitored metrics.

7.  Create an alert group. For more information, see [Create alert contacts and alert groups](https://www.alibabacloud.com/help/doc-detail/104004.htm).
8.  Create an alert rule. For more information, see [ApsaraDB for RDS monitoring](https://www.alibabacloud.com/help/doc-detail/28587.htm).

**Manage alert rules**

1.  Log on to the [CloudMonitor console for monitoring ApsaraDB for RDS](https://cloudmonitor.console.aliyun.com/#/cloud/rds/).
2.  Select the region where your instance is located.
3.  Find the instance and click the instance ID.
4.  On the Alarm Rules tab, find the alert and select one of the following operations:
    -   View: views the details of an alert rule.
    -   Alarm Logs: views the alert history for a certain period of time.
    -   Modify: modifies alert rules. For more information about the parameters, see [Parameter description](https://www.alibabacloud.com/help/doc-detail/119898.htm).
    -   Disable: disables the selected alert rules. If an alert rule is disabled, no alert is triggered even though the monitored metric meets the conditions.
    -   Delete: deletes the selected alert rules. An alert rule cannot be restored after you delete the rule. You can only add it again.

