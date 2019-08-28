# Configure SSL encryption {#concept_ack_rv4_ydb .concept}

This topic describes how to enable Secure Sockets Layer \(SSL\) encryption and install SSL CA certificates to applications. SSL encrypts data over network connections at the transport layer. This enhances data security and integrity but increases network connection response time.

## Prerequisites {#section_dgv_5z0_yuz .section}

The DB engine versions and editions that support SSL encryption are as follows:

-   All SQL Server versions and editions
-   MySQL 8.0 High-availability Edition
-   MySQL 5.7 High-availability Edition
-   MySQL 5.6

## Precautions {#section_1x1_k93_5w2 .section}

-   The validity period of an SSL CA certificate is one year. You must renew the validity period of the SSL CA certificate in your application or client within one year. Otherwise, your application or client that uses an encrypted network connection cannot connect to RDS properly.
-   SSL encryption increases CPU usage. Therefore, we recommend that you enable SSL encryption only for public endpoints when required. In typical cases, private endpoints do not require SSL encryption.
-   SSL encryption cannot be disabled once it is enabled for an RDS for SQL Server instance.
-   Read/write splitting addresses do not support SSL encryption.

## Enable SSL encryption {#section_hjf_z54_ydb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156698853037169_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  Click the **SSL Encryption** tab.
6.  Click the switch next to **Disabled** in the **SSL Encryption** parameter.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/15669885304147_en-US.png)

7.  In the Configure SSL dialog box, select the endpoint for which you want to enable SSL encryption, then click **OK**.

    **Note:** You can choose to encrypt the private or public endpoint, but note that you can encrypt only one endpoint.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/15669885304148_en-US.png)

8.  Click **Download CA Certificate** to download the SSL CA certificate files in a compressed package.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/15669885304149_en-US.png)

    The compressed package consists of the following three files:

    -   .p7b file: used to import CA certificate files in Windows operating systems.
    -   .pem file: used to import CA certificate files in other systems or applications.
    -   .jks file: used to import link CA certificate files in Java-based applications. The .jks file is stored in the TrustStore of Java.

        **Note:** When you use the .jks file in JDK 7 or JDK 8, you must modify the default JDK security configuration. Specifically, you must find the `jre/lib/security/java.security` file on the server where the database you want to access through SSL is located, and then reconfigure the file as follows:

        ``` {#codeblock_87r_f11_zem}
        jdk.tls.disabledAlgorithms=SSLv3, RC4, DH keySize < 224
        jdk.certpath.disabledAlgorithms=MD2, RSA keySize < 1024
        ```

        If you do not modify the JDK security configuration, the system reports errors similar to the following:

        ``` {#codeblock_vm7_4rt_jox}
        javax.net.ssl.SSLHandshakeException: DHPublicKey does not comply to algorithm constraints
        ```


## Configure the SSL CA certificate {#section_mdn_nv4_ydb .section}

After SSL encryption is enabled, you must configure the SSL CA certificate for your application or client when connecting to RDS. This section uses MySQL Workbench as an example to describe how to install the SSL CA certificate.

1.  Start MySQL Workbench.
2.  Choose **Database** \> **Manage Connections** .
3.  Select If avaliable from the **Use SSL** drop-down list.
4.  In the **SSL CA File** field, click .... Then, select the .pem file.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/15669885304150_en-US.png)


## Renew the validity period of the SSL CA certificate {#section_q09_pr3_6zz .section}

**Note:** **This operation** causes your RDS instance to restart. You must make proper service arrangements before this operation.

![更新证书有效期](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/156698853045367_en-US.png)

## Disable SSL encryption {#section_374_d4f_5si .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156698853036543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  Click the **SSL Encryption** tab.
6.  Click the switch next to **Enabled** in the **SSL Encryption** parameter. In the displayed Disable SSL Encryption dialog box, click **OK**.

    ![关闭SSL加密](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41826/156698853057405_en-US.png)


