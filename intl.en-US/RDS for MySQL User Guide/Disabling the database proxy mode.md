# Disabling the database proxy mode {#concept_jlf_hpq_wdb .concept}

Disabling the database proxy mode helps to increase RDS instance performance.

**Note:** The database proxy mode may cause service instability in certain circumstances. For smooth service operation, we recommend that you upgrade the network connection mode of your RDS instance as soon as possible. For more information, see [\[Important\] RDS network link upgrade](../DNMYSQ1821992/EN-US_TP_64586.md#).

## Precautions {#section_lcz_9kl_9wm .section}

-   In the database proxy mode, the multi-statement function is enabled by default at the protocol layer. Therefore, after you disable the database proxy mode, if you do not enable the multi-statement function but run multiple SQL statements, the system reports errors in the SQL statements. To prevent this problem, you must check and add connection parameters in advance. For example, you can add the allowMultiQueries parameter to JDBC as follows:

    ``` {#codeblock_ve0_dw3_79l}
    dbc:mysql:///test?allowMultiQueries=true
    ```

-   You can only disable the database proxy mode \(that is, switch from the database proxy mode to the standard mode\). However, you cannot enable the database proxy mode \(that is, switch from the standard mode to the database proxy mode\).
-   During the access mode switching, your RDS instance may be disconnected once for about 30 seconds. We recommend that you perform the switching during off-peak hours or make sure that your application can automatically reconnect to the RDS instance.

## Prerequisites {#section_f2u_ly8_ivg .section}

The database proxy mode is enabled for your RDS instance.

**Note:** 

-   If the **Database Proxy** tab is displayed, the database proxy mode is enabled and you can proceed with the operations described in this topic.
-   If the **Database Proxy** tab is not displayed, the database proxy mode is not displayed and you can skip this topic.

![数据库代理页签](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7942/156747625139637_en-US.png)

## Procedure {#section_8wn_61e_s6u .section}

**Method 1**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156747625236543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Database Connection**.
5.  Click **Switch Access Mode**.

    ![数据库连接](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41816/156747625237541_en-US.png)

    **Note:** This button is available only if you have enabled the database proxy mode.


**Method 2**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156747625236543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Database Proxy**.
5.  On the **Database Proxy** tab, click the slider to turn on or off the database proxy mode.

    **Note:** This tab page is available only if you have enabled the database proxy mode.


