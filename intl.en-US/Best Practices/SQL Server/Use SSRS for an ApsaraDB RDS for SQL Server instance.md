# Use SSRS for an ApsaraDB RDS for SQL Server instance {#task_1580281 .task}

You can install SQL Server Reporting Services \(SSRS\) on an ECS instance and create reports based on the data in an ApsaraDB RDS for SQL Server instance. This topic describes how to use ApsaraDB RDS for SQL Server instances as data sources to create reports.

Microsoft SQL Server contains server components such as SQL Server database engine, SSRS, and SQL Server Analysis Services \(SSAS\). The SQL Server database engine is a standard relational database component. ApsaraDB RDS for SQL Server is a PaaS that provides this database engine. Components such as SSRS run as Windows services, and are not provided as PaaS services on Alibaba Cloud. If you need to use SSRS on Alibaba Cloud, you must create a Windows-based ECS instance before installing and configuring SSRS.

**Note:** You cannot create the SSRS configuration database in an ApsaraDB RDS for SQL Server instance.

## Prerequisites {#section_5iy_p7v_igq .section}

-   You have created an ApsaraDB RDS for SQL Server instance. For more information, see [Create an RDS for SQL Server instance](../../../../intl.en-US/Quick Start for SQL Server/Create an RDS for SQL Server instance.md#).
-   You have [created an instance by using the wizard](https://www.alibabacloud.com/help/zh/doc-detail/87190.htm).
-   You have [installed SQL Server](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/installation-for-sql-server?view=sql-server-2017) on the ECS instance.

**Note:** The version of SQL Server on the ECS instance can be different from the version of the ApsaraDB RDS for SQL Server instance.

## Procedure {#section_umx_t6u_68i .section}

1.  Download and install [Reporting Services](https://www.microsoft.com/zh-CN/download/details.aspx?id=55252) in the ECS instance.
2.  Start the Report Server Configuration Manager. Configure Server Name and Report Server Instance. Click **Connect**. 

    **Note:** Report Server Configuration Manager automatically displays all the Report Server instances that are in the ECS instance. Select an instance as needed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1253389/156739009354639_en-US.png)

3.  In the left-side navigation pane, click **Service Account** and **Web Service URL** and configure parameters based on your business needs. 

    **Note:** For more information, see [Install SQL Server Reporting Services \(2017 and later\)](https://docs.microsoft.com/en-us/sql/reporting-services/install-windows/install-reporting-services?view=sql-server-2017).

4.  In the left-side navigation pane, click **Database**. On the right side of the page, click **Change Database** to create a new report server database in the ECS instance. 

    1.  Select **Create a new report server database** and click **Next**.
    2.  Enter the server name and click **Next**.
    3.  Enter the database name and select a language for the script. Click **Next**. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1253389/156739009354641_en-US.png)

    4.  Configure the credentials for the account to connect to the report server and click **Next**.
    5.  Confirm the information on the Summary page and click **Next**. Wait for the database to be created. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1253389/156739009354642_en-US.png)

    6.  Click **Finish**.
    **Note:** For more information, see [Install SQL Server Reporting Services \(2017 and later\)](https://docs.microsoft.com/en-us/sql/reporting-services/install-windows/install-reporting-services?view=sql-server-2017).

5.  In the left-side navigation pane, click **Web Portal URL** and click **Apply**. After the application operation is finished, click the URL to go to the Web portal of the report server. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1253389/156739009454644_en-US.png)

6.  In the upper-right corner of the page, choose **New** \> **Data Source**.
7.  Configure the parameters as follows: 

    |Section|Parameter|Description|
    |-------|---------|-----------|
    |**Properties**|**Name**|Enter the name of the data source. The name cannot contain special characters. Special characters include / @ $ & \* + = < \> : ' , ? | \\|
    |**Description**|Specify the description of the data source to identify different data sources.|
    |**Hide**|Click to hide the data source.|
    |**Enable**|Click to enable the data source.|
    |**Connections**|**Type**|Select a type of the data source. Select **Microsoft SQL Server**.|
    |**Connection String**|Specify the endpoint and the database name of the ApsaraDB RDS for SQL Server instance in the `Data Source=<RDS for SQL Server instance endpoint>; Initial Catalog=<database name>` format. **Note:** Make sure the IP address of the ECS instance is added to the IP whitelist of the RDS instance. For more information, see [Configure a whitelist](../../../../intl.en-US/Quick Start for SQL Server/Initial configuration/Configure a whitelist.md#).

 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1253389/156739009454649_en-US.png)

|
    |**Credential**|**Data Source Login**|Select **Use the following credentials**.|
    |**Credential Type**|Select **Database username and password**.|
    |**Username**|Enter the database account of the ApsaraDB RDS for SQL Server instance.|
    |**Password**|Enter the password of the database account.|

8.  Click **Create**.

After the data source is created, you can use software such as Report Builder and Visual Studio to design reports. For more information, see [Report Builder in SQL Server](https://docs.microsoft.com/en-us/sql/reporting-services/report-builder/report-builder-in-sql-server-2016?view=sql-server-2017).

