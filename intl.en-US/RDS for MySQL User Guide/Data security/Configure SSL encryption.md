# Configure SSL encryption {#concept_ack_rv4_ydb .concept}

This topic describes how to enable Secure Sockets Layer \(SSL\) encryption and install SSL CA certificates to applications. SSL encrypts data over network connections at the transport layer. This enhances data security and integrity but increases network connection response time.

## Prerequisites {#section_lns_6e8_mca .section}

The DB engine versions and editions that support SSL encryption are as follows:

-   MySQL 8.0 High-availability Edition
-   MySQL 5.7 High-availability Edition
-   MySQL 5.6

## Precautions {#section_68t_1qf_ymg .section}

-   The validity period of an SSL CA certificate is one year. You must renew the validity period of the SSL CA certificate in your application or client within one year. Otherwise, your application or client that uses an encrypted network connection cannot connect to RDS properly.
-   SSL encryption increases CPU usage. Therefore, we recommend that you enable SSL encryption only for public endpoints when required. In typical cases, private endpoints do not require SSL encryption.
-   Read/write splitting addresses do not support SSL encryption.
-   Disabling SSL encryption restarts your RDS instance.

## Enable SSL encryption {#section_hjf_z54_ydb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156698823836543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  Click the **SSL Encryption** tab.
6.  Click the switch next to **Disabled** in the **SSL Encryption** parameter.

    ![开启SSL加密](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/15669882384147_en-US.png)

7.  In the Configure SSL dialog box, select the endpoint for which you want to enable SSL encryption, then click **OK**.

    **Note:** You can choose to encrypt the private or public endpoint, but note that you can encrypt only one endpoint.

    ![开启SSL加密-选择加密地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/15669882384148_en-US.png)

8.  Click **Download CA Certificate** to download the SSL CA certificate files in a compressed package.

    ![下载SSL加密CA证书](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/15669882384149_en-US.png)

    The compressed package consists of the following three files:

    -   .p7b file: used to import CA certificate files in Windows operating systems.
    -   .pem file: used to import CA certificate files in other systems or applications.
    -   .jks file: used to import link CA certificate files in Java-based applications. The .jks file is stored in the TrustStore of Java.

        **Note:** When you use the .jks file in JDK 7 or JDK 8, you must modify the default JDK security configuration. Specifically, you must find the jre/lib/security/java.security file on the server where the database you want to access through SSL is located, and then reconfigure the file as follows:

        ``` {#codeblock_w55_efr_tml}
        jdk.tls.disabledAlgorithms=SSLv3, RC4, DH keySize < 224
        jdk.certpath.disabledAlgorithms=MD2, RSA keySize < 1024
        ```

        If you do not modify the JDK security configuration, the system reports errors similar to the following:

        ``` {#codeblock_lj1_hj3_avl}
        javax.net.ssl.SSLHandshakeException: DHPublicKey does not comply to algorithm constraints
        ```


## Configure the SSL CA certificate {#section_mdn_nv4_ydb .section}

After SSL encryption is enabled, you must configure the SSL CA certificate for your application or client when connecting to RDS. This section uses MySQL Workbench as an example to describe how to install the SSL CA certificate.

1.  Start MyQL Workbench.
2.  Choose **Database** \> **Manage Connections**.
3.  Enable **Use SSL** and import the SSL CA certificate files.

    ![配置SSL CA证书-使用MySQL Workbench](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/15669882384150_en-US.png)


## Renew the validity period of the SSL CA certificate {#section_42v_8li_qjg .section}

**Note:** This operation causes your RDS instance to restart. You must make proper service arrangements before this operation.

![更新证书有效期](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/156698823845367_en-US.png)

## Disable SSL encryption {#section_n1y_3dp_imh .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156698823836543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  Click the **SSL Encryption** tab.
6.  Click the switch next to **Enabled** in the **SSL Encryption** parameter. In the displayed Disable SSL Encryption dialog box, click **OK**.

    ![关闭SSL加密](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41826/156698823857405_en-US.png)


