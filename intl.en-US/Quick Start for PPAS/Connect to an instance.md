# Connect to an instance {#concept_nks_hwg_wdb .concept}

You can use a database client or Data Management Service \(DMS\) to connect to an RDS instance. This topic describes how to connect to an RDS instance by using DMS and the pgAdmin 4 client.

## Background information {#section_jgt_kwg_wdb .section}

You can log on to DMS from the [RDS console](https://rds.console.aliyun.com/?spm=5176.doc49015.2.2.1qi2e9) and then connect to an RDS instance. [DMS](https://dms-intl.console.aliyun.com/#/dms/login) offers an integrated solution for data and schema management, access security, BI charts, data trends, data tracking, performance and optimization, and server management. DMS can be used to manage non-relational databases and relational databases, such as MySQL, SQL Server, PostgreSQL, MongoDB, and Redis. It can also be used to manage Linux servers.

You can also use a database client to connect to an RDS instance. ApsaraDB RDS for PPAS is fully compatible with PPAS. You can connect to RDS in the similar way you connect to an on-premises PPAS server. This topic describes how to use the pgAdmin 4 client to connect to an RDS instance. This topic also serves as a reference if you choose to use other database clients. When you use a client to connect to an RDS instance, you must [set internal and public IP addresses](../../../../intl.en-US/User Guide/Connection management/Configure endpoints.md) as follows:

-   If your client is deployed in an ECS instance and the instance is in the same region and has the same network type as the target RDS instance, then you can use the internal IP address. For example, ECS and RDS instances are both in the VPC located in China \(Hangzhou\). You can use the internal IP address provided to create a secure connection.
-   Use the public IP address for other situations.

## Use DMS to connect to an RDS instance {#section_m4j_sxr_kdn .section}

For more information about how to connect to an RDS instance through DMS, see [Log on to the RDS database through DMS](https://www.alibabacloud.com/help/doc-detail/64703.htm).

## Use a client to connect to an RDS instance {#section_j0g_k5v_lhq .section}

1.  Add the IP address that is used to access the RDS instance to the RDS whitelist. For more information about how to configure a whitelist, see [Configure a whitelist](intl.en-US/Quick Start for PPAS/Initial configuration/Configure a whitelist.md#).
2.  Start the pgAdmin 4 client.
3.  Right-click **Servers** and choose **Create** \> **Server** from the shortcut menu.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7863/15674943612976_en-US.png)

4.  On the General tab of the Create - Server dialog box, enter the name of the server, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7863/15674943622977_en-US.png)

5.  Click the Connection tab, and enter the information of the target RDS instance, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7863/15674943622978_en-US.png)

    Parameter description:

    -   **Host name/address**: the connection address of the RDS instance. If it is an internal connection, enter the internal IP address of the RDS instance. If it is an external connection, enter the public IP address of the RDS instance. To view the connection address and the port information of the RDS instance, take these steps:

        1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
        2.  In the upper-left corner, select the region where the target instance is located.
        3.  Find the target instance and click its ID.
        4.  On the Basic Information page, find the Internet/intranet IP address and Internet/intranet port number of the instance.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7863/15674943622979_en-US.png)

    -   **Port**: the port number of the RDS instance. If it is an internal connection, enter the port number for internal connections. If it is an external connection, enter the port number for external connections.

    -   **Username**: the name of the initial account name for the RDS instance.

    -   **Password**: the password of the initial account for the RDS instance.

6.  Click **Save**.
7.  If the connection information is correct, choose **Servers** \> **Server Name** \> **Databases** \> **edb** or **postgres**. The following page is displayed, which indicates that the connection to the RDS instance is successful.

    **Note:** Edb and postgres are default system databases of the RDS instance. Do not perform any operation in the two databases.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7863/15674943622980_en-US.png)


