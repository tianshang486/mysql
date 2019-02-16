# Connect to an instance {#concept_n1v_qpf_vdb .concept}

After [creating an instance](intl.en-US/Quick Start for MySQL/Create an instance.md), [setting the whitelist](intl.en-US/Quick Start for MySQL/Initial configuration/Set the whitelist.md#), and [creating a database account](intl.en-US/Quick Start for MySQL/Initial configuration/Create accounts and databases.md), you can connect to the RDS for MySQL instance through any MySQL client.

## Use a client to connect to RDS for MySQL {#section_fbz_ym5_vdb .section}

The following uses [MySQL-Front](http://www.mysqlfront.de/) as an example.

1.  Start the MySQL-Front client.
2.  In the Open Connection window, click **New**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/15503045032607_en-US.png)

3.  Enter the RDS connection information.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/15503045032608_en-US.png)

    |Parameter|Description|
    |---------|-----------|
    |**Description Name**|Enter the connection task name. It is the same as the **Host** field by default.|
    |**Host**|Enter the intranet or Internet address of the RDS instance.    -   If your client is deployed on an ECS instance that is in the same region and has the same network type as your RDS instance, use the intranet address.
    -   In other cases, use the Internet address.
You can view the address and port information as follows:

    1.  Log on to the [RDS console](https://rds.console.aliyun.com/?spm=a2c63.p38356.a3.3.37eb609eGtv1CF).
    2.  Select the region where the target instance is located.
    3.  Click the ID of the instance to visit the Basic Information page.
    4.  In the Basic Information area, you can find the Internet and intranet addresses and port numbers.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/15503045032609_en-US.png)

|
    |**Port**|     -   Enter the intranet port number if you use an intranet address.
    -   Enter the Internet port number if you use an Internet address.
 |
    |**User**|Enter an account name of the RDS instance.|
    |**Password**|Enter the password of the preceding account.|

4.  Click **OK**.
5.  In the Open Connection window, select the connection that you created and click **Open**.

    If the connection information is correct, the RDS instance gets connected successfully.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7823/15503045032610_en-US.png)


