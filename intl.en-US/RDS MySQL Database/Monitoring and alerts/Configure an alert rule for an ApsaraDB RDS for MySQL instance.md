# Configure an alert rule for an ApsaraDB RDS for MySQL instance

This topic describes how to configure an alert rule for an ApsaraDB RDS for MySQL instance. If a metric meets the conditions specified in the alert rule, an alert will be sent to all of the contacts in the contact group that is associated with the metric.

The RDS instance resides in a region of mainland China.

The monitoring and alerts feature of ApsaraDB for RDS is implemented by using Cloud Monitor. Cloud Monitor allows you to configure metrics and alert rules. You can also specify the contact groups that are associated with specific metrics. If a metric triggers an alert based on a specified alert rule, the system sends emails to all of the contacts in the contact group that is associated with the metric.

For more information about how to configure alert rules for RDS instances that run other database engines, see the following topics:

-   [Configure an alert rule for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Monitoring and alerts/Configure alert rules for an ApsaraDB RDS instance.md)
-   [Configure an alert rule for an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for PostgreSQL instance.md)
-   [Configure an alert rule for an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Monitoring and alerts/Set Alarm Rules.md)
-   [Configure an alert rule for an ApsaraDB RDS for MariaDB TX instance](/intl.en-US/RDS MariaDB TX Database/Monitoring and alerts/Set Alarm Rules.md)

## Create alert rules

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Monitoring and Alerts**.

5.  Click the **Alerts** tab.

6.  Click **Set Alert Rule** to go to the Cloud Monitor console.

    ![Set Alert Rule](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2350359951/p95893.png)

7.  Create an alert contact group. For more information, see [Create an alert contact or alert group](/intl.en-US/Alarm service/Alert contacts/Create an alert contact or alert group.md).

8.  Create alert rules. For more information, see [Create a threshold-triggered alert rule](/intl.en-US/Alarm service/Alarm rules/Create a threshold-triggered alert rule.md).

    **Note:** You can also configure Cloud Monitor to automatically monitor resources based on tags. For more information, see [Monitor resources based on tags](/intl.en-US/Best Practices/Monitor resources based on tags.md).


## Manage alert rules

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Monitoring and Alerts**.

5.  Click the **Alerts** tab.

6.  Click **Set Alert Rule** to go to the Cloud Monitor console.

    ![Set Alert Rule](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2350359951/p95893.png)

7.  On the **Alarm Rules** tab, find the target alert rule and in the Actions column select one of the following operations:

    -   View: View details about the alert rule.
    -   Alarm Logs: View the alerts that were triggered by the alert rule over a specific period of time.
    -   Modify: Modify the alert rule. For more information about the parameters, see [Alarm rule parameters](/intl.en-US/Alarm service/Alarm rules/Alarm rule parameters.md).
    -   Disable: Disable the alert rule. After you disable the alert rule, no alerts will be triggered even if the metric meets the conditions specified in the alert rule.
    -   Delete: Delete the alert rule. After you delete an alert rule, the alert rule cannot be restored. You can only re-create the alert rule if necessary.

