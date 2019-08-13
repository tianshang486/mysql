# Create databases and accounts {#concept_jx1_w5g_wdb .concept}

Before using RDS, you must create databases and accounts for your RDS instance. For PPAS instances, you must create an initial account on the RDS console. And then you can create and manage databases through a client. This topic takes the pgAdmin 4 client as an example to introduce how to create databases and accounts for PPAS instances.

## Precautions {#section_zfc_bvg_wdb .section}

-   Databases under a single instance share all the resources of this instance. Each PPAS instance supports one initial account, countless general accounts, and countless databases. You must create and manage common accounts and databases through SQL statements.
-   To migrate your local database to an RDS instance, you must create the same databases and accounts for the RDS instance as your local database.
-   When assigning account permissions for each database, follow the minimum permission' principle and consider service roles to create accounts. Alternatively, rationally assign read-only and read/write permissions. When necessary, you can split accounts and databases into smaller units so that each account can only access data for its own services. If the account does not need to write data to a database, assign the read-only permission for the account.
-   For database security, set strong passwords for the accounts and change the passwords regularly.

## Procedure {#section_k5v_cwj_50c .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156566537536543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Click **Create Initial Account**.
6.  Enter the account information.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653756102_en-US.png)

    Parameter description:

    -   **Database Account**: the name of the initial account. It contains 2 to 16 characters including the lowercase letters, digits, or underscores \(\_\). It must begin with a letter and end with a letter or digit.
    -   **Password**: the password of the initial account. It contains 8 to 32 characters including at least three of the following types of characters: uppercase letters, lowercase letters, digits, and special characters. The allowed special characters are as follows:

        ! @ \# $ % ^ & \* \( \) \_ + - =

    -   **Re-enter Password**: Re-enter the password to make sure that the password is entered correctly.
7.  Click **OK**.
8.  Add the IP address that is allowed to access the RDS instance to the RDS whitelist. For more information about how to configure a whitelist, see [Configure a whitelist](intl.en-US/Quick Start for PPAS/Initial configuration/Configure a whitelist.md#).
9.  Start the pgAdmin 4 client.
10. Right-click **Servers** and choose **Create** \> **Server** from the shortcut menu.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653764047_en-US.png)

11. In the Create Server dialog box, click the **General** tab and enter the server name.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653764048_en-US.png)

12. Click the Connection tab and enter the information about the instance to be connected.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653764049_en-US.png)

    Parameter description:

    -   **Host name/address**: the connection address of the RDS instance. If your application accesses the RDS instance through the intranet, enter the intranet IP address of the RDS instance. If your application accesses the RDS instance through the Internet, enter the Internet IP address of the RDS instance. The following procedure shows how to find the connection address and port number of the RDS instance:
        1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
        2.  Select the region where the target instance is located.
        3.  Find the target instance and click its ID.
        4.  On the Basic Information page, find the Internet/intranet IP address and Internet/intranet port number of the instance.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653764050_en-US.png)

    -   **Port**: the port number of the RDS instance. If your application accesses the RDS instance through the intranet, enter the intranet port number of the RDS instance. If your application accesses the RDS instance through the Internet, enter the Internet port number of the RDS instance.
    -   **Username**: the name of the initial account name for the RDS instance.
    -   **Password**: the password of the initial account for the RDS instance.
13. Click **Save**.
14. If the connection information is correct, choose **Servers** \> **server name** \> **Databases** \> **edb or postgres**. The following page is displayed, which indicates that the connection to the RDS instance is successful.

    **Note:** postgres is the default system database of the RDS instance. Do not perform any operation in this database.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653764051_en-US.png)

15. Double-click **postgres** and choose **Tools** \> **Query Tool**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653774052_en-US.png)

16. Enter the following command on the **Query-1** tab page to create a database:

    ``` {#codeblock_0pr_g88_yev}
    create database <database name>;
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653774053_en-US.png)

17. Click **Execute/Refresh**, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653774054_en-US.png)

    If the execution is successful, the new database is created.

18. Right-click **Databases** and choose **Refresh** from the shortcut menu. Then you can find the new database.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653774055_en-US.png)

19. Enter the following command on the Query-1 tab page to create an account:

    ``` {#codeblock_4vo_0m1_m9s}
    CREATE ROLE "username" CREATEDB CREATEROLE LOGIN ENCRYPTED PASSWORD 'password';
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653774056_en-US.png)

20. Click **Execute/Refresh**, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653784057_en-US.png)

    If the execution is successful, the new account is created.

21. Right-click **Login/Group Roles** and choose **Refresh** from the shortcut menu. Then you can find the new account.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7862/15656653784058_en-US.png)


## FAQ {#section_0q7_cg3_rz1 .section}

Can I use the new account of my RDS instance on the corresponding read-only instances?

The new account will be synchronized to the read-only instances of your RDS instance. However, you cannot manage the account in the read-only instances. The new account only has the read permissions on the read-only instances.

## APIs {#section_9zx_sdf_q9s .section}

|API|Description|
|---|-----------|
|[CreateAccount](../intl.en-US/API Reference/Account management/CreateAccount.md#)|Used to create an account.|

