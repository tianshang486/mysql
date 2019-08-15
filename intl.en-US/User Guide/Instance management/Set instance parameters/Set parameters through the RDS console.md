# Set parameters through the RDS console {#concept_lfl_xmn_wdb .concept}

You can view and reconfigure some parameters for your RDS instance through the RDS console or APIs. Additionally, you can view the parameter reconfiguration history on the RDS console.

**Note:** For instances of SQL Server 2012 or later, you can set their parameters only by running SQL commands. For more information, see [Use SQL commands to set parameters](intl.en-US/User Guide/Instance management/Set instance parameters/Use SQL commands to set parameters.md#).

## Precautions {#section_mkp_gnn_wdb .section}

-   The new parameter values must be within the allowed value ranges shown on the **Modifiable Parameters** tab page of the RDS console.
-   Your RDS instance must be restarted after some of its parameters are reconfigured. On the **Modifiable Parameters** tab page, you can check the value in the **Force Restart** column for a parameter to determine whether you must restart your RDS instance after you reconfigure the parameter. Restarting an RDS instance interrupts the connection to the instance. Therefore, before restarting your RDS instance, you must guarantee appropriate business arrangements.

## Reconfigure parameters {#section_wmp_lnn_wdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/?spm=a2c63.p38356.a3.1.514e5c6dFW5iGI).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156585869437169_en-US.png)

3.  Find the target RDS instance and click its ID to open the Basic Information page.
4.  In the left-side navigation pane, click **Parameters**.
5.  Click the **Modifiable Parameters** tab.
6.  Reconfigure parameters.
    -   To reconfigure a parameter:

        1.  Click ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/26179/cn_zh/1466499669749/Image%20005.png) following the parameter.
        2.  Enter the target value and click **Confirm**.
        3.  Click **Apply Changes**.
        4.  In the displayed dialog box, click **Confirm**.
        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7895/15658586943045_en-US.png)

    -   To reconfigure multiple parameters:

        1.  Click **Export Parameters** to export the parameters as a .txt file to your computer.
        2.  Open the file and reconfigure parameters.
        3.  Click **Import Parameters**.
        4.  In the displayed Import Parameters dialog box, copy and paste the parameters to be reconfigured and their values, then click **OK**
        5.  Confirm the parameter reconfiguration results in the parameter list and click **Apply Changes**.
        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7895/15658586943046_en-US.png)


## View the parameter reconfiguration history {#section_fvg_vnn_wdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/?spm=a2c63.p38356.a3.1.514e5c6dFW5iGI).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156585869437169_en-US.png)

3.  Find the target RDS instance and click its ID to open the Basic Information page.
4.  In the left-side navigation pane, click **Parameters**.
5.  Click the **Modification History** tab.
6.  Select a time range and click **Search**.

## APIs {#section_jkb_znn_wdb .section}

-   [DescribeParameterTemplates](../../../../intl.en-US/API Reference/Parameter management/DescribeParameterTemplates.md#)
-   [DescribeParameters](../../../../intl.en-US/API Reference/Parameter management/DescribeParameters.md#)
-   [ModifyParameter](../../../../intl.en-US/API Reference/Parameter management/ModifyParameter.md#)

## Parameters {#section_ldg_scy_cyb .section}

If you are new to ApsaraDB RDS, begin learning more with the following resources:

-   [MySQL 5.5 Parameters](http://dev.mysql.com/doc/refman/5.5/en/server-system-variables.html)
-   [MySQL 5.6 Parameters](http://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html)
-   [MySQL 5.7 Parameters](http://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html)
-   [SQL Server Parameters](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/server-configuration-options-sql-server?view=sql-server-2017)
-   [PostgreSQL and PPAS Parameters](https://www.postgresql.org/docs/10/static/runtime-config.html)
-   [MariaDB Parameters](https://mariadb.com/kb/en/library/server-system-variables/)

## Best practice {#section_cfc_14n_wdb .section}

For more information, see [Parameter optimization for MySQL instances](https://www.alibabacloud.com/help/doc-detail/63255.htm).

