# Apply for an Internet address {#concept_nsl_hff_vdb .concept}

RDS provides two types of address: intranet address and Internet address.

## Intranet and Internet addresses {#section_j61_zy0_6ms .section}

|Address|Description|
|-------|-----------|
|Intranet address| The intranet address is generated by default.

 Use the intranet address if **all** of the following conditions are met:

 -   Your application is deployed on an ECS instance.
-   The ECS instance is located in the same region as your RDS instance.
-   The ECS instance has the same [network type](../../../../intl.en-US/User Guide/Connection management/Set network type.md) as your RDS instance.

 The intranet address is recommended because accessing RDS through the intranet is most secure and delivers optimal performance.|
|Internet address|You need to manually apply for the Internet address. You can also release it anytime. Use the Internet address if you cannot access RDS through the intranet. Specific scenarios are as follows:

 -   An ECS instance accesses your RDS instance but the ECS instance is located in a different region or has a network type different from your RDS instance.
-   A server or computer outside Alibaba Cloud accesses your RDS instance.

 **Note:** 

-   The Internet address and traffic are currently free of charge.
-   Using the Internet address reduces security. Please exercise caution.
-   To ensure high security and performance, it is recommended that you migrate your application to an ECS instance that is in the same region and has the same network type as your RDS instance and then use the intranet address.

 |

## Apply for an Internet address {#section_nhs_4g3_9dn .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/?spm=5176.doc43185.2.7.mR2Syx).
2.  In the upper-left corner, select the region where the RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7817/155715746141362_en-US.png)

3.  Find the RDS instance and click its ID.
4.  In the left-side navigation pane, choose **Connection Options**.
5.  Click **Apply for Internet Address**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7817/15571574611802_en-US.png)

6.  In the displayed dialog box, click **OK**.

    The Internet address is generated.

    **Note:** You can view the Internet address only after the [whitelist](intl.en-US/Quick Start for MySQL/Initial configuration/Set the whitelist.md) is configured.

7.  \(Optional\) To modify the Internet address or port number, click **Modify Connection Address**. In the displayed dialog box, set the Internet address and port number and click **OK**.

    -   **Connection Type**: Select **Internet address**.

        **Note:** This option is available only after you have applied for the Internet address.

    -   **Connection Address**: You can modify the address prefix, which consists of 8 to 30 characters, including letters and digits, and starts with a lower-case letter.
    -   **Port**: The port number can be modified only if the RDS network type is classic network.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7817/15571574611805_en-US.png)


## Related API {#section_9n7_g9r_esa .section}

|API|Description|
|---|-----------|
|[Apply for an Internet connection string](../../../../intl.en-US/API Reference/Network management/Apply for an Internet connection string.md#)|Apply for an Internet address.|
