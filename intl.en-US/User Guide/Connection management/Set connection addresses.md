# Set connection addresses {#concept_tv3_pq1_ydb .concept}

RDS supports two types of connection addresses: intranet IP addresses and Internet IP addresses.

## Intranet and Internet IP addresses {#section_8sw_rkp_hiw .section}

|Connection Address Type|Description|
|-----------------------|-----------|
|Intranet IP addresses| -   An intranet IP address is provided by default. This intranet IP address cannot be released. However, you can change the network type.
-   If the following conditions are met, you do not need to apply for an Internet IP address:
    -   Your application is deployed on an ECS instance.
    -   The ECS instance is located in the same region as your RDS instance.
    -   The network type of the ECS instance is the same as that of your RDS instance. For more information, see [Set network type](intl.en-US/User Guide/Instance management/Set network type.md#).
-   Accessing your RDS instance through an intranet IP address enhances security and RDS instance performance.

 |
|Internet IP addresses| -   To obtain an Internet IP address, you need to manually apply for one. You can release it when it is no longer needed.
-   If you cannot access your RDS instance through an intranet IP address, you need to apply for an Internet IP address. For example:
    -   You access your RDS instance from an ECS instance that is located in a different region or have a different network type from your RDS instance. For more information, see [Set network type](intl.en-US/User Guide/Instance management/Set network type.md#).
    -   You access your RDS instance from a device that is not provided by Alibaba Cloud.

 **Note:** 

-   Accessing your RDS instance through an Internet IP address reduces security. Exercise caution when you do so.
-   To increase transmission speed and security, we recommend that you migrate your application to an ECS instance that is located in the same region and have the same network type as your RDS instance, so that you can access your RDS instance by using an intranet IP address.

 |

## Apply for or release an Internet IP address {#section_adc_sr1_ydb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.
3.  Click the ID of the instance to visit the Basic Information page.
4.  In the left-side navigation pane, click **Database Connection**.
5.  Apply for or release the Internet IP address.
    -   If you have applied for an Internet IP address for the instance, click **Apply for Public Connection Address**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7945/15656636773991_en-US.png)

    -   If you have not applied for an Internet IP address for the instance, click **Release Internet Address**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7945/156566367750909_en-US.png)

6.  In the displayed confirmation dialog box, set the parameters and click **OK**.

## Modify an intranet or Internet IP address {#section_upj_cs1_ydb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.
3.  Click the ID of the instance to visit the Basic Information page.
4.  In the left-side navigation pane, click **Database Connection**.
5.  Click **Modify Connection Address**.
6.  In the displayed dialog box, select a connection type, set the connection address and port, and click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7945/15656636773992_en-US.png)

    **Note:** 

    -   The connection address starts with a prefix that contains lowercase letters and contains 8 to 64 characters including letters, digits, and hyphens \(-\).
    -   If your RDS instance runs in a VPC, you cannot change the port of the Internet or intranet IP address.
    -   If your RDS instance runs in a classic network, you can change the port of the Internet or intranet IP address as needed.

## APIs {#section_3ty_0jo_lhg .section}

|API|Description|
|---|-----------|
|[AllocateInstancePublicConnection](../../../../intl.en-US/API Reference/Network management/AllocateInstancePublicConnection.md#)|Applies for an Internet IP address for your RDS instance.|
|[ReleaseInstancePublicConnection](../../../../intl.en-US/API Reference/Network management/ReleaseInstancePublicConnection.md#)|Releases the IP address of your RDS instance.|

