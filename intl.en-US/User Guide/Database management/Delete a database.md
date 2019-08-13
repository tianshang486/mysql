# Delete a database {#concept_ijx_zjq_wdb .concept}

You can use the RDS console or an SQL statement to delete a database. Each method applies to different types of instances. Choose a suitable method based on the instance you want to delete.

## Use the RDS console to delete a database {#section_wnq_3kq_wdb .section}

This operation applies to RDS for MySQL, SQL Server, and MariaDB TX instances.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target instance is located.

    ![Region screenshot](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156568212537169_en-US.png)

3.  Find the target instance and click the instance ID.
4.  In the left-side navigation pane, click **Databases**.
5.  Find the database you want to delete and in the **Actions** column click **Delete**.
6.  In the displayed dialog box, click **OK**.

## Run a SQL statement to delete a database {#section_jzp_rkq_wdb .section}

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/?spm=5176.doc26187.2.2.OVo7wv).
2.  In the upper-left corner, select the region where the target instance is located.

    ![Region screenshot](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156568212537169_en-US.png)

3.  Find the target instance and click the instance ID.
4.  Click **Log On to DB** in the upper-right corner of the page to go to the Quick logon page of the [DMS console](https://dms.console.aliyun.com/?token=549cf345-ac05-455c-b3f9-75eadae023fe#/dms/login).
5.  On the Quick logon page, check the connection address and port information displayed on the RDS Database Logon page. If the information is correct, enter the database username and password, and click **Log On**. Parameter description:
    -   Database username: the name of the premier account.

    -   Password: the password for the premier account.

        **Note:** You can view the connection address and port information of this account on the Basic Information page of the instance in the RDS console.

6.  Enter the verification code and click **Log On**.

    **Note:** If you want the browser to remember the password, select **Remember Password** and click **Log On**.

7.  If DMS prompts you to add the IP address segment of the DMS server to the RDS address whitelist, click **Configure Whitelist**. For more information about how to manually configure the whitelist, see [Configure the whitelist](intl.en-US/User Guide/Security/Set the whitelist.md#).
8.  Click **Log On**.
9.  In the top navigation bar, choose **SQL Operations** \> **SQL Window**.
10. Run the following statement to delete the database:

    ``` {#codeblock_uje_tnp_dsx}
    DROP DATABASE <database name>;
    ```

    **Note:** For high-availability instances of RDS for SQL Server 2012 and later, you can also use the following stored procedure. This stored procedure deletes the specified database, removes the associated image, and kills the connection to the database.

    ``` {#codeblock_s90_3m4_e59}
    EXEC sp_rds_drop_database 'database name'
    ```

11. Click **Execute** to delete the database.

