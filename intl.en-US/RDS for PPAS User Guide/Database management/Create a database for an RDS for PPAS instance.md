# Create a database for an RDS for PPAS instance {#concept_cg3_ljq_wdb .concept}

This topic uses the pgAdmin 4 client as an example to describe how to create a database for an RDS for PPAS instance. Before using an RDS for PPAS instance, you must create accounts and databases for it. Specifically, you must create a premier account in the RDS console, and then create and manage databases by using the DMS console.

## Precautions {#section_kcx_dgg_wdb .section}

-   The databases in an RDS instance share all resources provided by the instance. You can create and manage more than one database by using SQL statements.
-   If you want to migrate an on-premises database to an RDS instance, you must create the same accounts and databases in the RDS instance as those in the on-premises database.

## Procedure {#section_ixc_fgg_wdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156888647636543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  Add the IP addresses of the devices that are to access the RDS instance to a whitelist of the RDS instance. For more information, see [Configure a whitelist for an RDS for PPAS instance](intl.en-US/RDS for PPAS User Guide/Data security/Configure a whitelist for an RDS for PPAS instance.md#).
5.  Start the pgAdmin 4 client.
6.  In the left-side navigation pane, right-click **Servers** and choose **Create** \> **Server**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7850/15688864764034_en-US.png)

7.  In the Create - Server dialog box, click the **General** tab and enter the server name.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7850/15688864764035_en-US.png)

8.  Click the **Connection** tab and enter the information about the RDS instance to be connected.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7850/15688864764036_en-US.png)

    Parameter description:

    -   **Host name/address**: The internal or public endpoint of the RDS instance. To obtain the internal and public endpoints and ports of the RDS instance, follow these steps:
        1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
        2.  In the upper-left corner, select the region where the target RDS instance is located.
        3.  Find the target RDS instance and click the instance ID.
        4.  On the Basic Information page, find the **Basic Information** section, where you can obtain the internal and public endpoints and ports of the RDS instance.
    -   **Port**: The internal or public port numbr of the RDS instance.
    -   **Username**: The username of the premier account for the RDS instance.
    -   **Password** The password of the premier account for the RDS instance.
9.  Click **Save**.
10. Choose **Servers** \> **Server name** \> **Databases** \> **postgres**. If the connection information is correct, the page shown in the following figure is displayed, indicating that a connection is established.

    **Note:** **postgres** is the default database of the RDS instance. Do not perform any operation in this database.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7850/15688864764039_en-US.png)

11. Select **postgres** and choose **Tools** \> **Query Tool**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7850/15688864766452_en-US.png)

12. On the **Query-1** tab, enter the following command to create a database:

    ``` {#codeblock_dgq_do3_1qj}
    create database <database name>;
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7850/15688864764040_en-US.png)

13. Click the execute or refresh button.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7850/15688864766453_en-US.png)

14. When the command is executed successfully, indicating that the database is created, right-click **Databases** and choose the refresh button to view the new database.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7850/15688864764041_en-US.png)


