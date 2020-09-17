# View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance

When you connect to an ApsaraDB RDS for MySQL instance, you must enter its internal or public endpoint and port number. This topic describes how to view and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance in the ApsaraDB for RDS console.

## View the internal and public endpoints and port numbers of an RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the **Basic Information** section of the Basic Information page, view the internal and public endpoints and port numbers of the RDS instance.

    **Note:**

    -   The endpoints and port numbers appear only after you configure an IP address whitelist or security group for the RDS instance. For more information, see [Configure a whitelist for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.md).
    -   The public endpoint appear only after you have applied for a public endpoint for the RDS instance. For more information, see [Apply for or release a public endpoint for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Apply for or release a public endpoint for an ApsaraDB RDS for MySQL instance.md).
    ![View the internal and public endpoints and port numbers of an RDS instance](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4250359951/p4256.png)


## Change the internal and public endpoints and port numbers of an RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Database Connection**.

5.  In the upper-right corner of the Instance Connection tab, click **Change Endpoint**.

6.  In the dialog box that appears, select a connection type, enter the prefix of the endpoint, specify the port number, and then click **OK**.

    **Note:**

    -   The prefix of the endpoint must be 8 to 64 characters in length and can contain letters, digits, and hyphens \(-\). It must start with a lowercase letter.
    -   The port number must be within the range of 1000 to 5999.
    ![Change the internal and public endpoints and port numbers of an RDS instance](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4250359951/p53802.png)


## FAQ

-   After I change an endpoint or port number of my RDS instance, do I need to update the endpoint or port number on my application?

    Yes, after you change an endpoint or port number of your RDS instance, you must update the endpoint or port number on your application. If you do not update the endpoint or port number on your application, your application cannot connect to your RDS instance.

-   After I change an endpoint or port number of my RDS instance, is the change immediately applied? And do I need to restart my RDS instance?

    After you change an endpoint or port number of your RDS instance, the change is immediately applied. You do not need to restart your RDS instance.

-   After I change or release an endpoint of my RDS instance, can I use the endpoint for another RDS instance?

    Yes, after you change or release an endpoint of your RDS instance, you can use the endpoint for another RDS instance.

-   Does a primary/secondary switchover trigger changes to the endpoints and port numbers of my RDS instance?

    No, a primary/secondary switchover does not trigger changes to the endpoints or port numbers of your RDS instance. Only the IP addresses associated with the endpoints change. Your application can still connect to your RDS instance by using the endpoints.


## References

For more information about how to enable, change, and disable a proxy endpoint, see [Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md).

