# Use DMS to log on to an RDS instance {#concept_cml_x4v_ydb .concept}

You can use DMS to log on to an RDS instance. For more information, see [Data management](https://www.alibabacloud.com/help/zh/doc-detail/47550.htm). This topic describes how to use DMS to log on to an RDS instance from the RDS console.

## Precautions {#section_yj4_kfv_cgb .section}

-   You can only use an internal address to log on to DMS.
-   The following instances do not support DMS:
    -   MariaDB instances
    -   MySQL 8.0 instances

## Procedure {#section_obw_z4v_ydb .section}

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the instance is located.

    ![Region screenshot](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156446333437169_en-US.png)

3.  Click the ID of the instance to go to the Basic Information page.
4.  Click **Log On to DB** in the upper-right corner of the page, as shown in the following figure, to go to the Quick Logon page of the [DMS console](https://dms.console.aliyun.com/?spm=5176.doc49015.2.5.1qi2e9&token=549cf345-ac05-455c-b3f9-75eadae023fe#/dms/login).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8006/15644633344253_en-US.png)

5.  On the Quick Logon page, check the connection address and port information displayed on the RDS Database Logon page. If the information is correct, enter the username and password of the database, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8006/15644633344254_en-US.png)

    Parameter description:

    -   1: The internal address and port information of an instance, which is in the `<internal address>:<port number>` format. For information about how to view the internal address and port information of an instance, see [View instance intranet/Internet address and port number](intl.en-US/User Guide/Connection management/View intranet__Internet IP addresses and port number of an instance.md#).
    -   2: The account used to connect to the instance.
    -   3: The password of the account used to connect to the instance.
6.  Click **Log On**.

    **Note:** If you want the Web browser to remember the password, select **Remember Password** and click **Log On**.

7.  If DMS prompts you to add the IP address segment of the DMS server to the RDS address whitelist, click **Specify for All Instances** or **Specify for Current Instance**.

    ![](images/4255_en-US.png)

8.  Click **Log On**.

