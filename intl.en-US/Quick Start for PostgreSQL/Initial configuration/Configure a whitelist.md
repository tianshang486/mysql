# Configure a whitelist {#concept_sfx_kdg_wdb .concept}

To ensure database security and stability, before using RDS instances, you must whitelist the IP addresses or IP address segments that need to access the database. We recommend that you periodically check and adjust your whitelist according to your requirements to maintain RDS security. This document provides information about and the procedure of setting a whitelist.

## Background {#section_iht_ndg_wdb .section}

You can access the RDS instance through the intranet, the Internet, or both the intranet and Internet. For more information about the applicable scenarios of each connection type \(intranet and Internet\), see **Background** of [Set connection addresses](../../../../intl.en-US/User Guide/Connection management/Set connection addresses.md#).

-   Access the RDS instances through the intranet.
-   Access the RDS instances through the Internet.
-   Access the RDS instances through both the intranet and Internet.

Before setting the connection type, you must add the IP addresses or IP address segments of your application service or the ECS instance to the whitelist of your RDS instance. When the whitelist is set, the system automatically generates the intranet IP address for the RDS instance. If you need an Internet IP address, refer to [Apply for an Internet address](intl.en-US/Quick Start for PostgreSQL/Initial configuration/Apply for an Internet address.md).

**Note:** If you cannot connect to the RDS instance after adding the application service IP address to the whitelist, you must obtain the actual IP address of the application service.

## Attention {#section_nzr_pdg_wdb .section}

-   The system automatically creates a **default** whitelist group for each newly created RDS instance. This default whitelist group can only be modified or cleared, but cannot be deleted.
-   For each newly created RDS instance, the local loopback IP address 127.0.0.1 is added to the **default** whitelist group by default. This means that all the IP addresses or IP address segments are prohibited to access this RDS instance. Therefore, you must delete 127.0.0.1 from the default whitelist group before you add other IP addresses or IP address segments to the RDS whitelist.
-   % or 0.0.0.0/0 indicates any IP address is allowed to access the RDS instance. This configuration greatly reduces the security of the database and is not recommended.

## Procedure {#section_d1f_rdg_wdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.
3.  Click the name of the target instance to go to the Basic Information page.
4.  Select **Security Controls** in the left-side navigation pane to visit the Security Controls page.
5.  On the Whitelist Settings tab page, click **Modify** of the **default** whitelist group, as shown in the following figure.

    **Note:** If you want to add a customized whitelist group to the RDS instance, you can click **Clear** of the **default** whitelist group to delete the IP address 127.0.0.1 first, and then click **Add a Whitelist Group**. The setting steps for a customized whitelist are similar to the following steps.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7848/15663504752956_en-US.png)

6.  On the Modify Group page, add the IP addresses or IP address segments to access the RDS instance to the Whitelist field. If you want to add the ECS intranet IP addresses, click **Upload ECS Intranet IP Address** and select the IP addresses according to the prompt window, as shown in the following figure.

    **Note:** After you add a new IP address or IP address segment to the **default** group, the loopback address 127.0.0.1 is automatically deleted.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7848/15663504752957_en-US.png)

    Parameters description:

    -   Group Name: It contains 2 to 32 characters including lowercase letters, digits, or underscores \(\_\). The group name must start with a lowercase letter and end with a letter or digit. This name cannot be modified once the whitelist group is successfully created.
    -   Whitelist: Enter the customized IP addresses or IP segments that are allowed to access the RDS instance.
        -   If you enter an IP address segment, such as 10.10.10.0/24, it indicates that any IP address in the format of 10.10.10.X can access the RDS instance.
        -   If you want to enter multiple IP addresses or IP address segments, separate them by commas \(,\) \(do not add blank spaces\), such as 192.168.0.1,172.16.213.9.
        -   For each whitelist group, up to 1,000 IP addresses or IP address segments can be set for MySQL, PostgreSQL, and PPAS instances and up to 800 can be set for SQL Server instances.
    -   Upload ECS intranet IP Address: By clicking this button, you can select the intranet IP address of the ECS instance under the same account as the RDS instance. This is a quick method to add ECS intranet IP address.
7.  Click **OK**.

## Modify or delete the whitelist group {#section_bn2_fff_vdb .section}

You can modify or delete the whitelist group according your business requirements. The detailed procedure is as follows:

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.
3.  Click the name of the target instance to go to the **Basic Information** page.
4.  Select **Security** in the left-side navigation pane.
5.  On the **Whitelist Settings** tab page, click **Modify** or **Delete** of the target whitelist group.
6.  Click **OK** after you modify the IP addresses or IP address segments. Alternatively, click **Confirm** if you are sure that the whitelist group is to be deleted.

