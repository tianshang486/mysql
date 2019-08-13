# Apply for an Internet address {#concept_zx5_ytg_wdb .concept}

If your application is deployed on the ECS instance that is located in the same region and has the same [network type](../intl.en-US/User Guide/Instance management/Set network type.md#) as your RDS instance, you do not need an Internet address. If your application is deployed on the ECS that is located in the different region or has the different network type from those of your RDS instance, or on a platform other than Alibaba Cloud, an Internet address is necessary to access an RDS instance.

**Note:** When instances are in the same region \(their zones can be different\), they can access each other through the intranet.

## Background information {#section_eh3_c5g_wdb .section}

RDS supports connections through the intranet and Internet. The [access mode](../intl.en-US/User Guide/Connection management/Disabling the database proxy mode.md#) and [instance type](../intl.en-US/Product Introduction/Instance types/Instance type list.md#) of the instance determine available connection types.

|Instance series|Instance version|Access mode|Connection address|
|---------------|----------------|-----------|------------------|
|Basic Edition| -   MySQL 5.7
-   SQL Server 2016 Web Basic Edition/2012 Web Basic Edition/2012 Enterprise Basic Edition
-   PostgreSQL 10

 |Standard whitelist mode| -   Intranet address
-   Internet address
-   Intranet and Internet addresses

 |
|High-availability Edition| -   MySQL 5.5/5.6/5.7
-   SQL Server 2008 R2/2016 Standard High-availability Edition/2012 Standard High-availability Edition/2016 Enterprise High-availability Edition/2012 Enterprise High-availability Edition
-   PostgreSQL 9.4
-   PPAS 10

 |Standard whitelist mode| -   Intranet address
-   Internet address

 |
|Enhanced whitelist mode| -   Intranet address
-   Internet address
-   Intranet and Internet addresses

 |
|Finance Edition|MySQL 5.6|Standard whitelist mode| -   Intranet address
-   Internet address

 |
|Enhanced whitelist mode| -   Intranet address
-   Internet address
-   Intranet and Internet addresses

 |

The applicable scenarios of the connection addresses are as follows:

-   Use the intranet address only:
    -   The system provides an intranet address by default and you can directly modify the connection address.
    -   This condition is applicable when your application is deployed on an ECS instance that is located in the same region and has the same [network type](../intl.en-US/User Guide/Instance management/Set network type.md#) as your RDS instance.
-   Use the Internet address only:
    -   This condition is applicable when your application is deployed on an ECS instance that is located in the different region from that of your RDS instance.
    -   This condition is applicable when your application is deployed on a platform other than Alibaba Cloud.
-   Use both intranet and Internet addresses:
    -   This scenario is applicable when your application is deployed on an ECS instance that is located in the same region and has the same [network type](../intl.en-US/User Guide/Instance management/Set network type.md#) as your RDS instance, and application modules are deployed in an ECS where your RDS instance is not located.
    -   This scenario is applicable when your application is deployed on an ECS instance that is located in the same region and has the same [network type](../intl.en-US/User Guide/Instance management/Set network type.md#) as your RDS instance, and on a platform other than Alibaba Cloud.

## Precautions {#section_hwz_s4y_r2b .section}

-   Before accessing the database, you must add the addresses or CIDR blocks to a whitelist. For more information, see [Set the whitelist](../intl.en-US/User Guide/Security/Set the whitelist.md#).
-   Traffic fees are charged for connections through Internet. For more information about pricing and fees charging, see [RDS Pricing](https://www.alibabacloud.com/product/apsaradb-for-rds?spm=a2c63.p38356.a3.8.27427f39WeCYZ1#pricing).
-   Connecting the RDS instance through an Internet address may reduce the instance security. Proceed with caution. To get a higher transmission rate and a higher security level, we recommend that you migrate your applications to an ECS instance that is in the same region as your RDS instance.

## Procedure {#section_npv_7q8_k8o .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567844736543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Database Connection**.
5.  Click **Apply for Public Endpoint**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7861/15656784484046_en-US.png)

6.  In the displayed dialog box, click **OK**.
7.  Click **Change Endpoint**, and in the displayed dialog box change the address and port number of the instance.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7861/15656784482972_en-US.png)

    Parameter description:

    -   **Connection Type**: Select **Internet Endpoint** or **Intranet Endpoint**.
    -   **Endpoint**: The address format is `xxx.mysql.rds.aliyuncs.com`, where xxx is a user-defined field. The address contains 8 to 64 characters including letters and digits. It must begin with a lowercase letter.
    -   **Port**: The number of the port through which RDS provides external services. The port number can be an integer within the range \[3200, 3999\].
8.  Click **OK**.

