# Set Alarm Rules

This topic describes how to monitor an apsaradb for RDS instance. This function provides the ability to notify you when an instance exception is detected. In addition, the system will notify you when the instance is locked due to insufficient disk capacity.

## Prerequisites

The instance must be in the mainland China region.

## Background information

Monitoring and alerting are implemented through CloudMonitor. With CloudMonitor, you can configure monitored metrics and alert rules, and can associate contact groups with monitored metrics. When a monitored metric triggers an alert based on a specified alert rule, the system sends notification emails to all contacts in the contact groups associated with the monitored metric.

## Create alert rules

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, select the region where the target RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the target RDS instance and click its ID.
4.  In the left-side navigation pane, click **Monitoring and Alerts**.
5.  On the Alarm Contact Management page, click the **Alerts** tab.
6.  Click **Set Alert Rule** to go to the CloudMonitor console.

    ![Set alarm rules](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2350359951/p95893.png)

7.  Create an alert group. For more information, see [create an alert contact and an alert Contact Group](https://www.alibabacloud.com/help/zh/doc-detail/104004.htm).
8.  Create an alarm rule. For more information, see [apsaradb for RDS](https://www.alibabacloud.com/help/zh/doc-detail/28587.htm).

    **Note:** You can also use tags to automatically monitor resources. For more information, see [Monitor resources based on tags](/intl.en-US/Best Practices/Monitor resources based on tags.md).


## Manage alert rules

1.  Log on to the [CloudMonitor console for monitoring ApsaraDB for RDS](https://cloudmonitor.console.aliyun.com/#/cloud/rds/).
2.  Select the region where your instance is located.
3.  Find the target RDS instance and click its ID.
4.  On the Alarm Rules tab, find the alert and select one of the following operations:
    -   View: views the details of an alert rule.
    -   Alarm Logs: views the alert history for a certain period of time.
    -   Modify: modifies alerts. For more information about the parameters, see [alarm rule parameters](https://www.alibabacloud.com/help/zh/doc-detail/119898.htm).
    -   Disable: disables the selected alert rules. If an alert rule is disabled, no alert is triggered even though the monitored metric meets the conditions.
    -   Delete: deletes the selected alert rules. An alert rule cannot be restored after you delete the rule. You can only add it again.

