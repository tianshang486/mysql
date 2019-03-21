# Apply for an Internet address {#concept_nsl_hff_vdb .concept}

If your application is deployed on an ECS instance that is located in the same region and has the same [network type](../../../../../intl.en-US/User Guide/Connection management/Set network type.md) as your RDS instance, you do not need an Internet IP address. If your application is deployed on an ECS that is located in a different region or has a network type different from your RDS instance, or is deployed on a platform other than Alibaba Cloud, an Internet IP address is necessary for access to the RDS instance.

## Background information {#section_x5z_5ff_vdb .section}

RDS supports connections through the intranet and Internet. The [series](../../../../../intl.en-US/Product Introduction/Product series/Product series overview.md), version, and [access mode](../../../../../intl.en-US/User Guide/Connection management/Set the access mode.md) of the instance determine available connection types.

|Series|Version|Access mode|Connection address|
|------|-------|-----------|------------------|
|Basic Edition| -   MySQL 5.7
-   SQL Server 2012

 |Standard mode| -   Intranet IP address
-   Internet IP address
-   Both intranet and Internet IP addresses

 |
|High-availability Edition| -   MySQL 5.5/5.6
-   SQL Server 2008 R2
-   PostgreSQL 9.4
-   PPAS 9.3

 |Standard mode| -   Intranet IP address
-   Internet IP address

 |
|Safe connection mode| -   Intranet IP address
-   Internet IP address
-   Both intranet and Internet IP addresses

 |

The applicable scenarios of the connection addresses are as follows:

-   Use the intranet IP address only:
    -   The system provides an intranet IP address by default, and you can directly modify the connection address.
    -   This scenario is applicable when your application is deployed on an ECS instance that is located in the same region and has the same [network type](../../../../../intl.en-US/User Guide/Connection management/Set network type.md) as your RDS instance.
-   Use the Internet IP address only:
    -   This scenario is applicable when your application is deployed on an ECS instance that is located in a region different from that of your RDS instance.
    -   This scenario is applicable when your application is deployed on a platform other than Alibaba Cloud.
-   Use both the intranet and Internet IP addresses:
    -   This scenario is applicable when your application is deployed on both: \(1\) An ECS instance that is in the same region and has the same [network type](../../../../../intl.en-US/User Guide/Connection management/Set network type.md) as your RDS instance; \(2\) An ECS instance that is in a region different from your RDS instance.
    -   This scenario is applicable when your application is deployed on both: \(1\) An ECS instance that is in the same region and has the same [network type](../../../../../intl.en-US/User Guide/Connection management/Set network type.md) as your RDS instance; \(2\) A platform other than Alibaba Cloud.

## Attentions { .section}

-   Before accessing an RDS instance, add IP addresses or IP address segments to the whitelist. Otherwise, they cannot access the RDS instance. For more information, see [Set a whitelist](intl.en-US/Quick Start for MySQL/Initial configuration/Set the whitelist.md#).
-   Traffic fees are charged for connections through Internet. For more information about pricing and fees charging, see RDS pricing.
-   Connecting the RDS instance through an Internet IP address may reduce the instance security. Proceed with caution. To get a higher transmission rate and a higher security level, we recommend that you migrate your applications to an ECS instance that is in the same region as your RDS.

## Procedure { .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/?spm=5176.doc43185.2.7.mR2Syx).
2.  Select the region where the target instance is located.
3.  Click the ID of the instance to visit the **Basic Information** page.
4.  Select **Connection Options** in the left-side navigation pane.
5.  Click **Apply for Internet Address**, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7817/15531747281802_en-US.png)

6.  On the displayed confirmation window, click **OK** to generate an Internet IP address.
7.  Click **Modify Connection Address** and modify the connection address and port of the Internet or intranet.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7817/15531747281805_en-US.png)

    Parameter description:

    -   Connection Type: Select **intranet address** or **Internet address** according to the connection type to be modified.
    -   Connection Address: The address format is `xxx.sqlserver.rds.aliyuncs.com` and *xxx* is a user-defined field. The address contains 8 to 64 characters including letters and digits. It must begin with a lower-case letter.
    -   Port: indicates the number of the port through which RDS provides external services, which can be an integer within the range \[3200, 3999\].
8.  Click **OK**.

