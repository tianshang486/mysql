# Use a parameter template to manage parameters

This topic describes how to use a parameter template to manage the parameters of an ApsaraDB for RDS instance. ApsaraDB RDS for MySQL provides system parameter templates and custom parameter templates.

Instances run one of the following MySQL versions:

-   MySQL 8.0
-   MySQL 5.7
-   MySQL 5.6

To ensure service availability, you can only configure certain parameters in the ApsaraDB for RDS console. ApsaraDB RDS for MySQL provides various system parameter templates and allows you to customize parameter templates to suit your business requirements in high-performance and other scenarios.

**Note:** For more information about how to configure a single parameter, see [Reconfigure the parameters of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance parameters/Reconfigure the parameters of an ApsaraDB RDS for MySQL instance.md).

## System template introduction

**Note:** ApsaraDB RDS for MySQL provides system templates for High-availability and Basic Edition instances. You can create custom templates for Enterprise Edition instances. For more information, see [Create a custom parameter template](#section_zp4_33y_vx4).

ApsaraDB RDS for MySQL on High-availability Edition and Basic Edition instances can use the following system parameter templates:

-   Default parameter template

    It ensures the highest data security but costs more time. Data is semi-synchronously replicated. The parameters are specified with the following values to protect data:

    -   InnoDB
        -   innodb\_flush\_log\_at\_trx\_commit = 1
        -   sync\_binlog = 1
    -   X-Engine \(only the default parameter template is provided\)

        sync\_binlog = 1

-   Asynchronous parameter template

    It ensures high data security and fast speed. Data is asynchronously replicated. The parameters are specified with the following values to protect data:

    -   innodb\_flush\_log\_at\_trx\_commit = 1
    -   sync\_binlog = 1
-   High-performance parameter template

    It ensures average data security but is less time-intensive to implement. Data is asynchronously replicated. The parameters are specified with the following values to protect data:

    -   innodb\_flush\_log\_at\_trx\_commit = 2
    -   sync\_binlog = 1000

**Note:** You cannot use a custom parameter template to modify parameters that are in the system parameter templates.

The following table describes the parameters in the system parameter templates.

|Parameter|Value|Description|
|---------|-----|-----------|
|innodb\_flush\_log\_at\_trx\_commit|1|When you commit a transaction, the system writes the transaction log from the buffer to the log file and synchronizes the log file to the disk immediately.|
|2|When you commit a transaction, the system writes the transaction log from the buffer to the log file but does not immediately synchronize the log file to the disk. The log file is written to the disk every second. If the system stops responding before a write operation is performed, logs generated within the last second will be lost.|
|sync\_binlog|1|When you commit a transaction, the binary log file is written to the disk and the disk is immediately refreshed. The log file is not written to the buffer.|
|1000|The buffer is written to the disk and the disk is refreshed whenever 1,000 records are submitted to the buffer. This may result in data loss.|

## Apply a parameter template

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  In the left-side navigation pane, click **Parameter Templates**.

    ![View the parameter template list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8746317061/p55731.png)

4.  On the **Custom Parameter Templates** or **System Parameter Templates** tab, find the template that you want to apply.

5.  Click **Apply to Instance** in the Actions column.

6.  Select RDS instances from the All Instances section, click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2430359951/p55825.png) icon to move them to the Selected Instances section, and then check the parameter comparison.

    **Note:** Before you apply a parameter template to multiple RDS instances, you must verify that the parameters are suitable for the RDS instances.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2430359951/p55826.png)

7.  Click **OK**.


## Create a custom parameter template

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  In the left-side navigation pane, click **Parameter Templates**. In the upper-right corner of the page, click **Create Parameter Template**.

    ![Create a parameter template](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3430359951/p55718.png)

4.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Template Name**|The name of the parameter template. The name must be 8 to 64 characters in length and can contain letters, digits, periods \(.\), and underscores \(\_\). It must start with a letter.|
    |**Database Engine**|The engine of the database. Set the value to MySQL.|
    |**Engine Version**|The version of the database engine. Valid values: MySQL 5.6, 5.7, and 8.0.|
    |**Description**|The description that helps identify the parameter template. The description can be up to 200 characters in length.|
    |**Add Parameter**|Click **Add Parameter** and select a parameter from the **Parameter** drop-down list. Then, you can set the parameter value as well as view the value range and default value. **Note:**

    -   For more information about available parameters, see **Editable Parameters** on the **Parameters** page.
    -   If you want to add another parameter, you must click **Add Parameter** again.
    -   If you want to remove a parameter, you must click **Delete** to the right of the parameter.
![Add a parameter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3430359951/p55727.png) |
    |**Import**|If you have exported a parameter template to your computer, you can edit that template based on your business needs and then click **Import** to copy its parameters. For more information about how to export a parameter template, see [Reconfigure the parameters of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance parameters/Reconfigure the parameters of an ApsaraDB RDS for MySQL instance.md).|

5.  Click **Confirm**.


## Clone a parameter template

You can clone a parameter template from the current region to another region.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  In the left-side navigation pane, click **Parameter Templates**.

    ![View the parameter template list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8746317061/p55731.png)

4.  Find the target parameter template, and click **Clone** in the Actions column.

5.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Region**|The destination region to which you want to clone the parameter template.|
    |**Template Name**|The name of the parameter template. The name must be 8 to 64 characters in length and can contain letters, digits, periods \(.\), and underscores \(\_\). It must start with a letter.|
    |**Description**|The description that helps identify the parameter template. The description can be up to 200 characters in length.|

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3430359951/p55830.png)

6.  Click **OK**.


## Manage parameter templates

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  In the left-side navigation pane, click **Parameter Templates**.

    ![View the parameter template list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8746317061/p55731.png)

4.  Manage parameter templates in this region.

    **Note:** You can only perform the **View** and **Apply to Instance** operations on system templates.

    To view a parameter template, follow these steps:

    Find the target parameter template, and click **View** in the Actions column. On the page that appears, view the basic information and parameters of the template.

    ![View a parameter template](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3430359951/p55733.png)

    To modify a parameter template, follow these steps:

    1.  Find the target parameter template, and click **Edit** in the Actions column. For more information, see [Step 4](#table_ijx_nyq_jjz) in the "Create a parameter template" section.

    2.  Click **Edit**.

    To delete a parameter template, follow these steps:

    Find the target parameter template, and click **Delete** in the Actions column. In the message that appears, click **OK**.

    **Note:** When you delete a parameter template, it does not affect the RDS instances to which the template is applied.


## Related operations

|API|Description|
|---|-----------|
|[Create a parameter template](/intl.en-US/API Reference/Parameter management/Create a parameter template.md)|Creates an ApsaraDB for RDS parameter template.|
|[Modify a parameter template](/intl.en-US/API Reference/Parameter management/Modify a parameter template.md)|Modifies an ApsaraDB for RDS parameter template.|
|[Copy a parameter template](/intl.en-US/API Reference/Parameter management/Copy a parameter template.md)|Clones an ApsaraDB for RDS parameter template from one region to another.|
|[Query parameter templates](/intl.en-US/API Reference/Parameter management/Query parameter templates.md)|Queries the ApsaraDB for RDS parameter templates available within a region.|
|[Query information of a parameter template](/intl.en-US/API Reference/Parameter management/Query information of a parameter template.md)|Queries an ApsaraDB for RDS parameter template.|
|[Delete a parameter template](/intl.en-US/API Reference/Parameter management/Delete a parameter template.md)|Deletes an ApsaraDB for RDS parameter template.|

