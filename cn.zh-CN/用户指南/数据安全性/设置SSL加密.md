# 设置SSL加密 {#concept_ack_rv4_ydb .concept}

为了提高链路安全性，您可以启用SSL（Secure Sockets Layer）加密，并安装SSL CA证书到需要的应用服务。SSL在传输层对网络连接进行加密，能提升通信数据的安全性和完整性，但会同时增加网络连接响应时间。

## 前提条件 {#section_dgv_5z0_yuz .section}

实例版本如下：

-   SQL Server所有版本
-   MySQL 8.0高可用版
-   MySQL 5.7高可用版
-   MySQL 5.6

## 注意事项 {#section_1x1_k93_5w2 .section}

-   SSL的证书有效期为1年，请在1年内更新证书有效期，否则使用加密连接的客户端程序将无法正常连接。
-   由于SSL加密的固有缺陷，启用SSL加密会显著增加CPU使用率，建议您仅在外网链路有加密需求的时候启用SSL加密。内网链路相对较安全，一般无需对链路加密。
-   SQL Server实例开启SSL加密后，将无法再关闭，请谨慎操作。
-   读写分离地址不支持SSL加密。

## 开启SSL加密 {#section_hjf_z54_ydb .section}

1.  登录 [RDS 管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156655435537169_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧菜单栏中单击**数据安全性**。
5.  选择**SSL**标签页。
6.  单击**未开通**前面的开关，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/15665543554147_zh-CN.png)

7.  在设置 SSL对话框中选择要开通SSL加密的链路，单击**确定**，开通 SSL 加密。

    **说明：** 用户可以根据需要，选择加密内网链路或者外网链路，但只可以加密一条链路。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/15665543554148_zh-CN.png)

8.  单击**下载证书**，下载SSL CA证书，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/15665543554149_zh-CN.png)

    下载的文件为压缩包，包含如下三个文件：

    -   p7b文件：用于Windows系统中导入CA证书。

    -   PEM文件：用于其他系统或应用中导入CA证书。

    -   JKS文件：java中的truststore证书存储文件，密码统一为apsaradb，用于java程序中导入CA证书链。

        **说明：** 在java中使用JKS证书文件时，jdk7和jdk8需要修改默认的jdk安全配置，在需要SSL访问的数据库所在机器的`jre/lib/security/java.security`文件中，修改如下两项配置：

        ``` {#codeblock_87r_f11_zem}
        jdk.tls.disabledAlgorithms=SSLv3, RC4, DH keySize < 224
        jdk.certpath.disabledAlgorithms=MD2, RSA keySize < 1024
        ```

        若不修改jdk安全配置，会报如下错误。其它类似报错，一般也都由java安全配置导致。

        ``` {#codeblock_vm7_4rt_jox}
        javax.net.ssl.SSLHandshakeException: DHPublicKey does not comply to algorithm constraints
        ```


## 配置SSL CA证书 {#section_mdn_nv4_ydb .section}

开通SSL加密后，应用或者客户端连接RDS时需要配置SSL CA证书。本文以MySQL Workbench为例，介绍SSL CA证书安装方法。其它系统、应用、客户端或者程序请使用正确类型的CA证书文件。

1.  打开MySQL Workbench。
2.  选择**Database** \> **Manage Connections** 。
3.  在**Use SSL**栏选择If avaliable。
4.  在**SSL CA File**栏单击...选择PEM文件。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/15665543564150_zh-CN.png)


## 更新证书有效期 {#section_q09_pr3_6zz .section}

SSL的证书有效期为1年，请在1年内更新证书有效期，否则使用加密连接的客户端程序将无法正常连接。

**说明：** **更新有效期**操作将会重启实例，重启前请做好业务安排，谨慎操作。

![更新证书有效期](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7949/156655435645367_zh-CN.png)

## 关闭MySQL实例SSL加密 {#section_374_d4f_5si .section}

1.  登录 [RDS 管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![选择地域](../DNmysql1824527/../DNMYSQ1820581/images/36543_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧菜单栏中单击**数据安全性**。
5.  选择**SSL**标签页。
6.  单击**已开通**前面的开关，在弹出的提示框中单击**确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41826/156655435657405_zh-CN.png)


